---
title: 'Multiple Interfaces at the same time for your Ubuntu'
date: 2013-04-07T18:05:00.002+05:30
draft: false
categories: ["🗃️ Tech" , "📚 Guides"]
aliases: [ "/2013/04/multiple-interfaces-at-same-time-for.html" ]
tags : [Unity, kubuntu, Software, Desktop Environments, LXDE, lubuntu, KDE, Guides, Ubuntu, XFCE, Cinnamon, Gnome, interface, xubuntu]
---

[![](https://2.bp.blogspot.com/-51vNLpLWMq8/UWFdADnFz1I/AAAAAAAAAqc/JJL_Puk82G0/s1600/DeskEnv.png)](https://2.bp.blogspot.com/-51vNLpLWMq8/UWFdADnFz1I/AAAAAAAAAqc/JJL_Puk82G0/s1600/DeskEnv.png)

  

You may (or may not) know that Ubuntu has various Desktop Environments which is nothing but the interfaces it shows to you. So long I thought that we can have only one at a time but recently I found that we can all those interfaces installed at the same time. So here am I, showing you how to do it. (Before you begin, make sure you are a geek!)

  

Ubuntu will have Unity(the one at the top left corner of the image) as the desktop interface as default. To install multiple enviroments at the same time, do as follows:

  

### Steps:

1.   Open terminal (using the shortcut Ctrl+Alt+T)
2.  Type the following command(s) depending on which environment you want to install. You can also copy and paste the command but to paste it in the terminal, the shortcut is Shift+Ctrl+V not Ctrl+V

  

*   To install KDE(the one at the bottom right corner of the image)-sudo apt-get install --no-install-recommends kubuntu-desktop

  

*   To install LXDE(the one at the bottom left corner of the image)-sudo apt-get install --no-install-recommends lubuntu-desktop

  
  

*   To install Gnome 3 environment(the one at the top right corner of the image)-sudo apt-get install --no-install-recommends gnome-core\[Note: This will also install the gnome classic environment\]

  

*   To install XFCE(the one at the top middle of the image)-sudo apt-get install --no-install-recommends xubuntu-desktop

  

*   To install the Linux Mint's Cinnamon interface(its not there in the image but you can check this one [here](https://www.linuxmint.com/screenshots.php))-

sudo add-apt-repository ppa:gwendal-lebihan-dev/cinnamon-stable    
sudo apt-get update    
```
sudo apt-get install cinnamon
```  
  
  

**Note:**The command \--no-install-recommends is the one that says the OS not to replace the present desktop environment of Ubuntu. If you want to replace the present environment, just remove that part of the command.

  

### Warning:

Though the OS allows you to install as many Desktop environments as you want, it is recommended to not to install more than two interfaces as it may lead to conflicts. 

  

### Uninstalling:

If you think you had enough of any desktop environment, you can uninstall them using the following command

*   KDE- sudo apt-get purge kubuntu-desktop

*   LXDE- sudo apt-get purge lubuntu-desktop

*   Gnome- sudo apt-get purge gnome-core

*   XFCE- sudo apt-get purge xubuntu-desktop

*   Cinnamon-sudo apt-get purge cinnamon

  

and remember not to use the command to remove an environment while you are using that environment. You can switch between these interfaces in the login screen.