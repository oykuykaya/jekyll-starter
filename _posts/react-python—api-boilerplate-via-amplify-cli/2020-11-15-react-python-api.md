---
layout: default
comments: True
categories: jekyll update
title: React + Python API Boilerplate via Amplify CLI
date: "2020-11-15"
description: "In this tutorial, I'll try to let you know how to create a web application stack using AWS Amplify CLI."
---
In this tutorial, I'll try to let you know how to create a web application stack using AWS Amplify CLI.

* Fornt-end: React Framework, JS, CSS, Html
* Back-end: Python 3, Serverless Lambda.

### Prerequisetes

* Nodejs, NPX and NPM package managers

* AWS CLI, AWS Amplify CLI 

  ```shell
  npm install -g @aws-amplify/cli
  ```

We will first <code>create-react-app</code> :

```shell
npx create-react-app gallery-app
cd gallery-app
```

```shell
amplify init
amplify add api
amplify push
```

:warning:	To activate this project's virtualenv, run pipenv shell.

Selecting path as <code>/gallery</code>  on <code>amplify add api</code>	stage. This only alows requests to the specific path.

```python
curl -X POST -H "Content-Type: application/json" -d '{"bucket":"umutyalcinkaya", "key":"images/bye.png"}' https://ixjg1ibb61.execute-api.eu-west-1.amazonaws.com/dev/gallery

```

### Creating Pre-signed URL

```python
import boto3
from io import StringIO
import logging
from botocore.exceptions import ClientError
from botocore.config import Config
import requests 
import json

config = Config(
   retries = {
      'max_attempts': 10,
      'mode': 'standard'
   }
)

s3 = boto3.client('s3', config=config)

# Create public link to share html
def create_presigned_url(bucket, key, expiration=3600, method_parameters=None ,http_method=None): # Maximum 7 days: 1 week expiration value
    """Generate a presigned URL to share an S3 object

    :param bucket_name: string
    :param object_name: string
    :param expiration: Time in seconds for the presigned URL to remain valid
    :return: Presigned URL as string. If error, returns None.
    """
    try:
        response = s3.generate_presigned_url(
            'get_object',
            Params={'Bucket': bucket,
                    'Key': key},
            ExpiresIn=expiration)
    except ClientError as e:
        logging.error(e)
        return None

    # The response contains the presigned URL
    return response

def handler(event, context):

  url = create_presigned_url(bucket=event['bucket'], key=event['key']) # 'umutyalcinkaya' , 'images/bye.png'

  if url is not None:
    response = requests.get(url)

  body = {
    "message":"{}".format(url)
  }
  
  result = {
    "statusCode": 200,
    "body": json.dumps(body),
    "headers": {
      "Content-Type":"application/json",
      "Access-Control-Allow-Origin":"*"
    }
  }

  return result
```

### Reading base64 image 

```python
import base64
import boto3
import json
import random

s3 = boto3.client('s3')

def handler(event, context):
    number = 1
    if number == 1:
        response = s3.get_object(
            Bucket='umutyalcinkaya',
            Key='images/hi.png',
        )
        image = response['Body'].read()
        return {
            'headers': { "Content-Type": "image/png" },
            'statusCode': 200,
            'body': base64.b64encode(image).decode('utf-8'),
            'isBase64Encoded': True
        }
    else:
        return {
            'headers': { "Content-type": "text/html" },
            'statusCode': 200,
            'body': "<h1>Image does not exist. Will soon checkout :) </h1>",
        }
```
{% if page.comments %} 
<div id="disqus_thread"></div>
<script>
    /**
    *  RECOMMENDED CONFIGURATION VARIABLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS.
    *  LEARN WHY DEFINING THESE VARIABLES IS IMPORTANT: https://disqus.com/admin/universalcode/#configuration-variables    */
    /*
    var disqus_config = function () {
    this.page.url = PAGE_URL;  // Replace PAGE_URL with your page's canonical URL variable
    this.page.identifier = PAGE_IDENTIFIER; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
    };
    */
    (function() { // DON'T EDIT BELOW THIS LINE
    var d = document, s = d.createElement('script');
    s.src = 'https://blog-umutykaya-com.disqus.com/embed.js';
    s.setAttribute('data-timestamp', +new Date());
    (d.head || d.body).appendChild(s);
    })();
</script>
<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
{% endif %}