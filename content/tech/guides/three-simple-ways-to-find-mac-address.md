---
title: 'Three simple ways to find MAC address in Ubuntu 16.04.'
date: 2016-07-27T23:16:00.000+05:30
draft: false
categories: ["🗃️ Tech" , "🪧 Guides"]
aliases: [ "/2016/07/three-simple-ways-to-find-mac-address.html" ]
tags : [How To's, Ubuntu, Ubuntu 16.04, mac address, network]
---

You may need the MAC address for various functions at some point in your life. So, it will always be helpful to know how to find out mac address in Ubuntu.  
  

#### 1) Using Networks Manager:

[![](httpss://3.bp.blogspot.com/-nGoSINT4gaE/V5jyVDPg5MI/AAAAAAAAGLA/68VDU2eUOGc0i2xGeSZ8gxQUQ0H1cEVowCK4B/s320/nm.jpg)](https://3.bp.blogspot.com/-nGoSINT4gaE/V5jyVDPg5MI/AAAAAAAAGLA/68VDU2eUOGc0i2xGeSZ8gxQUQ0H1cEVowCK4B/s1600/nm.jpg)

  

*   Go to _System Settings_.
*   Select _Network_.
*   Click on the arrow next to your current connection (Wired or Wifi connected to).
*   Then mac address will be available under the name _Hardware address_.

#### 2) Using command line

Using command line, it is rather simple.  
  

*   Open _Terminal_ ( Ctrl+Alt+T)
*   Copy the following code:  **ifconfig | grep HWaddr**
*   And, paste in the terminal ( Ctrl+Shift+V ).

You may probably get two mac address (as I got). Don't worry. They might be the mac addresses for the LAN and WiFi respectively.

  

[![](httpss://3.bp.blogspot.com/-Vq1dDtlO-Io/V5juhp3uULI/AAAAAAAAGKA/KP4jDKOiA4Eh40Pr1-X0p5Nf6HnTK1LxwCK4B/s320/terminal.jpg)](https://3.bp.blogspot.com/-Vq1dDtlO-Io/V5juhp3uULI/AAAAAAAAGKA/KP4jDKOiA4Eh40Pr1-X0p5Nf6HnTK1LxwCK4B/s1600/terminal.jpg)

  

  

#### 2) Using Connection Information:

You can use the connection information for gaining the mac addresses.

  

*   Click on the _Network indicator_ in the Unity panel.
*   Select _connection information_ from the submenu.

[![](httpss://3.bp.blogspot.com/-8vO12QbfGQM/V5jwXBasi3I/AAAAAAAAGKY/MK4oscYpSf828QrbSJbm9PoyxT9pGCnfACK4B/s320/connection.jpg)](https://3.bp.blogspot.com/-8vO12QbfGQM/V5jwXBasi3I/AAAAAAAAGKY/MK4oscYpSf828QrbSJbm9PoyxT9pGCnfACK4B/s1600/connection.jpg)

*   The Hardware address provides you with your current connection's (LAN or Wifi) mac address.

[![](httpss://2.bp.blogspot.com/-hkTYwE8t1u4/V5jxA1WMI4I/AAAAAAAAGKs/5-5MOWHyRzUxJY-gccAku8p8PTeWFMZHgCK4B/s320/hadinfo.jpg)](https://2.bp.blogspot.com/-hkTYwE8t1u4/V5jxA1WMI4I/AAAAAAAAGKs/5-5MOWHyRzUxJY-gccAku8p8PTeWFMZHgCK4B/s1600/hadinfo.jpg)

  

Hope this helped you. If something didn't work out, please let me know!