---
title: 'Microsoft Documents opens via Ark in KDE Neon (with Solution)'
date: 2017-07-28T19:10:00.000+05:30
draft: false
aliases: [ "/2017/07/microsoft-documents-opens-via-ark-in.html" ]
tags : [How To's, MS Office, Dolphin, Ubuntu, filetype, WPS Office, App, association, KDE, Ark, KDE Neon]
---

[![](httpss://1.bp.blogspot.com/-r6xwzuB4Q54/WXszff4CgDI/AAAAAAAAN0Q/mHZJFisraI0rbc3ggyLdwPAusb2Y-pU9ACK4BGAYYCw/s400/kde_neon_laptop.png)](https://1.bp.blogspot.com/-r6xwzuB4Q54/WXszff4CgDI/AAAAAAAAN0Q/mHZJFisraI0rbc3ggyLdwPAusb2Y-pU9ACK4BGAYYCw/s1600/kde_neon_laptop.png)

  
With Ubuntu moving away from Unity, I was looking for a different desktop experience with a modern outlook. So, I decided to try out KDE Neon, using KDE for the first time in my life. So, when I finally setup WPS Office successfully (Yes, that needs squashing bypassing some bugs too! [Click here for install and setup guide.](https://techbytesinfinite.blogspot.in/2017/07/how-to-install-and-open-wps-office-in.html)), it didn't open files when opened from the default file manager. Instead, I was facing an Ark zip manager. For the first time, I realized that MS Office documents are really archives!  

[![](httpss://3.bp.blogspot.com/-a9_dOtIgTco/WXs336fGM8I/AAAAAAAAN0c/Dcpe5hzLx24QCqtmfgaQbhyWccFqZUu5gCK4BGAYYCw/s640/Screenshot_20170728_184011.png)](https://3.bp.blogspot.com/-a9_dOtIgTco/WXs336fGM8I/AAAAAAAAN0c/Dcpe5hzLx24QCqtmfgaQbhyWccFqZUu5gCK4BGAYYCw/s1600/Screenshot_20170728_184011.png)

  
The usual steps for any other misconfiguration of filetypes is as follows.  

*   Open Dolphin
*   Right click one of those documents and select properties
*   Then click the File Type Options button
*   Then in the Application Preference Order window select the program you want to handle that type, and use Move Up button till that program is at the top.

It was a pretty weird bug because the above steps didn't solve the issue. No matter what you change in file association box in dolphin, that doesn't work. So, instead of going for the obvious workaround (uninstalling WPS), I chose to find some answer. Thanks to the strong community of Manjaro Linux, I was able to find the workaround which is as follows.

[![](httpss://4.bp.blogspot.com/-9HF55q1SRZ0/WXs97mUoGbI/AAAAAAAAN0s/QT23BGtF2RkPzSdSduJMp_-9o-NCrYGkgCK4BGAYYCw/s640/Screenshot_20170728_190600.png)](https://4.bp.blogspot.com/-9HF55q1SRZ0/WXs97mUoGbI/AAAAAAAAN0s/QT23BGtF2RkPzSdSduJMp_-9o-NCrYGkgCK4BGAYYCw/s1600/Screenshot_20170728_190600.png)

  

*   _cd /usr/share/mime/packages/_
*   _sudo rm wps-office-et.xml _
*   _sudo rm wps-office-wpp.xml_
*   _sudo rm wps-office-wps.xml_
*   _sudo update-mime-database /usr/share/mime_
*   Now, follow the usual steps as provided above to set the file types successfully.

  
Source: [Manjaro Linux forum](httpss://forum.manjaro.org/t/xlsx-and-docx-files-are-opened-as-zip-file/25814/4)