---
title: 'How to Install and Open WPS Office in KDE Neon?'
date: 2017-07-28T19:59:00.000+05:30
draft: false
categories: ["🗃️ Tech" , "🪧 Guides"]
aliases: [ "/2017/07/how-to-install-and-open-wps-office-in.html" ]
tags : [Linux, Dolphin, kubuntu, Software, WPS Office, App, association, KDE, How To's, Ubuntu, filetype, KDE Neon]
typora-root-url: ../../../static/images
---

![](httpss://2.bp.blogspot.com/-d1a9ZW9l4is/WXtJt9iNXAI/AAAAAAAAN1w/oGuQ48Mi1VwFfSO2nxunFA60avsFzOMswCK4BGAYYCw/s1600/Presentation_Slide2.png)


WPS Office is a popular MS Office clone for Linux and they provide better support for MS Office files than Libre Office or any other Office in Linux (as far as I know). But, WPS Office doesn't work well with Neon's KDE environment and fails to launch. So, I will explain the steps to install and setup WPS Office successfully in Neon.  


*   Download the latest WPS Office from [here](https://wps-community.org/downloads).
*   Open the Downloads folder in Dolphin file manager and right click on the Debian package.
*   Select Open With --> QApt Package Installer. It is available in every KDE Neon installation.
*   Select Install and input your Password when requested.
*   Close it once the installation is over.
*   sudo dpkg --configure -a

Now, after installing, you may not be able to launch it when opening a document opening a document or in Applications menu. This is because of incompatibility with KDE. We have to make it fallback to GTK for it to work. Now follow these steps.

[![](httpss://3.bp.blogspot.com/-6z-pxMhd66o/WXtHIQnsrbI/AAAAAAAAN1o/ViKwI85RGAoElkjoCMpLMMLuC9U2MBPHQCK4BGAYYCw/s400/Screenshot_20170728_194554.png)](https://3.bp.blogspot.com/-6z-pxMhd66o/WXtHIQnsrbI/AAAAAAAAN1o/ViKwI85RGAoElkjoCMpLMMLuC9U2MBPHQCK4BGAYYCw/s1600/Screenshot_20170728_194554.png)

*   Right click the Application Launcher and select "Edit Applications".
*   Select Submenu WPS Writer under Office.
*   In the General tab, replace _/usr/bin/wps %f_ with  _/usr/bin/wps %f__  -style gtk_.
*   Similarly, add _\-style gtk_ to the existing commands for WPS Presentation and Spreadsheets.
*   Finally, click Save and close the Menu Editor.

Now, if you open WPS Office from Application Menu, it will launch successfully. **However, if you try to open documents from Dolphin, the Ark archive tool will open. For that problem, follow this work around. **

[Microsoft Documents opens via Ark in KDE Neon (with Solution)](httpss://technologyinfinite.blogspot.com/2017/07/microsoft-documents-opens-via-ark-in.html)
==========================================================================================================================================================