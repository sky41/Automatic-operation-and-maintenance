\#!/bin/bash

read -p "光盘是否已连接(y/n)" a

case $a in

y)

echo "正在配置yum源中"

ping -c5 www.baidu.com &> /dev/null

 if [ $? -eq 0 ];

   then

   mount /dev/sr0 /mnt &> /dev/null

   mkdir -p /etc/yum.repos.d/repo.bak

   mv /etc/yum.repos.d/* /etc/yum.repos.d/repo.bak &> /dev/null

   wget -O /etc/yum.repos.d/CentOS-Base.repo https://mirrors.aliyun.com/repo/Centos-7.repo &> /dev/null

   "yum clean all && yum makecache" &> /dev/null

   echo "在线yum源已配置完成"

 else

   mount /dev/sr0 /mnt &> /dev/null

   mkdir -p /etc/yum.repos.d/repo.bak

   mv /etc/yum.repos.d/* /etc/yum.repos.d/repo.bak &> /dev/null

   echo '[local]                       

name=local           

baseurl=file:///mnt           

enabled=1                        

gpgcheck=0' > /etc/yum.repos.d/local.repo

   "yum clean all && yum makecache" &> /dev/null

   echo "本地yum源已配置完成"

  fi

;;

n)

 echo "请连接光盘再执行该脚本"

;;

*)

 echo "错误命令无法识别"

esac