
#
~ 当前用户的主目录，如/home/www

[Bash 脚本 set 命令教程 - 阮一峰的网络日志](http://www.ruanyifeng.com/blog/2017/11/bash-set.html)

# 构建环境
安装nodejs
[Installing Node.js via package manager | Node.js](https://nodejs.org/en/download/package-manager/)
yarn


# 部署
[ssh-keygen 基本用法 | Yet Another Summer Rain](https://www.liaohuqiu.net/cn/posts/ssh-keygen-abc/)
[Using SSH keys with GitLab CI/CD - GitLab Documentation](https://docs.gitlab.com/ee/ci/ssh_keys/README.html)
[两台Linux系统之间传输文件的几种方法 - CSDN博客](http://blog.csdn.net/gatieme/article/details/51673229)

[rsync命令_Linux rsync 命令用法详解：远程数据同步工具](http://man.linuxde.net/rsync)
[Rsync（远程同步）：10 Linux中Rsync命令的实际示例](https://www.howtoing.com/rsync-local-remote-file-synchronization-commands/)
[《rsync同步的艺术》–linux命令五分钟系列之四十二 – Linux大棚](http://roclinux.cn/?p=2643)
[Rsync（远程同步）：10 Linux中Rsync命令的实际示例](https://www.howtoing.com/rsync-local-remote-file-synchronization-commands/)

rsync同步两个本地目录， 注意源文件夹和目标文件夹后都有/，否则会将r1同步到r2目录下面

rsync -ravz /export/servers/r1/ --delete /export/servers/r2/
rsync同步到远程目录：

rsync -ravz /export/servers/r1/ --delete root@192.168.158.133:/export/servers/r2/
如果远程没有指定文件夹，会自动先创建文件夹，然后再同步文件。

首先需要将源服务器的ssh公钥复制到目标服务器上

执行ssh-keygen命令，然后连续两次回车，生成公钥文件。 然后执行ssh-copy-id -i ~/.ssh/id_rsa.pub 192.168.158.132 将公钥文件复制到目标服务器，需要输入132的密码。

ssh-copy-id -i ~/.ssh/id_rsa.pub root@服务器地址

然后就可以通过下面命令，无须输入密码同步文件了：

rsync -avze ssh /export/servers/r1/ --delete admin@192.168.158.132:/export/servers/r2/


scp使用的是ssh协议，通过密钥对进行加密和解密，做法是通过以下命令生成密钥对：

```
$ ssh-keygen
```

在执行过程中会让你输入密钥存储的文件名，比如输入的是mykey，提示输入密码的时候直接回车。以上完成后会生成两个文件，mykey和mykey.pub，其中mykey.pub是公钥，mykey是私钥，你需要把公钥mykey.pub的内容copy到服务器端的/home/username/.ssh/authorized_keys文件中，如果.ssh目录和authorized_keys不存在，则手动创建。  
以上完成之后，你就可以使用以下命令还进行scp操作了。

```
scp -i /path/to/private-key /path/to/source username@xxx.yyy.zzz.www:/path/to/dest
```

其中/path/to/private-key为上面生成的私钥mykey，要保证私钥的权限为600。
