---
title: 'How to install Ubuntu in Chromebook and unlock its full potential'
date: 2013-05-22T23:25:00.001+05:30
draft: false
aliases: [ "/2013/05/how-to-install-ubuntu-in-chromebook-and.html" ]
tags : [How To's, pixel, Ubuntu, kubuntu, chromebook, dual boot, crouton, lubuntu, chrubuntu, xubuntu]
---

#### does this work on a samsung chromebook(ARM process...
[ariel]( "noreply@blogger.com") - <time datetime="2013-05-25T18:30:18.600+05:30">May 6, 2013</time>

does this work on a samsung chromebook(ARM processor) as well?
<hr />
#### Yes, this will work on all chromebooks. But, you w...
[Jebin](https://www.blogger.com/profile/10059007117931210486 "noreply@blogger.com") - <time datetime="2013-05-25T21:34:29.360+05:30">May 6, 2013</time>

Yes, this will work on all chromebooks. But, you will find yourself running out of resources quite quickly in case of crouton. So, dual-boot (using chrubuntu) will be a better option for Samsung Chromebook.
<hr />
#### so i turned off my chromebook now and turned it ba...
[Anonymous]( "noreply@blogger.com") - <time datetime="2013-07-29T02:45:49.649+05:30">Jul 1, 2013</time>

so i turned off my chromebook now and turned it back on and its not there what do i do !!!!!!!
<hr />
#### Please make sure that the chromebook is in the dev...
[Jebin](https://www.blogger.com/profile/10059007117931210486 "noreply@blogger.com") - <time datetime="2013-08-10T00:36:02.366+05:30">Aug 6, 2013</time>

Please make sure that the chromebook is in the developer mode.
<hr />
#### Jebin: Thanks for the article! I just got an Ace...
[Unknown](https://www.blogger.com/profile/00180214609214382895 "noreply@blogger.com") - <time datetime="2013-08-26T00:37:23.564+05:30">Aug 1, 2013</time>

Jebin: Thanks for the article! I just got an Acer Chromebook C7 and the apps in the Chrome store kind of suck. I'm a total newbie to Linux. So how would I change the Crouton commands to install Ubuntu 13.04 with XFCE rather than 12.04? Is that a possibility or do I have to install 12.04 and then upgrade?
<hr />
#### Anonymous said, so i turned off my chromebook now ...
[Unknown](https://www.blogger.com/profile/00180214609214382895 "noreply@blogger.com") - <time datetime="2013-08-30T03:52:25.599+05:30">Aug 5, 2013</time>

Anonymous said, so i turned off my chromebook now and turned it back on and its not there what do i do !!!!  
  
As the article states: you can switch back and forth between Chrome OS and Ubuntu using Ctrl+Alt+Shift+Back and Ctrl+Alt+Shift+Forward (if you're on an ARM-based Chromebook) or Ctrl+Alt+Back and Ctrl+Alt+Forward (If you're on an Intel-based Chromebook). In the latter case, you will also need to press Ctrl+Alt+Refresh after pressing Ctrl+Alt+Forward to bring up the desktop.  
  
On my Chromebook keyboard Back is the F1 key and Forward is the F2 key. After you press Ctrl+Alt+F2, you'll see the "localhost login:" prompt. Then type:  
  
chronos (then press the enter key)  
sudo startxfce4 (then press the enter key)  
Then Ubuntu will start up.
<hr />
#### Run sh -e ~/Downloads/crouton -r list to list the ...
[Jebin](https://www.blogger.com/profile/10059007117931210486 "noreply@blogger.com") - <time datetime="2013-11-13T17:34:05.389+05:30">Nov 3, 2013</time>

Run sh -e ~/Downloads/crouton -r list to list the recognized releases and which distros they belong to and then install the needed release. I believe this would solve the problems and I'm really sorry for being this much late
<hr />
#### I think this link can be useful to you https://git...
[Jebin](https://www.blogger.com/profile/10059007117931210486 "noreply@blogger.com") - <time datetime="2013-11-13T17:35:41.670+05:30">Nov 3, 2013</time>

I think this link can be useful to you https://github.com/dnschneid/crouton
<hr />
