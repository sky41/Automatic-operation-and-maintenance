*#!**/bin/bash*

*#* *微信公众号skywdie*

*#* *程序开发作者刘清政*

*#* *定义函数名slFunlocalyum配置本地yum源函数*

*#* *定义函数名slFunnetwork查看网络信息*

*#* ***** Shell脚本运维编程考查 **** #*

*#* *功能需求*

*#* *编写Shell脚本，实现运维常用工具箱，能够根据用户输入的菜单项执行相应功能，具体支持如下功能：*

*#* *（1）查看系统信息，包括：内核版本、Linux发行版本、内存信息、CPU信息、磁盘信息、IP地址等信息。*

*#* *（2）一键配置网络IP地址（ip、掩码、网关、dns由用户输入），并输出配置好之后的IP地址信息。*

*#* *（3）一键配置本地YUM源，并输出配置好之后的repolist信息。*

*#* *（4）一键关闭并永久关闭防火墙与SELinux。*





*#**<-------------------------------------------------主函数调用全局函数*

main(){

​    TTTT

​    whether

​    while :

​    do

​    ToolboxMenu *#**<-----------------------系统选项菜单函数*

​    read -p "Please enter your choice![1..8]" number

​            case $number in

​            1)

​            *#**<-----------------------yum源配置函数*

​            slFunlocalyum 

​            ;;

​            2)

​            *#**<-----------------------网络配置函数*

​            slFunnetwork 

​            ;;

​            3)

​            *#**<-----------------------查看系统信息函数*

​            slFunsystemin 

​            ;;

​            4)

​            *#**<-----------------------一键关闭防火墙和selinux函数*

​            ;;

​            5)

​            *#**<-----------------------检验linux安全启动项*

​            ;;

​            8)

​            *#**<-----------------------其他功能函数*

​            Function 

​            ;;

​            *)

​            *#**<-----------------------待开发或设定为exit退出函数*

​            exit

​            ;;

​            esac

​    done

}

*#**<-------------------------------------------------判断是否需要工具箱服务*

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

 echo -e "\033[33m |       1.yum源配置选项              | \033[0m"

 echo -e "\033[33m |       2.网络配置选项               | \033[0m"

 echo -e "\033[33m |       3.查看系统信息               | \033[0m"

 echo -e "\033[33m |       4.一键关闭防火墙和selinux          | \033[0m"

 echo -e "\033[33m |       5.查看进程信息               | \033[0m"

 echo -e "\033[33m |       6.                     | \033[0m"

 echo -e "\033[33m |       7.Exit Toolbox               | \033[0m"

 echo -e "\033[33m |       8.其他功能lbox               | \033[0m"

 echo -e "\033[33m | Current Time:$(date "+%Y-%m-%d %H:%M:%S") welcome!!engineer! |\033[0m"

 echo -e "\033[5;34m =============System detection toolbox=================\033[0m"

}

TToolboxMenu () {

 echo -e "\033[5;34m ========This is a anython detection toolbox============\033[0m"

 echo -e "\033[33m |       1.查看磁盘挂载信息              | \033[0m"

 echo -e "\033[33m |       2.查看内存信息               | \033[0m"

 echo -e "\033[33m |       3.查看CPU信息                | \033[0m"

 echo -e "\033[33m |       4.查看网络端口信息              | \033[0m"

 echo -e "\033[33m |       5.查看进程信息                | \033[0m"

 echo -e "\033[33m |       6.磁盘每秒进程下的I0读写数量         | \033[0m"

 echo -e "\033[33m |       7.Exit Toolbox               | \033[0m"

 echo -e "\033[33m | Current Time:$(date "+%Y-%m-%d %H:%M:%S") welcome!!engineer! |\033[0m"

 echo -e "\033[5;34m =============System detection toolbox=================\033[0m"

}

*#**<-------------------------------------------------*

*#* *（3）一键配置本地YUM源，并输出配置好之后的repolist信息。*

slFunlocalyum(){

  echo"欢迎进入yum源本地配置功能"

  read -p "光盘是否已连接(y/n)" a

  case $a in

  y)

​    read -p "选择网络1或者本地yum源2" netlocal

​    case $netlocal in

​    1)

​    echo "正在配置网络yum源中"

​    echo "正在再次验证网络环境"

​    ping -c5 www.baidu.com &> /dev/null

​    echo "网络检验通过"

​    if [ $? -eq 0 ];

​        then

​        *#* *mount /dev/sr0 /mnt &> /dev/null*

​        *#* *mkdir -p /etc/yum.repos.d/repo.bak*

​        *#* *mv /etc/yum.repos.d/\* /etc/yum.repos.d/repo.bak &> /dev/null*

​        *#* *wget -O /etc/yum.repos.d/CentOS-Base.repo https://mirrors.aliyun.com/repo/Centos-7.repo &> /dev/null*

​        *#* *"yum clean all && yum makecache" &> /dev/null*

​        echo "在线yum源已配置完成"

​        yum repolist

​    else

​        echo "网络环境有问题，请检查后再使用网络yum源配置选项"

​        

​    fi

​    ;;

​    2)    

​        echo "正在配置本地yum源中"

​        mount /dev/sr0 /mnt &> /dev/null

​        mkdir -p /etc/yum.repos.d/repo.bak

