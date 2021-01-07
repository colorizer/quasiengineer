---
title: 'How to install Ubuntu in Chromebook and unlock its full potential'
date: 2013-05-22T23:25:00.001+05:30
draft: false
categories: ["🗃️ Tech" , "🪧 Guides"]
aliases: [ "/2013/05/how-to-install-ubuntu-in-chromebook-and.html" ]
tags : [How To's, pixel, Ubuntu, kubuntu, chromebook, dual boot, crouton, lubuntu, chrubuntu, xubuntu]
---

There are some Chromebooks with awesome hardware out there, like [the beautiful Chromebook Pixel](https://gizmodo.com/5986747/google-chromebook-pixel-awesome-just-not-1300-worth-of-awesome), but they don't quite hit their full potential with Chrome OS. Here's how to install Ubuntu and get more out of your Chromebook.  

  

[![](https://3.bp.blogspot.com/-7zi1u1YdR-k/UZ0F6hh496I/AAAAAAAABfs/zwho66Ztt8E/s640/ubuntu+chromebook+linux.jpg)](https://3.bp.blogspot.com/-7zi1u1YdR-k/UZ0F6hh496I/AAAAAAAABfs/zwho66Ztt8E/s1600/ubuntu+chromebook+linux.jpg)

  

Chrome OS isn't bad, and you can actually do a lot of work with the great Chrome apps out there. But sometimes, you just need a full desktop to get things done. Enter Ubuntu: with just a few minutes of work, you can get a full-fledged Linux desktop up and running on some solid Chromebook hardware, making for a pretty great laptop.  

  

We're going to use a tool called [Crouton](httpss://github.com/dnschneid/crouton) to install Ubuntu, which uses the chroot command to run Ubuntu on top of Chrome OS, which is already based on Linux. Unlike dual-booting, that means you can switch between Chrome OS and Ubuntu with a quick keyboard shortcut, no reboots necessary, which is awesome. It's speedy, powerful, and there only when you need it. If you prefer a more traditional dual-boot environment, check out [ChrUbuntu](https://chromeos-cr48.blogspot.fr/) instead. Chrubuntu needs you to reboot to switch the OS but it might have a better performance in case of older machines.  

  

#### Step One: Enable Developer Mode

This will wipe your local data, so make sure to back anything up that you don't have stored in the cloud. To put your Chromebook in Developer Mode:  

  

1.  Press and hold the Esc and Refresh keys together, then press the Power button (while still holding the other two keys). This will reboot your Chromebook into Recovery Mode.
2.  As soon as you see Recovery Mode pop up—the screen with the yellow exclamation point—press Ctrl+D. This will bring up a prompt asking if you want to turn on Developer Mode.
3.  Press Enter to continue, then give it some time. It'll pop up with a new screen for a few moments, then reboot and go through the process of enabling Developer Mode. This may take a little while (about 15 minutes or so), and will wipe your local information.
4.  When it's done, it will return to the screen with the red exclamation point. Leave it alone until it reboots into Chrome OS.

  

![](https://img.gawkerassets.com/img/18od6wnzwo855jpg/ku-xlarge.jpg)  
  
Note that some older Chromebooks have a physical switch that you'll have to flip in order to turn on Developer Mode. If you aren't sure, look up instructions for your specific device on enabling Developer Mode.

  

#### Step Two: Install Crouton

  
Next, we're going to install Crouton and get Ubuntu up and running. To do so, follow these instructions:  
Download Crouton from the top of [this page](httpss://github.com/dnschneid/crouton) (or by [clicking here](https://goo.gl/fd3zc)) and save it in your Downloads folder.  
Press Ctrl+Alt+T to bring up a terminal on your Chromebook.  
At the Terminal, run the following command to enter a Ubuntu shell:

 _shell_

Next, run the following command to install Crouton: 

_sudo sh -e ~/Downloads/crouton -t xfce_

If you're doing this on a Chromebook Pixel, change it to:

 _sudo sh -e ~/Downloads/crouton -t touch,xfce_

to get touch screen support. 

  

**Optional:** You can also encrypt your new desktop with a password for extra security using the -e flag (since Developer Mode inherently decreases the security of your machine). You can [read more about that here](httpss://github.com/dnschneid/crouton/blob/master/README.md).

  

![](https://img.gawkerassets.com/img/18od7bereiqoljpg/ku-xlarge.jpg)

  

  
Let your computer install Crouton. This might be a good time to grab a cup of tea. When it's done it'll ask you for a username and password for your new Ubuntu installation, so enter them when prompted.  
After it's finished installing, run the following command to start your new desktop environment:

_ sudo startxfce4_  
If you want Ubuntu's Unity interface instead of the XFCE desktop environment, you'd change instances of "xfce" to "unity" (no quotes) in the above commands, including the last command (which would become "startunity"). You can also install LXDE or KDE if you prefer. See the Crouton GitHub page for more info on what you can do, and our guide to desktop environments for the difference between each one.

#### Step Three: Optimize Your Linux Desktop for Your Chromebook:

Now, you can switch back and forth between Chrome OS and Ubuntu usingCtrl+Alt+Shift+Back and Ctrl+Alt+Shift+Forward (if you're on an ARM-based Chromebook) or Ctrl+Alt+Back and Ctrl+Alt+Forward (If you're on an Intel-based Chromebook). In the latter case, you will also need to press Ctrl+Alt+Refresh after pressing Ctrl+Alt+Forward to bring up the desktop. To exit the Linux desktop, just log out of it like you would on a normal PC—you'll close it completely and go back to Chrome OS (after which you can run sudo startxfce4 again to go back).  
  
![](https://img.gawkerassets.com/img/18od7dtknfi1zjpg/ku-xlarge.jpg)  
  
Now that you're on the Desktop, here are some things you may want to know to optimize your experience:  
  
Your desktop won't come with very many programs installed. You'll find that even a lot of default Ubuntu tools are left out, so you'll have to install them yourself using apt-get. If you're on an ARM-based Chromebook, not all apps will be compatible. Intel users will be much better off.  
  
If you're using XFCE, you should disable the screensaver, which can cause graphics issues in Chrome OS.  
The Downloads folder in Chrome OS is the same as the Downloads folder on the Linux desktop, so if you download or create a file in one environment, you can put it in the Downloads folder to make it available in the other as well.  
  
If you're on a high resolution display like the Chromebook Pixel, your icons will be very, very tiny. [The Crouton wiki has a few options](httpss://github.com/dnschneid/crouton/wiki/Chromebook-Pixel) for fixing this, though none are quite perfect. You either deal with a few tinier buttons or you go to a more standard resolution.  
  
Since your Chromebook is in Developer Mode, it will take an extra 30 seconds to boot up, since it shows you the Developer Mode message. You can skip this by pressing Ctrl+D.  
  
Lastly, if you want to remove your Linux desktop and go back to regular ol' Chrome OS, you can just reboot your Chromebook and press spacebar when it prompts you to re-enable OS verification. This will remove Crouton and restore Chrome OS in its original state.  
  
That's it! Now you have a fully working Linux desktop on top of Chrome OS, and you can switch between them whenever you want with a quick keystroke. This makes those great but seemingly dumbed-down Chromebooks a lot more useful.  
  

| via [Lifehacker](https://lifehacker.com/how-to-install-linux-on-a-chromebook-and-unlock-its-ful-509039343)