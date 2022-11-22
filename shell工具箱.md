*#!**/bin/bash*

*#!**/bin/csh* 

*#* *微信公众号skywdie*

*#* *程序开发作者刘清政*

*#* *定义函数名slFunlocalyum配置本地yum源函数*

*#* *定义函数名slFunnetwork查看网络信息*

*#* *定义函数名function查看网络信息*





*#**<-------------------------------------------------主函数调用全局函数*

main(){

  whether

  while :

  do

  ToolboxMenu

  read -p "Please enter your choice![1..7]" number

​          case $number in

​          1)

​          slFunlocalyum

​          ;;

​          2)

​          slFunnetwork

​          ;;

​          esac

  done

}

*#**<-------------------------------------------------*

whether () { read -p "Continue to use[y],sign out[n]:" play

​    if [[ "$play" == "y" ]];then

​    clear

​    else

​        echo "Thank you for your use. Have a nice day!";exit

​    fi

}

*#**<-------------------------------------------------*

ToolboxMenu(){

 echo -e "\033[5;34m ========This is a system detection toolbox============\033[0m"

 echo -e "\033[33m |       1.yum源配置                  | \033[0m"

 echo -e "\033[33m |       2.查看ip网络信息                 | \033[0m"

 echo -e "\033[33m |       3.查看CPU信息               | \033[0m"

 echo -e "\033[33m |       4.查看网络端口信息              | \033[0m"

 echo -e "\033[33m |       5.查看进程信息               | \033[0m"

 echo -e "\033[33m |       6.                     | \033[0m"

 echo -e "\033[33m |       7.Exit Toolbox              | \033[0m"

 echo -e "\033[33m | Current Time:$(date "+%Y-%m-%d %H:%M:%S") welcome!!engineer! |\033[0m"

 echo -e "\033[5;34m =============System detection toolbox=================\033[0m"

}

*#**<-------------------------------------------------*

slFunlocalyum(){

  echo"欢迎进入yum源本地配置功能"

  read -p "光盘是否已连接(y/n)" a

  case $a in

  y)

  echo "正在配置yum源中"

  ping -c5 www.baidu.com &> /dev/null

   if [ $? -eq 0 ];

​     then

​     mount /dev/sr0 /mnt &> /dev/null

​     mkdir -p /etc/yum.repos.d/repo.bak

​     mv /etc/yum.repos.d/* /etc/yum.repos.d/repo.bak &> /dev/null

​     wget -O /etc/yum.repos.d/CentOS-Base.repo https://mirrors.aliyun.com/repo/Centos-7.repo &> /dev/null

​     "yum clean all && yum makecache" &> /dev/null

​     echo "在线yum源已配置完成"

   else

​     mount /dev/sr0 /mnt &> /dev/null

​     mkdir -p /etc/yum.repos.d/repo.bak

​     mv /etc/yum.repos.d/* /etc/yum.repos.d/repo.bak &> /dev/null

​     echo '[local]                       

  name=local            

  baseurl=file:///mnt           

  enabled=1                        

  gpgcheck=0' > /etc/yum.repos.d/local.repo

​     "yum clean all && yum makecache" &> /dev/null

​     echo "本地yum源已配置完成"

​    fi

  ;;

  n)

   echo "请连接光盘再执行该脚本"

  ;;

  *)

   echo "错误命令无法识别"

  esac



}

*#**<-------------------------------------------------*

slFunnetwork(){

  echo"欢迎进入网络配置工具"

  read -p "是否需要一键配置网络(y/n)" ipsl

  case $ipsl in

  y)

  echo "一键配置网络运行中"

  ;;

  n)

  echo "正在退出配置功能"

  ;;

  *)

  echo "命令错误"

  ;;

  esac



}

function function(){

  *#**<----------------邀请用户输入需要检测的信息*

  while :

  do

​      ToolboxMenu

​      read -p "Please enter your choice![1..7]" number

​          case $number in

  *#**<-----------------------------------------------------------磁盘挂载信息*

​          1)

​                  echo -e "\033[5;34m ============Partition information${z}============\033[0m"

​                  df -hT

​                  whether

​          ;;

  *#**<------------------------------------------------------内存使用情况*

​          2)

​              echo -e "\033[5;34m ============Memory usage============\033[0m"

​              free -h

​              n=1

​              for i in {1..3}

​              do

​                  echo -e "\033[5;34m ============Memory usage${n}============\033[0m"

​                  vmstat | awk '{if(NR==3){print "You have free memory left:" $4}}'

​                  let ++n

​                  sleep 1

​              done

​              whether

​          ;;

  *#**<-------------------------------------------------------CPU利用率和负载*

​          3)

​              v=1

​              for i in {1..3}

​              do

​                  echo -e "\033[5;34m ============CPU usage${v}===========\033[0m"

​                  uptime

​                  vmstat | grep 2 |awk '{if (100-$15<=10){print 100-$15 "%","您的CPU很安全"}else{print 100-$15 "%","您的CPU即将满载请留意"}}'

​                  let ++v

​                  sleep 1

​              done

​                  whether

​          ;;

  *#**<---------------------------------------------------------------网络端口信息*

​          4)

​              while :

​              do

​                  echo -e "\033[5;34m ============Network port information============\033[0m"

​                  read -p "Please enter the network port number you want to query:" Port

​                  netstat -anpt | head -2

​                  netstat -anpt | grep $Port

​                  read -p "Do you want to check the port?[y/n]" see

​                  if [[ ! $see == "y" ]];then

​                      echo "Thank you for your use. Have a nice day!";exit

​                  else

​                      break

​                  fi

​              done

​              whether

​          ;;

  *#**<----------------------------------------------------------------进程信息查询*

​          5)

​              echo -e "\033[5;34m ============Process information============\033[0m"

​              read -p "Please enter the process information you want to query:" Process

​              ps aux | grep -v grep |grep $Process

​              whether

​          ;;

  *#**<-------------------------------------------磁盘每秒进程下的IO读、写请求数量*

​          6)

​              b=1

​              for i in {1..3}

​              do

​                  echo -e "\033[5;34m ============Number of IO read / write requests issued by the process${b}============\033[0m"

​                  iostat | grep ^sd | awk '{print $1,$2}'

​                  let ++b

​                  sleep 1

​              done

​                  whether

​          ;;

  *#**<---------------------------------退出*

​          7)

​              echo -e "\033[36 Thank you for your use. Have a nice day!\033[0m"

​              exit

​          ;;

  *#**<------------------没有匹配项重新显示菜单*

​          *)

​              echo -e "\033[31m  Error redirecting to menu for you ! \033[0m"

​          ;;

​      esac

  done

  *#**script end*    

  }

main

  

​           