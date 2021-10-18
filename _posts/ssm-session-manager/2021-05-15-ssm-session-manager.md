---
layout: default
comments: True
categories: jekyll update
title: "SSM Session Manager"
date: 2021-05-15
description: SSM Session Manager with port forwarding option.
---

AWS Systems Manager Agent (SSM Agent) is Amazon software that can be installed and configured on an EC2 instance, an on- premises server, or a virtual machine (VM). SSM Agent makes it possible for Systems Manager to update, manage, and configure these resources.
In some cases we should have an access to servers securely. Enterprise companies have strict compliance rules.
İmagine that you are managing database, DWH cluster. Lets assume that you have an RDS instance with postgres installation. You need to connect database in a secure manner.
Its private ip is 10.159.60.60 and port is 5439. Using SSM by changing host name as localhost and port as 15439 will fix the pain point. Lets dive into topic !

### Prerequisite

1. SSM Agent must be installed on EC2 instance. 2. AWS CLI must be installed.
3. IAM credentials should be located.
4. Session Manager Plugin must be installed.
Configuration
You need to specify a config file in the .ssh hidden directory. The statement will allow you to use ssh command instead of aws ssm.
```bash
# Use IDE e.g. vi,nano emacs that you feel confident
# If you don't have a config file, please create one.
vim ~/.ssh/config
```
### SSH Config File
```bash
# SSH over Session Manager
host i-* mi-*
    ProxyCommand sh -c "aws ssm start-session --target %h --document-name AWS-StartSSHSession --parameters
'portNumber=%p'"
# example.com is a placeholder, can be mutable
# instance-id is unique for each instance
# username can be ec2-user
# keyfile can be example.pem
Host example.com
    ProxyCommand sh -c "aws ssm start-session --target %h --document-name AWS-StartSSHSession --parameters
'portNumber=%p'"
        HostName instance-id
    User username
    IdentityFile /path/to/keyfile
```

### Start a Session
```bash
# SSH Client
ssh -i ~/path/to/keyfile username@instance-id
# AWS SSM Client
aws ssm start-session --target instance-id
```
### Port Forwarding

You need to jump a server to forward connection to your local pc. Thats why, we are connecting to jumpbox server with using usernam
e@instance-id.
The part with -L says that private-ip (e.g 10.159.60.60), remote-port (e.g 8080) forwards to my local-port with (e.g 18080)

Start a Port Forwarding Session
```bash
# SSH Client
ssh -L local-port:private-ip:remote-port -i /path/to/keyfile username@instance-id
# AWS SSM Client
aws ssm start-session --target $instance_id\ --document-name AWS-StartPortForwardingSession \ --parameters
'{"portNumber":["remote-port"],"localPortNumber":["local-port"]}'
```
As a result, you are able connect private (internal) application by passing all the steps.
## References
- SSM Agent: https://docs.aws.amazon.com/systems-manager/latest/userguide/ssm-agent.html
- Session Manager plugin: https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager-working-with- install-plugin.html
- Session Manager port forwarding blog post: https://aws.amazon.com/blogs/aws/new-port-forwarding-using-aws-system- manager-sessions-manager/
- Reinvent 2019 workshop: https://reinvent2019.aws-management.tools/mgt406/en/scenario.html

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