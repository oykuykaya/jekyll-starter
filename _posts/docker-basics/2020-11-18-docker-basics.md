---
layout: default
comments: True
categories: jekyll update
regenerate: true
description: Cron jobs ensure to automate and schedule python jobs.
title: Docker Basics
date: "2020-11-18 11:50:00"
description: "In this tutorial, I'll list most usefull docker commands."
---

In this tutorial, I'll list most usefull docker commands.


If you would like to search entity on docker hub, use <code>docker search</code>

```bash
docker search nginx
```

```bash
docker run --name my-nginx -P -d nginx
```

To get more details about container, use  <code>docker inspect </code>

```bash
docker ls -a # --all could is same.
docker inspect <container-id>
docker stop <container-id>
docker rm <container-id>
docker start <container-id>
```

To controll over image, use following commands

```
docker image ls
docker image rm <image-id>
```

### Environment Variables

First, docker pulls the  <code>ubuntu </code> image. Then, set environment variables. Thereafter, we can lookup the variable value.

```bash
docker run -e ENV_VAR1=myvalue1 ubuntu env | grep ENV_VAR
```



### Container Logs

```bash
docker container ls -a
docker logs <container-id>
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