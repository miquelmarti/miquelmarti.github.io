---
title: "Setting automatically a new wallpaper everyday"
excerpt_separator: "Here"
categories:
tags:
  - wallpaper
  - code
  - gnome
  - linux
  - bash
  - cron
  - national geographic
---

I have lately been an huge number of hours everyday in front of the computer and I kind of got tired of always the same background. In one of my usual Facebook News Feed scrolls I saw a beautiful picture of National Geographic.

![](http://yourshot.nationalgeographic.com/u/fQYSUbVfts-T7odkrFJckdiFeHvab0GWOfzhj7tYdC0uglagsDtoTKxqCP1z0Hak_pgOxThc6hM3eoBBMTTfODmgSWl6ow8KpZq9UjHr-XsVTAfam_KXKjcXuvLHf3Tp37GP2yfMIHkeR65M8YYwhf0xoWSO-M81UAY5AhyuPD_OohhIYdDxbyGBYEhLuSA1VPzUa0peK4c5RKJr_dCYaDjgKXNJBNE/)
*National Geographic Photo of the day 27/12/2016 by [Yan Gao](http://yourshot.nationalgeographic.com/photos/9092904/)*

So I decided that I wanted to have it as my wallpaper. But I don't want only that one, I want the one that is published everyday. First thing? Google it. Result? [Someone](https://www.google.co.jp/webhp?sourceid=chrome-instant&ion=1&espv=2&ie=UTF-8#q=ubuntu%20photo%20of%20the%20day%20national%20geographic) had already thought about it, ofc.

I tried one solution and it did not work so I decided to do it myself from scratch instead and here is the result. Working on Ubuntu 16.04:

<script src="https://gist.github.com/miquelmarti/f821239313c4462ef23205b64102f460.js"></script>

To set it up:

- Download the script and make it executable:

```
chmod +x wod.sh
```

- Then run:

```
crontab -e
```

- And add a line as:

```
@daily /home/<user>/wod.sh
```
