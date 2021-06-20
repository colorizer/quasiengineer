---
title: "Automate Daily Task with Bash and Cron"
date: 2021-06-20T15:18:26+05:30
draft: false
tags: [Guides]
categories: ["🗃️ Tech" , "📚 Guides"]
typora-root-url: ../../../static
---

Here is a simple method in which I am automating the creation of "Tomorrow's notes" for my [Obsidian.md](https://obsidian.md/) notes[^1]. In a similar manner, any simple tasks that needs to be repetitively done daily can be done with the help of bash scripting and cron job.

![image-20210620152537689](/2021/automate-daily-task-with-bash-and-cron/image-20210620152537689.png)

The above shows the daily notes I indent to create on a daily basis for the next day. This, I have implemented with the simple steps.

1. Check if tomorrow's file doesn't exist (or if it exists, check if its empty) `[ ! -s filename ]`
2. If the above statement is true, create an empty file of the filename and copy the predefined texts to it.

You may have noticed that my Date Format is a bit different. This can be achieved using the linux's `date` command. This can be written as a bash script as follows:

```bash
#! /bin/bash -e

TODAY=$(date +%d-%m-%y-%A)
YDY=$(date +%d-%m-%y-%A --date=yesterday)
TMW=$(date +%d-%m-%y-%A --date=tomorrow)
DATMW=$(date +%d-%m-%y-%A --date="tomorrow tomorrow")
JNL="Documents/Notes/Journal"

if [ ! -s $HOME/$JNL/$TMW.md ]
then
	touch $HOME/$JNL/$TMW.md
	cat <<- EOF > $HOME/$JNL/$TMW.md
	Date: [[$TMW]]
	Previous: [[$TODAY]]  
	Next: [[$DATMW]]

	## Agenda
	- 
	- 

	## Tasks
	- [ ] 

	## Today's Notes
	Readings:
	EOF
fi
```

The output of the cat command (which is the rest of the text until EOF) is piped to the file using a method called as [Here document redirection](https://linuxize.com/post/bash-heredoc/). This can be extensively helpful in remote SSH sessions as well. After creating, I had saved it with the filename `create-daily.sh`.

The next step is to make it a daily task which gets automatically executed everyday. The problem with **cron** is that it is meant server environment. Hence, if your computer resumes after a shutdown, it won't get executed. The solution is to use **anacron** which Ubuntu happens to use by default. Hence, one can simply copy the above script to a predefined folder as follows

```shell
sudo cp create-daily.sh /etc/cron.daily/
```

Thus, such simple but time consuming jobs can be automated.

---

[^1]: Obsidian supports template for "Today's notes" but it doesn't support tomorrow's notes yet. Hopefully, it may get implemented in a later release.
