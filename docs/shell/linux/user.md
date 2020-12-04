# 简介

本文主要用于介绍`Ubuntu`下用户管理的相关指令。

## 指令集

* 添加用户
  * [Create a User account on ubuntu ](https://www.cyberciti.biz/faq/create-a-user-account-on-ubuntu-linux/)
  * [What is difference between "adduser" and "useradd"](https://askubuntu.com/questions/345974/what-is-the-difference-between-adduser-and-useradd)

```sh  
# 添加kaizhou用户    
sudo adduser kaizhou
```
 
* 修改用户组

```sh
# 修改用户组  
# 将newUser 添加到sudo用户组  
# -a : 指定将用户追到到用户组  
# -G : 用于指定用户组  
usermod -aG sudo newUser  
```
  
* [Create sudo user on ubuntu](https://phoenixnap.com/kb/how-to-create-sudo-user-on-ubuntu)
* [新加入一个用户组后，如何再不退出shell的情况下加载新的用户组](https://superuser.com/questions/272061/reload-a-linux-users-group-assignments-without-logging-out)
