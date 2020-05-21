---
layout : post
title : "Download videos from linux academy"
date : 2020-05-05 07:45:36
author : Sasidhar
categories : linux_academy_videos
tags : videos linux academy download
---

Every month, Linux Academy releases courses for free. I'm a very busy college student and don't have time to whirl through everything I want to before it goes behind their paywall again so I figured out how to download a course or two every month using [`youtube-dl`](https://github.com/ytdl-org/youtube-dl/).

>READ TIME : 3 MINUTES

# Setup
* Install [`youtube-dl`](https://ytdl-org.github.io/youtube-dl/download.html)
* Make sure you have a browser handy
* Create a community account on [Linux Academy](https://linuxacademy.com/join/community)
* Get some food
* Maybe a drink
* Sit back down in your chair
* Spin around a bit
* Read on

# Downloading
* Log into your account
* Pick the course you want
* Open the developer console and go to `Network` (Ctrl+Shift+E in Firefox)
* You'll want to select `Media` as shown in the screenshot below

![](/assets/posts/linux-academy/scrot-1.png)

* Click the video you want to start with
* Watch the network logs
* You'll see an entry that starts with `playlist` (screenshot below)

![](/assets/posts/linux-academy/scrot-2.png)

* Right click it
* Copy the URL
* Paste it after `youtube-dl` in a terminal:

```sh
sasidhar@sasidhar:~ $ youtube-dl https://video-cdn.linuxacademy.com/vods3/_definst_/smil:box/cdnstore/modules/lots-of-stuff-in-here
```

* Press enter
* Watch the magic unfold

At a high level, `youtube-dl` is acting like your browser and following the `m3u` playlist to download chunks of the file. After it fetches them all, it runs them through `ffmpeg` to stitch them together into a single video!

I found it useful to open a text editor and script downloading a whole course at a time. All you have to do is type `youtube-dl -o` and copy/paste it however many times there are videos. Then, copy and paste the video title in quotes after `-o` and add `.mp4` to the end (command example below). After that, paste the URL. Do that with every video in the series, save the script, run `chmod +x <script>`, then `./<script>` and (after a bit) you'll have an entire course you can watch at your leasure!

```bash
sasidhar@sasidhar:~ $ youtube-dl -o "04 - Conclusion and Next Steps.mp4" https://video-cdn.linuxacademy.com/vods3/_definst_/smil:box/cdnstore/modules/lots-of-stuff-here
```

**NOTE:** You may want to set up your directory structure beforehand so it's easier to script the process. Here's an example of one of mine:

```bash
sasidhar@sasidhar:~/Videos/Courses/Ansible - Playbooks Deep Dive $ tree
.
├── 01 - Course Overview
│   ├── 01 - About the Course.mp4
│   ├── 02 - About the Training Architect.mp4
│   ├── 03 - Course Features and Tools.mp4
│   ├── 04 - About Ansible Playbooks.mp4
│   └── 05 - Advanced Inventory Configuration.mp4
├── 02 - Playbook Basics
│   ├── 01 - Using YAML for Ansible Playbooks.mp4
│   ├── 02 - Creating an Ansible Play.mp4
│   ├── 03 - The ansible-playbook Command.mp4
│   └── 04 - Understanding Playbook Tasks.mp4
├── 03 - Essential Playbook Syntax
│   ├── 01 - Using Variables in Playbooks.mp4
│   ├── 02 - Working with Templates.mp4
│   ├── 03 - Using Ansible Facts.mp4
│   ├── 04 - Conditional Execution in Playbooks.mp4
│   ├── 05 - Using Loops in Ansible.mp4
│   └── 06 - Working with Handlers in Ansible.mp4
├── 04 - Advanced Playbook Syntax
│   ├── 01 - Executing Selective Parts of a Playbook.mp4
│   ├── 02 - Working with Sensitive Data Using Ansible Vault.mp4
│   ├── 03 - Error Handling in a Playbook: limit, ignore_errors, changed_when, and failed_when.mp4
│   ├── 04 - Error Handling in a Playbook: Block Groups and The Debug Module.mp4
│   ├── 05 - Asynchronous Tasks within a Playbook.mp4
│   ├── 06 - Delegating Playbook Execution with delegate_to and local_action.mp4
│   ├── 07 - Parallelism in Playbooks.mp4
│   ├── 08 - Using run_once.mp4
│   ├── 09 - Overview of Ansible Roles.mp4
│   └── 10 - Ansible Role Demo.mp4
└── 05 - Conclusion and Next Steps.mp4

4 directories, 26 files
sasidhar@sasidhar:~/Videos/Courses/Ansible - Playbooks Deep Dive $
```
