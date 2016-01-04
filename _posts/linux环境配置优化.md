title: linux环境配置优化
date: 2016-01-03 18:58:48
tags: linux profile
---
优化linux profile环境配置，解决配置文件复杂的问题

<!--more-->
1. 标准环境配置
	/etc/profile 配置

2. 环境配置优化
	查看/etc/profile 可以发现一个脚本
	```bash
		if [ -d /etc/profile.d ]; then
		  for i in /etc/profile.d/*.sh; do
		    if [ -r $i ]; then
		      . $i
		    fi
		  done
		  unset i
		fi
	```
	这里意思加载环境变量会加载 /etc/profile.d 目录下的所有sh文件 
	这就意味着我们可以把独立的配置单独一个sh放到目录下 

3.	为了方便管理 我们可以在目录下 用 ln -s 来引用脚本 
	例如： 
	java 环境 
	```bash
		- java:/usr/local/java/jdk1.7.0_71 
		$ mkdir /usr/local/profile.d 
		$ vi /usr/local/profile.d/java.sh
		
			export JAVA_HOME=/usr/local/java/jdk1.7.0_71
			export CLASSPATH=.:$JAVA_HOME/lib
			export PATH=$JAVA_HOME/bin:$PATH
		
		$ cd /etc/profile.d 
		$ ln -s /usr/local/profile.d/java.sh 
		$ source /etc/profile
	```
end..