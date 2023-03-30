---
title: Gitee Error
date: 2023-03-30 14:30:00
tags: [Gitee,Error]
categories: [Gitee,Error]
---

收集所有遇见过 Gitee 提交错误, 并提供及解决方法.

<!-- more -->

1. GE007

	    remote: error: GE007: Your push would publish a private email address.
	    remote: You can make your email public or disable this protection by visiting:
	    remote: https://gitee.com/profile/emails
	    remote: error: hook declined to update refs/heads/master
	    To gitee.com:procedural-ape-lao-li/procedural-ape-lao-li.git
	     ! [remote rejected] HEAD -> master (hook declined)
	    error: failed to push some refs to 'gitee.com:procedural-ape-lao-li/procedural-ape-lao-li.git'

	原因：Gitee "不公开我的邮箱地址", 同时禁止命令行 "推送暴露个人邮箱".

	解决方法一：登陆 Gitee, 设置 -> 邮箱管理. "不公开我的邮箱地址" 或 "推送暴露个人邮箱".

	解决方法二：登陆 Gitee, 设置 -> 邮箱管理. 使用 Gitee 自动生成的提交邮箱.

		# 设置提交邮箱
		git config --global user.email 12666884+procedural-ape-lao-li@user.noreply.gitee.com

		# 查看全部变量
		git config -l
