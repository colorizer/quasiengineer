---
title: 'Three simple ways to find MAC address in Ubuntu 16.04.'
date: 2016-07-27T23:16:00.000+05:30
draft: false
aliases: [ "/2016/07/three-simple-ways-to-find-mac-address.html" ]
tags : [How To's, Ubuntu, Ubuntu 16.04, mac address, network]
---

#### Thanks man
[Unknown](https://www.blogger.com/profile/12475314874683682769 "noreply@blogger.com") - <time datetime="2019-05-20T22:16:50.070+05:30">May 1, 2019</time>

Thanks man
<hr />
#### Good Day Everyone, for those of you getting no res...
[Unknown](https://www.blogger.com/profile/10030354070552666501 "noreply@blogger.com") - <time datetime="2019-07-16T20:41:55.754+05:30">Jul 2, 2019</time>

Good Day Everyone, for those of you getting no result with this  
  
ifconfig | grep HWaddr  
  
you can try this instead  
  
ifconfig | grep ether
<hr />
#### The command \`ifconfig\` has been deprecated for yea...
[Kwetal](https://www.blogger.com/profile/02674120034333017876 "noreply@blogger.com") - <time datetime="2019-10-11T20:03:41.869+05:30">Oct 5, 2019</time>

The command \`ifconfig\` has been deprecated for years now. Use \`ip link\` instead.
<hr />