​        mv /etc/yum.repos.d/* /etc/yum.repos.d/repo.bak &> /dev/null

​        echo '[local]                       

​           name=local            

​           baseurl=file:///mnt           

​           enabled=1                        

​           gpgcheck=0' > /etc/yum.repos.d/local.repo

​        "yum clean all && yum makecache" &> /dev/null

​        echo "本地yum源已配置完成"

​        yum repolist

​    ;;

​    esac

  ;;

  n)

   echo "请连接光盘再执行该脚本"

  ;;

  *)

   echo "错误命令无法识别"

  esac



}

*#**<-------------------------------------------------*

*#* *（2）一键配置网络IP地址（ip、掩码、网关、dns由用户输入），并输出配置好之后的IP地址信息。*



slslFunnetwork(){

​    echo"欢迎进入网络配置工具"

​    read -p "是否需要一键配置网络(y/n)" ipsl

​    case $ipsl in

​    y)

​    echo "请确定网络配置文件位置"

​    read -p "配置文件路径：" netfile

​    `cd $netfile`

​    read -p "是否(y/n)需要文件备份以防文件配置错误崩溃" fileerror

​    case $fileerror in 

​    y)

​    echo ""

​    ;;

​    n)

​    ;;

​    esac

​    *#**定义网络配置文件变量*

​    BOOTPROTO1=static *#**静态IP*

​    BOOTPROTO2=dhcp *#**动态IP*

​    BOOTPROTO3=none *#**无（不指定）*

​    *#**通常情况下是dhcp或者static*

​    *#**ONBOOT ：是否开机*

​    *#**ifcfg-ens33文件参数*

​    TYPE=Ethernet      *#* *网络类型为以太网*

​    BOOTPROTO=none  *#**ip获取方式，DHCP为自动获取，静态IP为none和static*

​    NAME=ens33       *#**网卡名称*

​    DEVICE=ens33      *#* *网卡设备名，设备名一定要跟文件名一致* 

​    ONBOOT=yes       *#* *该网卡是否随网络服务启动*

​    IPADDR=192.168.146.129   *#* *该网卡ip地址* 

​    NETMASK=255.255.255.0   *#* *子网掩码*

​    GATEWAY=192.168.146.2   *#* *网关*

​    DNS1=8.8.8.8          *#*  *8.8.8.8为Google提供的免费DNS服务器的IP地址*  

​    DNS2=8.8.4.4       *#*  *8.8.4.4为Google提供的免费DNS服务器的IP地址*  





​    echo "一键配置网络运行中"

​    ;;

​    n)

​    echo "正在退出配置功能"

​    ;;

​    *)

​    echo "命令错误"

​    ;;

​    esac



}



}

*#**<-------------------------------------------------*

*#* *（1）查看系统信息，包括：内核版本、Linux发行版本、内存信息、CPU信息、磁盘信息、IP地址等信息。*

function slFunsystemin(){

​    echo "sssss"

}

*#**<-------------------------------------------------*

*#**（4）一键关闭并永久关闭防火墙与SELinux。*

selinux(){

​    echo "欢迎进入linux安全防护设置"

​    read -p "一键永久关闭防火墙与selinux,\n一键临时关闭防火墙与selinux,\n一键开启防火墙与selinux" liself

​    case $liself in

​    1)

​    echo "已经永久关闭防火墙与selinux"

​    ;;

​    2)



​    ;;

​    3)

​    ;;

​    4)

​    ;;

​    5)

​    ;;

​    esac

}

function Function(){

  *#**<----------------邀请用户输入需要检测的信息*

  echo "欢迎进入其他功能"

  while :

  do

​      TToolboxMenu

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

TTTT(){

​    



​    trap 'onCtrlC' INT

​    function onCtrlC () {

​        *#**捕获CTRL+C，当脚本被ctrl+c的形式终止时同时终止程序的后台进程*

​        kill -9 ${do_sth_pid} ${progress_pid}

​        echo

​        echo 'Ctrl+C is captured'

​        exit 1

​    }

​    

​    do_sth() {

​        *#**运行的主程序*

​        echo "运行环境自检"

​        ping  -c 4 www.baidu.com

​        echo "网络环境良好"





​    }

​    

​    progress() {

​        *#**进度条程序*

​        local main_pid=$1

​        local length=20

​        local ratio=1

​        while [ "$(ps -p ${main_pid} | wc -l)" -ne "1" ] ; do

​            mark='>'

​            progress_bar=

​            for i in $(seq 1 "${length}"); do

​                if [ "$i" -gt "${ratio}" ] ; then

​                    mark='-'

​                fi

​                progress_bar="${progress_bar}${mark}"

​            done

​            printf "正在进入: ${progress_bar}\r"

​            ratio=$((ratio+1))

​            *#**ratio=`expr ${ratio} + 1`*

​            if [ "${ratio}" -gt "${length}" ] ; then

​                ratio=1

​            fi

​            sleep 0.1

​        done

​    }

​    

​    do_sth &

​    do_sth_pid=$(jobs -p | tail -1)

​    

​    progress "${do_sth_pid}" &

​    progress_pid=$(jobs -p | tail -1)

​    

​    wait "${do_sth_pid}"

​    printf "Progress: done         \n"

​    

}

main