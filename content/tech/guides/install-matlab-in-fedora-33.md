---
title: "Install Matlab in Fedora 33"
subtitle: "![Matlab Loading Screen](/images/2021/install-matlab-in-fedora-33/Screenshot_20210117_191232.png)"
date: 2021-01-17T19:02:28+05:30
draft: false
tags: [Guides, Matlab, Linux, Fedora]
categories: ["🗃️ Tech" , "📚 Guides"]
typora-root-url: ../../../static
---

While Matlab installed just fine for me in Ubuntu, it greeted me with errors in Fedora. Here's how I got it working[^1]. Hope this helps someone.

**Step 1:**

Download matlab from [source] and extract the matlab zip file keeping its original permissions (otherwise, won't work)

```bash
unzip -K matlab_R2020b_glnxa64.zip -d matlab
```

**Step 2:**

cd into matlab folder and run

```bash
cd matlab
sudo ./install
```

If it runs, well you are lucky. If there is error, proceed to step 3.

**Step 3 \[Optional - Read Step 4\]**

Using legacy installer causes matlab to write the downloads to ram instead of actual /tmp. Hence we need to create a directory and make it as tmp temporarily. Create a directory in home folder and make it as tmp.

```bash
mkdir "$HOME/matlabdl"
mount --bind -o nonempty "$HOME/matlabdl" /tmp
```

**Step 4:**

In the matlab folder, run

```bash
sudo ./bin/glnxa64/install_unix_legacy 
```

Login and proceed. If there's an error saying not enough space, quit and start from Step 3. Then proceed and complete the installation.

**Step 5:**

Unmount the tmp we had created.

```bash
umount /tmp
```

If there is an error, there might be some other applications making use of this tmp (for me it was firefox). Check using `lsof`, close those applications and try again.

**Step 6:**

To enable installation of updates/modules in the future, make the current user the owner of the installed directory.

```bash
sudo chown -R $LOGNAME: /usr/local/MATLAB
```

**Step 7:**

Now create a desktop entry for the application with the following in the command box.

```bash
matlab -desktop -nosoftwareopengl
```

Incase you are using nvidia with PRIME profile,

```bash
__NV_PRIME_RENDER_OFFLOAD=1 __GLX_VENDOR_LIBRARY_NAME=nvidia matlab -desktop -nosoftwareopengl
```

**Step 8:**

If you want that retro-look, skip. Otherwise enable anti-aliasing through Preferences > Fonts > Anti-aliasing. Now restart Matlab.

![Matlab in Fedora](/images/2021/install-matlab-in-fedora-33/Screenshot_20210117_195554.png "Matlab in Fedora 33")

It should be working fine now, I hope!

---

[source]: https://in.mathworks.com/downloads/web_downloads/	"Matlab India site"

[^1]: This is a repost of what I had previously shared in Reddit.
