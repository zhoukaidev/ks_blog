# 简介

`ssh-keygen`是用于生成,管理以及转换授权密钥的工具。


## 操作流程

* `ssh-keygen`支持很多不同的参数组合,用于生成可以用于登录的rsa key pairs
* 生成相应的key之后，可以使用`ssh-copy-id`参数来讲相应的public key文件安装到远端服务器上
    * `ssh-copy-id -i ~/.ssh/my.pub myusrname@server-ip-address`
    * ssh-copy-id installs an SSH key on a server as an authorized key. Its purpose is to provide access without requiring a password for each login. This facilitates automated, passwordless logins and single sign-on using the SSH protocol.
    * [ssh-copy-id参考文档](ssh-copy-id installs an SSH key on a server as an authorized key. Its purpose is to provide access without requiring a password for each login. This facilitates automated, passwordless logins and single sign-on using the SSH protocol.)
* 在服务器上面安装完成相应的public key之后，可以关掉账户名密码的登录方式，来增加系统的安全性
    * `sudo vim /etc/ssh/sshd_config`
    * 设置 `PasswordAuthentication no`
    * `sudo systemctl reload sshd.service`
* 使用你的private key来登录远端的系统
    * `ssh -i ./your_private  usrename@server_ip_address`
#### 生成RSA密钥

在不添加任何参数的情况下,默认会生成RSA密钥.

```sh
$ ssh-keygen
xxxx
```

#### 生成指定类型的密钥

具体支持的类型可以通过`man ssh-keygen`查看。

```sh
# 生成DSA密钥
# -t 指定密钥的类型
# -b 指定密钥的长度
$ ssh-keygen -t dsa
$ ssh-keygen -t rsa -b 4096
```
#### 指定公私钥的存储路径

```sh
# 此命令会在该文件夹下生成名为testkey的公私钥，类型为4096的rsa
$ ssh-keygen -t rsa -b 4096 -f ./testkey
# -C参数可以指定相应的comment
$ ssh-keygen -t rsa -b 4096 -C myname@example.com
```

#### 获取指定公钥的fingerprint

The fingerprint is based on the host's public key, usually based on the /etc/ssh/ssh_host_rsa_key.pub file.  Generally it's for easy identification/verification of the host you are connecting to.

If the fingerprint changes, the machine you are connecting to has changed their public key. 

```sh
# 适用 -l 来获取
# -f 指定公钥文件, -l 指定获取fingerprint
$ ssh-keygen -l -f xxx.pub
```

#### 指定fingerprint的编码格式

```sh
# 当使用putty登陆时,显示的fingerprint适用MD5编码进行显示
# 在ssh-keygen也可以通过 -E 指定显示的格式
$ ssh-keygen -E md5 -l -f xxx.pub
```

### 参考文档 

* [How to configure ssh key based authentication on linux](https://www.digitalocean.com/community/tutorials/how-to-configure-ssh-key-based-authentication-on-a-linux-server)
* [Configure ssh key based authentication on raspberry pi](https://www.geekyhacker.com/2021/02/15/configure-ssh-key-based-authentication-on-raspberry-pi/)