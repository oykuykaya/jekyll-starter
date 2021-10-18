---
layout: default
comments: True
categories: jekyll update
title: Enable SSH Password Authentication
date: "2021-05-15 18:15:00"
description: "Password authentication to Linux server"
---

Bastion host itself has built-in integration with AWS SSM. So that, SSM Agent has been already configured by launching the project. All you need to do is setting password authentication to the host.

Be sure that you set the AWS profile correctly. Please go ahead and connect bastion host.
```bash
export AWS_PROFILE=profile-name
aws ssm start-session --target instance-id
```
```bash
sudo -i 
vim /etc/ssh/sshd_config
```
Change following attribute to `yes`

```bash
PasswordAuthentication yes
```
Then, restart sshd service in Amazon Linux instance

```bash
service sshd restart
```
Then, you can follow-up the session manager article in [here](https://blog.umutykaya.com/ssm-session-manager/) to start port forwarding session to RDS PostgreSQL instance.

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