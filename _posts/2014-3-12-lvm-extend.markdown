---
layout: post
title:  "LVM扩展磁盘空间"
date:   2014-3-12 22:40:00
categories: blog
tags: linux lvm
---

1. 用fdisk分区

2. 初始化为pv `sudo pvcreate /dev/sda6`

3. 将分区加入vg `sudo vgextend vg1 /dev/sda6`

4. 扩展lv `sudo lvextend -L +100G /dev/vg1/vg1_home`

5. 扩展文件系统 `sudo resize2fs /dev/vg1/vg1_home`
