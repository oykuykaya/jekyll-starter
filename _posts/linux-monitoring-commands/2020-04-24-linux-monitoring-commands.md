---
layout: default
comments: True
categories: jekyll update
regenerate: true
title: Linux monitoring commands
date: "2020-04-24 16:29:06"
description: "Here is a comprehensive guide that I thing beneficial while monitoring users."
---

Common Linux systems need to be supervision by system admins.
Here is a comprehensive guide that I thing beneficial while monitoring users.

| Description |Command|
|--|--|
| Bash history of all users |``` cat /home/*/.bash_history ```|
| Bash history specified user| ```cat /home/firstname_lastname/.bash_history ```|  
| Memory summary | ``` free -g``` |  
| Detailed memory summary |``` cat /proc/meminfo ```|  
| Find a file | ```sudo find -type f -name pandas``` |  
| To list the processes executed by a specific user | ```ps -U <username>``` |  
| Running process | ```top```, ```htop```|
| Show Active Sessions | ```ps aux| grep "X" ```|

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