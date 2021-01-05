---
title: 'How to recover your Windows password (by hacking into it)'
date: 2013-05-20T11:10:00.002+05:30
draft: false
aliases: [ "/2013/05/how-to-recover-your-windows-password-by.html" ]
tags : [How To's, data recovery, hack, passwords, Windows]
---

  

[![](http://cdn.mos.techradar.com//art/magazines/PC%20Format/Issue%20277/OWV74.ex9_wifi.win7back-470-75.jpg)](http://cdn.mos.techradar.com//art/magazines/PC%20Format/Issue%20277/OWV74.ex9_wifi.win7back-470-75.jpg)

  
  
Ever forgotten your Windows password and locked yourself out of your PC? It's a nightmare, but there are several ways to get back in.  
  
We're going to explore the method a professional hacker would use to get into your PC. It's straightforward and uses your Windows 7 installation disc, which contains all the tools you need to get in and change the password.  
  
The technique we'll use contains a real life hack. We'll replace the Sticky Keys executable with a command prompt, so that even without logging in, we can pull up a command line and change the password, then use it to log in.  
  
If you don't have a Windows installation disc, one option is to load up a password cracker. This is exactly what we'll do using the industry standard Ophcrack. You should only use these techniques to access your own PC. **_Hacking into another person's machine is a criminal offence._**  

### Step-by-step: Recover Windows 7 passwords

#### 1\. Boot installation disc:

To reset your Windows user account password, you must first boot the computer from the Windows 7 installation disc. Switch on your PC, and when you're given the option to boot from DVD, quickly hit any key to boot. After Windows loads its installation files, you'll be shown the language setup page. Select your country to set up the keyboard, then click the 'Next' button.  
  

#### 2\. Repair the computer

  

  

[![](http://mos.futurenet.com/techradar/art/magazines/PC%20Format/Issue%20277/OWV81.explore3.step2-420-90.jpg)](http://mos.futurenet.com/techradar/art/magazines/PC%20Format/Issue%20277/OWV81.explore3.step2-420-90.jpg)

  
  
  
Click 'Repair your computer'. The repair software takes a few moments to load from the installation disc, then begins examining the computer's hard disk boot table, looking for any current Windows 7 installations to repair. Unless you've installed many copies of the operating system by hand, there will be just one installation, so click 'Next' to continue the recovery process.  
  

#### 3\. Find the C drive:

[![](http://mos.futurenet.com/techradar/art/magazines/PC%20Format/Issue%20277/OWV81.explore3.step3-420-90.jpg)](http://mos.futurenet.com/techradar/art/magazines/PC%20Format/Issue%20277/OWV81.explore3.step3-420-90.jpg)

  
  
The resulting screen gives you many options. Click 'Command prompt' and one appears. The C drive is usually not mounted as C at all, so you need to find out its current drive letter. To do this, type  

**bcdedit | find "osdevice"**

into the command line. This command results in text ending in partition= and a drive letter. This is the letter you should use instead of C in the following step.  
  

#### 4\. Prepare the recovery:

  

[![](http://mos.futurenet.com/techradar/art/magazines/PC%20Format/Issue%20277/OWV81.explore3.step4-420-90.jpg)](http://mos.futurenet.com/techradar/art/magazines/PC%20Format/Issue%20277/OWV81.explore3.step4-420-90.jpg)

  
  
Enter the following commands. Take care to ensure that you use the correct driver letter in place of C:  

**copy c:\\windows\\system32\\sethc.exe c:\\**

and

**copy c:\\windows\\system32\\cmd.exe c:\\windows\\system32\\sethc.exe**

When prompted, confirm the second command by typing Yes. The first command backs up a file, and the second replaces it with the command prompt.  
  

####   
5\. Reboot into Windows:

  

[![](http://mos.futurenet.com/techradar/art/magazines/PC%20Format/Issue%20277/OWV81.explore3.step5-420-90.jpg)](http://mos.futurenet.com/techradar/art/magazines/PC%20Format/Issue%20277/OWV81.explore3.step5-420-90.jpg)

  
  
Now remove the installation disc and reboot. On the login screen, press the \[Shift\] key five times in a row. As if by magic, a command prompt appears. Enter the following command:  

**Net user <name> <new password>**

Substitute the name of the account to reset and a new password as appropriate. Close the command prompt and enter the new password to log in.  
  

#### 6\. Copy sethc.exe:

  

[![](http://mos.futurenet.com/techradar/art/magazines/PC%20Format/Issue%20277/OWV81.explore3.step6-420-90.jpg)](http://mos.futurenet.com/techradar/art/magazines/PC%20Format/Issue%20277/OWV81.explore3.step6-420-90.jpg)

  
  
The final step we must take to restore access is to restore the sethc.exe file we overwrote in step 4. To do so, click 'Start > Accessories', right-click 'Command prompt' and select 'Run as Administrator'. This gives you the right to copy sethc.exe back into the system32 folder. Now enter the command  

**Copy c:\\sethc.exe c:\\windows\\system32\\sethc.exe**

Confirm the copy to finish.  
  

#### 7\. Download Ophcrack:

  

[![](http://mos.futurenet.com/techradar/art/magazines/PC%20Format/Issue%20277/OWV81.explore3.step7-420-90.jpg)](http://mos.futurenet.com/techradar/art/magazines/PC%20Format/Issue%20277/OWV81.explore3.step7-420-90.jpg)

  
  
To crack an unknown password, we need to use a heavy duty password cracker like Ophcrack. You'll need to download it from [http://ophcrack.sourceforge.net/download.php](http://ophcrack.sourceforge.net/download.php). To get started, insert a blank, formatted DVD-RW, then right-click the downloaded image and select 'Burn disc image'. The disc being written is a bootable live CD containing both Linux and Ophcrack.  
  

#### 8\. Boot Ophcrack:

  

[![](http://mos.futurenet.com/techradar/art/magazines/PC%20Format/Issue%20277/OWV81.explore3.step8-420-90.jpg)](http://mos.futurenet.com/techradar/art/magazines/PC%20Format/Issue%20277/OWV81.explore3.step8-420-90.jpg)

  
  
Once the DVD has been written, boot the affected computer and the DVD should begin to automatically load the Ophcrack software, which runs outside of Windows. Once the software has loaded, a menu should appear offering several options for running Ophcrack. Either press \[Enter\], or wait for the timeout and automatically select the Ophcrack graphical mode.  

####   
9\. Crack passwords:

  

[![](http://mos.futurenet.com/techradar/art/magazines/PC%20Format/Issue%20277/OWV81.explore3.step9-420-90.jpg)](http://mos.futurenet.com/techradar/art/magazines/PC%20Format/Issue%20277/OWV81.explore3.step9-420-90.jpg)

  
  
Short passwords, such as '1234' or 'password', will fall to Ophcrack almost immediately because the software tries these first in a brute force attack. Complex passwords take more time, and the longer the password the longer it will take to crack - if it can be cracked at all. A complex password may take several hours to crack. Ophcrack doesn't store the passwords, so make a note.  
  

#### 10\. Comprehensive cracking:

  

[![](http://mos.futurenet.com/techradar/art/magazines/PC%20Format/Issue%20277/OWV81.explore3.step10-420-90.jpg)](http://mos.futurenet.com/techradar/art/magazines/PC%20Format/Issue%20277/OWV81.explore3.step10-420-90.jpg)

  
  
Finally, let's perform a deep scan of the whole computer to reveal all passwords associated with Windows user accounts. Close any windows and double click 'Launcher', then scroll down to 'DeepSearch' and press \[Enter\]. Ophcrack will search all available media for any password files - not just the system volume - and then perform its password-cracking wizardry.![](http://rss.feedsportal.com/c/669/f/9809/s/2c1e58d4/mf.gif)  

#### How to be secure:

Now people know how to recover the password but we can't be sure all of them would use it to recover only their password. In this case I will prefer you to use windows 8 which has a secure boot loader, which means, that other devices can't boot into your system unless you allow it. Also, always use the most secure password. These won't make the system unhackable but more secure.