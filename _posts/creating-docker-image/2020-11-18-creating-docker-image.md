---
layout: default
comments: True
categories: jekyll update
title: Creating Docker Image
date: "2020-11-18 13:58:00"
description: "In this article, I'll tell about how to create your own docker images."
---

In order to make our own image, we are using <code>Dockerfile</code>

```bash
cat > Dockerfile <<EOF
heredoc> FROM busybox
heredoc> CMD echo "Hello world! This is my first Docker image."
heredoc> EOF
```

```bash
docker build -t first-container .
docker image ls
docker run first-container
```

### Ubuntu Nginx Image

As shown in the below prompt, the  <code>Dockerfile</code> that we are using to execute  <code>Ubuntu</code> image.

```dockerfile
FROM ubuntu:latest
RUN DEBIAN_FRONTEND=noninteractive apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get -yq install net-tools nginx
EXPOSE 80
ENTRYPOINT ["/usr/sbin/nginx", "-g", "daemon off;"]
```

Then we're building and running it.

* -d: running docker container background.
* -p: port mappings <code>host-port:container-port</code>

```bash
docker build -t my-nginx .
docker image ls
docker run -d -p 8888:80 my-nginx
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