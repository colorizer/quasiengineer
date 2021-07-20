---
title: "Converting Video to Matroska Format using ffmpeg"
date: 2021-07-20T15:16:16+05:30
draft: false
tags: [Guides, ffmpeg]
categories: ["🗃️ Tech" , "📚 Guides"]
typora-root-url: ../../../static
---

My primary use case of `ffmpeg` had been to reduce the size of the downloaded online lectures. The output format did not actually matter for those videos as it seemed that the humongous file size of Powerpoint screen recording seems to be due to absence of proper [encoding](https://www.salientsys.com/files/whitepaper/Understanding%20H%20264.pdf) (not sure though). The matroska or "mkv" is an Open Source container format for video files. It has many advantages about which you can read about in their [FAQ page](https://matroska.org/faq.html). Here is how you can convert a batch of videos in a particular format (mp4, in my case) to mkv using ffmpeg.

**Note**: This is a simple code for video conversion. But, if you intend to perform complex use cases, check out [handbrake](https://handbrake.fr/), a free and open source video transcoding software.

## Linux

First, check whether you have the ffmpeg module installed and if not, get it installed. For Ubuntu, the following command can be used for installation. 

```bash
sudo apt install ffmpeg
```

Now, open the folder (`cd`) containing the videos inside the terminal. Then, the following bash command will be sufficient to convert all the videos in the current folder to mkv format while .

```bash
for file in *.mp4; do
	ffmpeg -i "$file" "${file%.*}.mkv"
done
```

 However, if you do not want the file to be re-encoded, that is, the file size is already small enough and you just want to change file type, use the following code instead. This will save time and quality.

```bash
for file in *.mp4; do
	ffmpeg -i "$file" -codec copy "${file%.*}.mkv"
done
```

## Windows

In windows, you can install ffmpeg from their [website](https://ffmpeg.org/download.html). But, if you have [Chocolatey](https://chocolatey.org/) installed, the following command in the powershell (as Administrator) can be used for installing ffmpeg.

```powershell
choco install ffmpeg
```

Then, open the folder containing videos in powershell. This can be done through navigating to the folder in File Explorer and then right click --> *Open in [Windows Terminal](https://www.microsoft.com/en-in/p/windows-terminal/9n0dx20hk701)*.  In that powershell session,  paste the following command 

```powershell
foreach ($file in (Get-Item .\*.mp4))
{
ffmpeg -i $file.FullName $file.Name.replace(".mp4",".mkv");
}
```

Similar to Linux, you can use the `-codec copy` parameter here to convert without re-encoding. 

