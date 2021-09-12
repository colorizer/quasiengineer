---
title: "Fix White Flash in Dark Mode in Firefox"
date: 2021-09-12T19:39:23+05:30
draft: false
tags: [Guides, firefox]
categories: ["🗃️ Tech" , "📚 Guides"]
typora-root-url: ../../../static
---

I use the dark mode plugin for firefox so that there's less eye strain at night times. But, since the new UI change of firefox, there's flash of white light before the dark mode kicks in, even when the firefox theme is set to dark. I was looking for a solution and found the following in reddit. 

### Solution 1:

One fix is to go to "`about:config`" in firefox and set **`browser.display.background_color`** to a darker colour, say `#2E2E31`. If this doesn't solve the issue, try the following.

### Solution 2:

For the following solution to work, you may have to turn on **User Stylesheets**.

1. Go to `about:config` page in firefox.
2. Click "Accept the Risk and Continue"
3. Search for: _toolkit.legacyUserProfileCustomizations.stylesheets_
4. Set the corresponding value to **true**

Now, you may need to create a chrome folder and two files. 

![Path for userChrome firefox](/images/2021/fix-white-flash-in-dark-mode-in-firefox/Screenshot_20210912_194656.png)

The default path for these user files will be `/home/username/.mozilla/firefox/xxxx.default-release/chrome`. But, ofcourse, it will be different in case you are using windows. 

For a general case, you can open the `about:profiles` page in firefox and open the **root directory** of the profile in use. In there, open the chrome folder (create one if it doesn't exist).

![about profiles in firefox](/images/2021/fix-white-flash-in-dark-mode-in-firefox/Screenshot_20210912_195145.png)

There, you need to create two files. The first comment in each code specify the filename.

```css
/* userChrome.css */
/* Prevents White pre-load flash */
.browserContainer { background-color: #333 !important; }
.tabbrowser tabpanels { background-color: #333 !important; }
```

```css
/* userContent.css */
@-moz-document url("about:newtab"),url("about:blank"), url("about:home") {  
    body {
        background-color: #333333 !important;
    }
}
```

Once you restart the firefox, the white flash will be gone for good!
