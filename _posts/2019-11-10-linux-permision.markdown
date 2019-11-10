---
layout: post
title:  "Linux: permission denied"
date:   2019-11-10 19:27:16 +0100
categories: linux
---
If you run the command less /etc/shadow you'll get /etc/shadow: Permission denied so you have to run it with sudo command, but if you assign a alias like this alias please='sudo $(history -p !!)' and just run please after you get permission denied that it should work :)
