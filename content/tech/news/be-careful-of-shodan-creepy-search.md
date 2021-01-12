---
title: 'Be Careful of Shodan - The Creepy Search Engine'
date: 2013-04-12T16:46:00.001+05:30
draft: false
categories: ["🗃️ Tech", "📺 News"]
aliases: [ "/2013/04/be-careful-of-shodan-creepy-search.html" ]
tags : [Security, Software, Google]
---

![](https://1.bp.blogspot.com/-GxOewWUHMC0/UWfs0D2C5zI/AAAAAAAAA2g/N8ZY79P8ohM/s640/Shodan+Banner.JPG)

  

If you don’t want your webcams, printers or home security systems to be hacked, be watchful. Recently, the internet has revealed the scariest search engine called Shodan that peeps into the dark corners of the web, finding servers, webcams and more devices connected to the internet. This search engine for hackers collects information on over 500 million devices every month.

![](https://1.bp.blogspot.com/-1Lkp0izpUcY/UWfs74IZ8YI/AAAAAAAAA2o/yDFNXAh2t-8/s1600/shodan.jpg)

  

Shodan, which stands for Sentient Hyper-Optimized Data Access Network, is the "Google for hackers." It is essentially a search engine for servers, routers, load balances and computers. Shodan's database contains devices identified by scanning the Internet for the ports typically associated with HTTP, FTP, SSH  and Telnet. Hackers are using the Shodan computer search engine to find Internet-facing SCADA systems using potentially insecure mechanisms for authentication, according to warning from [ICS-CERT](https://www.us-cert.gov/control_systems/pdf/ICS-Alert-10-301-01.pdf)(PDF).

  

Now that Shodan would bring more potential threat to connected technology, security professionals have begun to seek out vulnerable devices on the search engine and the response group recommends the following:

*   Place all control systems assets behind firewalls, separated from the business network
*   Deploy secure remote access methods such Virtual Private Networks (VPNs) for remote access
*   Remove, disable, or rename any default system accounts ( where possible)
*   Implement account lockout policies to reduce the risk from brute forcing attempts
*   Implement the policies requiring the use of strong passwords
*   Minotor the creation of administrator level accounts by third-party vendors