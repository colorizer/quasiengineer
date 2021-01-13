---
title: "Install Signal on Fedora 33"
subtitle: "![signal-fedora](/images/2021/signal-on-fedora/signal-fedora.png)"
date: 2021-01-13T23:20:30+05:30
draft: false
tags: [Linux, Signal, Messenger, Fedora]
categories: ["🗃️ Tech" , "📚 Guides"]
typora-root-url: ../../../static
---

With the ongoing privacy issues being raised due to Whatsapp's new policy updates, many people are trying to switch over to Signal. It is a secure encrypted messenger that has been endorsed by many people including Elon Musk. Hence, I was also one of the new flocks in Signal and soon discovered that it is not officially available for Fedora.

But, we have a copr repo built by [Luminoso] that has unofficial builds from the stable source releases. It currently supports Fedora 32, 33 and Rawhide along with CentOS 8 and OpenSuse Tumbleweed. You can install from that repo using the following codes

```bash
sudo dnf copr enable luminoso/Signal-Desktop
sudo dnf install signal-desktop
```

If you are worried about the security of this source[^1], you can verify the [spec  file]. The rpm files will be available at [copr git dist]. Let me know if there is any issue. I'll try to help.


---
[^1]: [Signal-desktop Copr](https://copr.fedorainfracloud.org/coprs/luminoso/Signal-Desktop/)

[spec file]: https://github.com/luminoso/fedora-copr-signal-desktop	"Signal Copr spec file"
[copr git dist]: http://copr-dist-git.fedorainfracloud.org/cgit/luminoso/Signal-Desktop/signal-desktop.git/	"Versioned RPM files for Signal"
[Luminoso]: https://copr.fedorainfracloud.org/coprs/luminoso/	"Author"

