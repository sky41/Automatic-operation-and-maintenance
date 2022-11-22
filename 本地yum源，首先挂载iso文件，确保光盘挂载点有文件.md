**本地****yum****源，首先挂载****iso****文件，确保光盘挂载点有文件**

如果出现yum被another app lock使用下面命令

rm -f /var/run/yum.pid

创建挂载点
 mkdir -p /mnt/local
 将iso文件挂载到指定挂载点
 mount /dev/cdrom /mnt/local

[root@xuexi yum.repos.d]# ls /mnt/local

CentOS_BuildTag EULA images  LiveOS  repodata    RPM-GPG-KEY-CentOS-Testing-7

EFI       GPL  isolinux Packages RPM-GPG-KEY-CentOS-7 TRANS.TBL

**2****、****yum****的一切配置信息都存储在一个叫****yum.repos.d****目录下的配置文件中。所以跳转到****/etc/yum.repos.d****目录下**

cd /etc/yum.repos.d

**3****、创建一个新的****yum****源配置文件，****yum****源配置文件的结尾必须是****.repo**

vim CentOS7.repo

内容如下：

[CentOS7]         //yum的ID，本地唯一，用于区分不同yum源
 name=CentOS-server     //描述信息
 baseurl=file:///mnt/local    //前面的file://是协议，后面的/mnt是光盘挂载点
 enabled=1         //1启用yum源，0禁用yum源
 gpgcheck=0         //1使用公钥验证rpm包的正确性，0不验证

保存退出后就可以开始验证了。

 如果启用公钥验证，需要配置公钥gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

**4****、接着清空****yum****已存在的源信息（缓存）**

**yum clean all**

**yum makecache**

 

**yum repolist    //****验证****local yum****源是否配置成功**

**5****、最后****yum makecache**查看本地源的所有软件,由于不太好展示，我只能大概说一下。使用命令” yum list | more”（注意使用more限制一下输出），列表会有三列输出，在最后一列显示的是yum的ID（这里就是上面的[CentOS7]），有你设置的yum的ID就是成功了。