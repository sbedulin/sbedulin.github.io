---
layout: post
title:  "Set up GoDaddy custom domain for Github Pages"
category: blog
tags: godaddy, custom domain, github pages
date:   2018-08-26
---
At some point I decided to transfer my domain from [ASPHostPortal][asphostportal] to [GoDaddy][godaddy]. After unlocking the domain, it took just a couple of minutes to initiate the move and about a week until the transfer was complete. I learned about the fact of completion when the site stopped working :)
gti
In case new site is being set up, a CNAME file with your custom domain name needs to be added to the repository before configuring DNS in GoDaddy.

![image](/img/posts/2018-08-26-set-up-godaddy-custom-domain-with-github-pages/CNAME.png)

GitHub then asks to add a couple of A records and a CNAME.

![image](/img/posts/2018-08-26-set-up-godaddy-custom-domain-with-github-pages/dns-mgmt.png)

Curent IPs can be copied from ["Setting up an apex domain"][set-up-apex-ips] or here are the ones I used:

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

It might take some time until chages propagate, for instance GitHub articles note that "Your DNS changes can take over a full day to update and the wait varies among DNS providers.". In my case everything started working after about five minutes.

In addition, there was no reason not to enable HTTPS, simple checkbox toggle did the trick (located in your GitHub site repository settings).

![image](/img/posts/2018-08-26-set-up-godaddy-custom-domain-with-github-pages/https.png)

That's it!

Here is GitHub article I used - ["Quick start: Setting up a custom domain"][set-up-custom-domain]. It references related topics if you need dive deeply.

[asphostportal]: https://www.asphostportal.com/
[godaddy]: https://www.godaddy.com/
[set-up-apex-ips]: https://help.github.com/articles/setting-up-an-apex-domain/#configuring-a-records-with-your-dns-provider
[set-up-custom-domain]: [https://help.github.com/articles/quick-start-setting-up-a-custom-domain]