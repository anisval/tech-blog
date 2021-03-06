---
layout: post
title:  "Tracking manager's work with git"
date: 2019-06-10 15:30:00 +0200
categories: culture
author_name: Łukasz Przybył
author_url : /author/luprzybyl
author_avatar: luprzybyl
read_time : 3
feature_image: posts/2019-06-10-tracking-managers-work-with-git/notes.jpg
show_related_posts: false
excerpt: "I have been using `git` for quite some time now. In the days were engineering work consumed most of my workday it was my weapon of choice for code versioning. Fortunately or not, about a year ago I was promoted to a manager position and I had to give away some coding fun for scheduling meetings in my calendar. Although I'm still trying my best not to be dragged away from technical tasks, sometimes I need to face weeks, where I hardly open my IDE or console."
square_related: 
---

## The background

I have been using `git` for quite some time now. In the days, where engineering work consumed most of my workday, it was my weapon of choice for code versioning. Fortunately or not, about a year ago I was promoted to a manager position and I had to give away some coding fun for scheduling meetings in my calendar. Although I'm still trying my best not to be dragged away from technical tasks, sometimes I need to face weeks where I hardly open my IDE or console.

What also changed with my promotion was my perception of a productive day. Back in the good old "backlog" days I could look at the tasks I have closed and tell myself _"that was a good day"_. After the turn in my career path, I could spot less and less days where I could congratulate myself such an achievement. Tasks on the board with my face on them were not moving and I saw a constant decrease in the rate of my commits being pushed to company GitHub. I was busy all day discussing with my reports, making agreements, advising… but none of this was giving me this tangible feeling of a work being done—similar to when you move your task to "done" column.

I knew this was a false feeling. I was doing my job after all. I just needed some assurance of progress I have made—especially after long day filled with meetings. And then I came up with an idea to version my notes.

## The solution

I have been doing notes before, but in tools dedicated for this kind of activity: Evernote, OneNote, bunch of text files. None of them however provided me flexibility to look back and track my progress. Then I thought about the old friend of mine, `git`.

First, I created a neat bash wrapper to make notes in files with timestamps:

```shell
$ cat bin/note 
#!/bin/bash
micro ~/Documents/notes/$(date +"%Y-%m-%d")_$1
```

I have decided to use small console editor [micro](https://micro-editor.github.io/) written in Golang. Inside the file I'm not using any particular style. Sometimes I use markdown, sometimes I don't.

Second, I have written a cronjob that would run once a day, around 4pm and automatically check in my notes to local git repository with timestamp as a commit message:

```shell
commit e41e157afccb06e90679f6a98bfb4faab7e85587 (HEAD -> master)
Author: Łukasz Przybył <lukasz.przybyl@holidaycheck.com>
Date:   Thu Jun 6 16:10:05 2019 +0200

    2019-06-06

commit 7d522af9bef76291e1098fbba25ff9fa082d6584
Author: Łukasz Przybył <lukasz.przybyl@holidaycheck.com>
Date:   Wed Jun 5 14:37:03 2019 +0200

    2019-06-05

commit 65bf08b54e720cd1803210668e96a1dee86bd286
Author: Łukasz Przybył <lukasz.przybyl@holidaycheck.com>
Date:   Mon Jun 3 09:28:21 2019 +0200

    2019-05-28
```

## The benefits

Now, I can start making notes right in my console and files will be stored in my homedir. `note companymeeting` will create a file `~/Documents/notes/2019-06-10_companymeeting`.

And when I am feeling down and pointless about my work, all I need to do is `git diff` with commits from 2-3 days ago and I can see my desired tangible proof of progress I have done with my work. 

Maybe it will help some of you, it sure did help me a lot!
