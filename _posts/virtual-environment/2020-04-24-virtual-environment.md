---
layout: default
comments: True
categories: jekyll update
regenerate: true
title: Virtual Environment
date: "2020-04-24 16:15:10"
description: "Cron jobs ensure to automate and schedule python jobs."
---

Developers deealing with virtual environment to execute python codes, isolated from system packages and dependencies.

### Activate:
```Shell
virtualenv venv -p python3
```
```Shell
virtualenv venv -p python2
```

```Shell
source venv/bin/activate
```
### Deactivate:
```Shell
deactivate
```
## Conda 

### Activate:
```Shell
conda activate
source activate py37
```

For the specific version of the python.
```Shell
conda create -n py37 python=3.7 anaconda
conda activate py37
```
### Deactivate:
```Shell
conda deactivate
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