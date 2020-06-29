---
title: Bash_usage
date: 2020-06-29 20:39:09
categories:
- Tools
- Bash
tags:
- Bash
---

## Useful Tools
1. [z.lua(zh)](https://github.com/skywind3000/z.lua)
2. [fzf](https://github.com/junegunn/fzf)
3. [rg](https://github.com/BurntSushi/ripgrep)
4. [fd](https://github.com/sharkdp/fd)

## Miscellaneous
1. `cat url-list.txt | xargs wget -c`xargs将参数列表转换成小块分段传递给其他命令
1. ssh scp 免密登录`ssh-keygen -t rsa && ssh-copy-id -i ~/.ssh/id_rsa.pub root@10.10.129.25`  或将一台机器的id_rsa.pub复制到另一台机器~/.ssh/authorized_keys文件中
1. `tree -L 2`  查看二级目录结构
1. `lsb_release -a`  查看操作系统版本，是Ubuntu还是CentOS，是14.04还是16.04
1. `./test.sh  2>&1 | tee test.log` log同时输出到前台和文件中    可以不带2>&1(将标准错误输出到标准输出)
   `./test.sh 2>test.log 1>&2`
1. IP地址别名，如服务器别名 `/etc/hosts 10.10.0.61 dg16`
1. `ssh -v root@10.10.129.25` 通过[-v]参数，查看ssh连接的具体过程
1. `echo123456 | sudo -S ./winless.sh`   以root权限来执行文件 这里123456是密码，参数-S专门为执行sudo命令的时候要输入密码而准备的，表示标准输入。
1. ssh打洞，中间机器运行 `ssh -R10115:${IP1}:22 ${IP2}`
   然后运行 `rsync -avz --progress -e 'ssh -p 10115' ${FILES} localhost:${PATH}`
1.  w查看登录的用户 who 向登录用户发消息 `( echo jia > /pts/20 for i in `who | awk '{print $2}'`; do echo "${i}" > /dev/${i}; done`
1.  开发板命令显示颜色：`alias ll="ls -al --color=auto"     alias ls="ls --color=auto"`
1. `nslookup www.baidu.com`  域名查询命令
1. split 将一个大文件分割成多个小文件
1. `chmod 777 -R work_space` 改变目录下所有文件权限
1. `time program` 测试程序运行时间
1. `ssh -XY jiaxiyang@10.10.0.61` 需要的时候显示图形界面
1. `arp -na` 查看网络中连接情况
1. `find  .  -name '*'  -exec touch {} \;` 修改当前目录及子目录中所有文件的时间
1. `chattr` 修改文件（夹）属性 不能被删除
1. `figlet "jia" -f scrpt(ls /usr/share/figlet)` 改变输出字体大小
1. `ln -s   source  target`   创建软连接
1. ln 非常有用，可以使用ln来重新命名文件，可以提供一层虚拟层，文件名字路径改变只需重新链接一下，上层代码不用改变。例如xilinx所有硬盘都连接到 /proj/rdi/staff/xiyang 方便操作
1. `watch -d -n 1 ./Re   reg` 每隔1秒查看程序变化
1. `axel -n 15（线程数）URL`     多线程下载
1. `apt-cache search trash`  搜索安装包
1. `ldconfig -p `查看系统安装的库
1. `ldconfig -p | grep pcap` 查看系统是否安装pcap
1.  `pkg-config --modversion poppler-data` 查看库版本 , pkg-confg配置文件在/usr/share/pkgconfig下(pkg-config一般为开发者使用，文件系统中勾选-dev)
1. `sudo dpkg --install atom-amd64.deb`   dpkg安装.deb软件包
1. `export PATH="/home/zxy/Desktop:$PATH"`   添加环境变量
1. `linuxlogo` 命令行显示linux logo
1. `sudo mount -t tmpfs -o size=8G tmpfs ramdisk/` 创建内存文件系统， 可以加快程序运行时间。
1. `hostname` 查看主机名
1. `tar -zxvf aa.tar.gz BOOT.BIN` 单独解压 某个文件 `tar -tf` 压缩包名称，可以查看压缩包内容  https://www.cnblogs.com/manong--/p/8012324.html
1. `speedtest-cli` 测下载上传网速
1.  `curl -O -u jiaxiyang:jiaxiyang -s[-#]`
1.  `wget -c url`   支持断点续传  好用，可以用来下载大文件，比如： petalinux cache 30G
1. rsync 同步数据， 可以启服务备份数据   `rsync -avzr --progress  test --exclude=test/5 10.10.0.98:/home/jiaxiyang/`   多用rsync，少用scp
1. `crontab -e`  定时执行脚本 cat /var/mail/jiaxiyang查看结果
1. `syncthing` 文件同步神器
1. `nl file` 显示行号
1. `realpath` 查看文件全路径
1. `shotwell` *.jpg 打开图片
1. `vimdiff dp` 快速移动不同
1. `stat -c %s file` 查看文件长度
1. `stat -z %s file` 查看文件修改时间
1. `rm file || true` 如果不存在执行true，还是会报错，但$?返回为0 使用，使用bash -ex时不会退出。
1. `cat file | grep -v '^#'` 输出不以#号开头的行
1.  `SCRIPT_PATH=$(dirname  $(realpath xx.sh)) ` 比pwd要好，pwd显示的是虚拟链接地址。
1.  `PROJECT_NAME=$(basename $(SCPRIT_PATH))` 当前脚本所在的工程名字
1. `sshpass -p root（密码） ssh -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null root@10.10.129.22 '/etc/init.d/led start'`  跨机器执行命令 在机器A上调用，在机器B上执行，将结果输出到A上。
1. `sshpass -p root（密码） ssh(scp) -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null root@10.10.129.22   ssh -y -y  root@zu9-2  " ' cd /home && ls'"  `zu9 上执行 cd /home && ls 注意  要同时加双引号和单引号。sshpass -p jiaxiyang scp -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null static_ip.txt jiaxiyang@10.10.0.96:~
1. `tar -cf - zu9_test | sshpass -p root ssh -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null root@10.10.129.133 ssh -y -y zu9-2 tar -xvf - -C /var`  跨机器cp文件并免密