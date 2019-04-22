# notes
some notes for Linux  

[基本操作](#基本操作)  
[文件及目录](#文件及目录)  
[时间及日期](#时间及日期)  
[打包压缩](#打包压缩)  
[软件安装](#软件安装)  
[网络常用命令](#网络常用命令)  
[shell使用](#shell使用)  
[vi/vim](#vi/vim)  
[磁盘及文件系统](#磁盘及文件系统)  
[文件权限管理](#文件权限管理)  
[用户和用户组管理](#用户和用户组管理)  
[网络配置命令](#网络配置命令)  

## 一些热键
Ctrl+C 退出前台执行程序  
Ctrl+D 离当前shell  
Ctrl+L 清屏  
Tab:按一次 命令后自动补全  
Tab:按两次列出以输入开头的所有命令  
## 基本操作  
* **帮助**  
command --help  
man command  
* **注销**  
logout  
exit  
Ctrl+D  
* **关机**  
shutdown  
init 0  
* **重启**  
reboot  
init 6  
* **ssh连接**  
ssh root@\[ip\]  
* **切换账户**  
su student  
* **列出文件和子目录**  
ls  
ll  
* **查看某个命令所在位置**  
whereis command   
## 文件及目录
* **显示当前路径**  
pwd  
* **切换路径**  
cd /  
cd 回到当前用户根目录  
cd ../ 上一级  
* **创建删除目录**  
mkdir  
rmdir  
rm  
* **查看文件或目录占磁盘空间大小**  
du  
* **复制目录及文件**  
cp  
* **创建空文件**  
touch filename  
echo > filename
* **移动目录或文件及重命名**  
mv  
* **cat**  
cat file1 显示文件内容  
cat > file1 从键盘创建一个文件,只能创建新文件,不能编辑已有文件,Ctrl+D退出创建  
cat file1 file2 > file3 将几个文件合并为一个文件   
cat > file1 << EOF 重定向输入文件,文件不存在则新建，同cat << EOF >file  
* **echo**  
echo > test 创建新文件  
echo "aaa" > test 创建并添加  
echo "aaa" >> test 追加  
* **连接**  
ln yy /root/zz 在/root下为文件yy生成一个硬链接zz，-s 软链接  
* **管道**  
  * 把前一个命令的标准输出作为下一个命令的标准输入  
ll | grep "drw"  
  * 将前一个命令的标准输出作管道后一个命令的参数  
echo "--help" | cat 等价于 cat "--help"  
echo "--help" | xargs cat 等价于 cat --help   
* **分页显示**  
more  
* **统计文件行数、字数和字符数**  
wc filename   
* **查看文件**  
file filename 查看文件详细信息  
head filename  
tail filename  
tail -f filename 循环显示最新添加内容  
* **统计两文件呢的不同**  
diff file1 file2  
* **别名**  
alias  
alias psa="/bin/ps -aux" 方便查看进程  
alias f= "find/ -name" 方便全盘查找  
* **通配符**  
\*代表任意个字符  
?代表一个字符  
* **find**  
用来在指定目录下查找文件,并且将查找到的子目录和文件全部进行显示。  
find 搜索文件的命令格式:  
find \[搜索范围\] \[匹配条件\]
选项:  
-name 根据名字查找  
-size 根据文件大小查找, +,-:大于设置的大小,直接写大小是等于  
-user 查找用户名的所有者的所有文件  
-group 根据所属组查找相关文件  
-type 根据文件类型查找(f文件,d目录,l软链接文件)  
-inum 根据i节点查找  
-amin 访问时间access  
-cmin 文件属性change  
-mmin 文件内容modify  
全盘搜索文件名为file的文件  
find / -name file  
/代表是全盘搜索,也可以指定目录搜索  
  * find 和管道  
  * find 和xargs  
* **locate**  
搜素包含特定字符串的文件及目录  
* **grep**  
搜索文件中包含指定字符串的行  
## 时间及日期  
* date  
* cal  
* ntpdate time.nist.gov 和时间域名同步  
## 打包压缩  
打包指归档文件，压缩是将一个大的文件通过压缩算法变成一个小文件  
* **tar**  
“-z” : 同时用gzip压缩  
“-j” : 同时用bzip2压缩  
“-x” : 解包或者解压缩  
“-t” : 查看tar包里面的文件  
“-c” : 建立一个tar包或者压缩文件包  
“-v” : 可视化  
“-f” : 后面跟文件名，压缩时跟 “-f 文件名”，意思是压缩后的文件名为filename, 解压时跟 “-f 文件名”，意思是解压filename. 请注意，如果是多个参数组合的情况下带有 “-f”，请把 “-f” 写到最后面。  
  * 常用压缩组合 czvf  
  * 常见结尾 .tar.gz  
  * 常用解压组合 xzvf  
* **zip unzip**  
zip -r archive_name.zip directory_to_compress  
unzip archive_name.zip  
* **gzip**  
压缩：gzip test.tar  
解压：gzip –d archive_name.gz  
* **bzip2**  
压缩：bzip2 -z  
解压：bzip2 -d  
* **xz**  
压缩率之王  
## 软件安装  
* **rpm**  
* **\*tar.gz**
* **yum**  
  * 安装  
yum install package1 安装指定的安装包package1  
yum groupinsall group1 安装程序组group1
  * 升级  
yum update 全部更新  
yum update package 更新指定程序包package  
yum check-update 检查可更新的程序  
yum upgrade package 升级指定程序包package  
yum groupupdate group 升级程序组group  
  * 查找和显示  
yum info package 显示安装包信息package  
yum list 显示所有已经安装和可以安装的程序包  
yum list package 显示指定程序包安装情况package  
yum search string 根据关键字string查找安装包  
  * 卸载程序  
yum remove package 删除程序包package  
yum groupremove group 删除程序组group  
yum deplist package 查看程序package依赖情况  
  *  清除缓存  
yum clean packages 清除缓存目录下的软件包  
## 网络常用命令  
net-tools和traceroute需要自己安装  
* **查看ip地址**  
 ip addr 显示网卡IP信息  
 ip route list 查看路由信息  
* **查看网络连通性**  
 ping  
* **联网状态**  
netstat  
* **查看或设置路由表**  
route  
* **查看或临时修改主机名**  
hostname  
* **查看当前主机到目的主机经过的节点**  
traceroute  
## shell使用  
标准输入 0  
标准输出 1  
标准错误 2  
* **历史命令**
history  
!  
* **dd**  
dd if=\[STDIN\] of=\[STDOUT\]
用指定大小的块拷贝一个文件，拷贝的同时进行指定的转换  
  * 将本地的/dev/sdb1整盘备份到/root/image  
  dd if=/dev/sdb1 of=/root/image  
  * 将备份文件恢复到指定盘  
  dd if=/root/image of=/dev/hdb  
  * 备份/dev/sdb全盘数据，利用gzip工具压缩并保存到指定路径  
  dd if=/dev/sdb | gzip > /root/image.gz  
* **空设备**  
/dev/null  
* **zero设备**  
/dev/zero  
* **重定向**  
command <<limit_string  
here documents  
limit_string  
## vi/vim
yum -y install vim-enhanced  
默认配置文件位置 /etc/vimrc  
同样值得推荐的文本编辑器还有Emacs,以及轻量级的nano
* **模式切换**  
： i Esc  
* **退出**  
命令模式：ZZ (保存退出），ZQ(直接退出）  
末行模式：q(直接退出)，q！(强制退出)， wq(保存退出）  
* **显示行号**  
末行模式：  
:set number  
:set nu  
* **移动光标**  
在命令行模式下：  
  * 方向键  
  *  Home : 光标移动到本行行首  
  End : 光标移动到本行行尾  
  *  nG : 转到行号位置  
  G : 转到文件最后一行  
  gg : 转到文件第一行  
  * ctrl + b 将屏幕向文件头方向翻滚一整屏  
  ctrl + f 将屏幕向文件尾方向翻滚一整屏  
* **文本删除**  
在命令模式下：  
dd: 删除当前行  
ndd: 删除从当前行起的n行
x: 删除光标处的字符  
nx: 删除光标位置起的右n个字符  
X : 删除光标前的字符  
nX: 删除光标位置前的左n个字符  
D或 d$: 删除光标起到行尾的内容  
d0: 删除光标前一个字符到行首的内容  
dw: 删除一个单词  
ndw: 删除n个单词  
* **恢复**  
在命令模式下/末行模式：  
u: 取消上一次的编辑动作(可多次)  
U: 取消在本行所有的编辑动作
* **搜索查找**  
末行模式：  
/ ?   
n: 继续向前查找  
N: 与n反向查找  
* **搜索替换**  
s: 用跟随在其后的字符串替换光标位置的字符  
ns: 用跟随在其后的字符串替换光标位置起的n个字符  
S: 用跟随在其后的字符串替换当前行  
nS: 用跟随在其后的字符串替换当前行起的n 行  
/g  全局操作  
:s/vivian /sky /g 替换当前行所有 vivian 为 sky  
:n，$s/vivian /sky /g 替换第 n 行开始到最后一行中每一行所有 vivian 为 sky  
* **行移动**  
  * ndd: 删除第n行  
  p: 被删除的粘贴到目的行  
  *  使用末行模式:  
  :n1,n2 m k  
  将从n1行到n2行的文本移动到k行处,其中m是移动命令
* **拷贝文本**  
  * 命令模式：  
  yy: 拷贝一行(从当前行)  
  nyy: 表示拷贝从光标所在的该行“往下数”n行文字  
  p：粘贴  
  * 末行模式：  
  :1,5 co 20  
  将1到5行拷贝到20行下  
* **文本块快速处理**  
命令模式下输入：  
ctrl+v  
e快速移动下个单词  
$快速移动到行尾  
* **vi中执行shell命令**  
:!command 不离开vi执行一条shell命令  
:r!command 将command执行的结果放到当前行之后  
## 磁盘及文件系统  
* **查询信息**  
  * 磁盘信息    
  fdisk -l  
  lsblk \[-f\] 树形结构，可查看大小和挂载  
  blkid \[设备\] UUID 文件系统类型  
  df \[hT\] 磁盘可用空间 挂载情况  
  du -h 目录或文件占用空间  
  fsck /dev/sdb1 检查并修复磁盘分区上的文件系统  
  * 查看Linux系统信息  
    * 发行版本  
    hostnamectl  
    * 文件系统  
    df -T  
    file -s \[设备文件\]  
* **磁盘分区步骤**  
  * 查询磁盘信息  
  * 为磁盘分区  
  fdisk /dev/sdb 划分新的分区  
  partprobe 重新读取分区信息，而不用重启系统  
  * 格式化分区  
  mkfs.xfs /dev/sdb1 将sdb1格式化为xfs  
  * 挂载分区  
  mount /dev/sdb1  /mnt  将sdb1挂载到mnt  
  mount -t ext4 /dev/sda5/ /mnt/sda 指定/dev/sda5是ext4文件系统并挂载到/mnt/sda目录  
  mount -a 让挂载生效  
  umount /dev/sda5 卸载/dev/sda5  
  * 永久挂载  
  vim /etc/fstab  修改配置文件，可挂载文件也可挂载uuid  
* **swap分区**  
  识别分区：partprobe  
  格式化为swap:mkswap /dev/sdb1  
  启用：swapon  
  查询内存和 swap 容量：free –m  
## 文件权限管理  
* 查看文件详情  
ll  
* r、w、x可以分别用4、2、1的二进制表示  
* **修改文件权限**  
  * 字母设定  
  chmod \[u/g/o/a\] \[+/-/=\] \[r/w/x\] filename  
  chmod g+w /home/mysgared  
  * 数字设定
  chmod 755 fileName #7=4+2+1=>rwx 5=>r-x
* **修改拥有者或所属组**  
chown -R root:grp01 /tmp/src  
修改/tmp/src目录的拥有者为root所属组为grp01，-R递归地遍历目录（对该目录下的也生效）  
* **更改所属组**  
chgrp -R grp01 /tmp/src  
修改/tmp/src目录所属组为grp01  
# 用户和用户组管理  
系统管理员UID为0，系统内建用户UID为1~499，自定义用户UID默认>500  
用户管理相关的文件：  
/etc/passwd 用户的配置文件  
/etc/shadow 用户影子密码文件  
用户组管理相关的文件：
/etc/group  
/etc/gshadow  
* **用户操作**  
  * 添加用户  
  useradd \[选项\] 用户名  
  -u UID  
  -g GID  
  -G 附属组  
  -d 设置主目录  
  -s 设置登陆shell  
  newusers \[选项\] filename 批量添加用户，导入的文件格式必须和/etc/passwd一样  
  * 删除用户  
  userdel -r username 删除用户及其主目录  
  * 设置密码  
  #passwd username root设置用户设置密码  
  #passwd root设置自己密码  
  $passwd 用户设置自己密码  
  echo mypwd | passwd --stdin username 非交互方式修改密码  
  * 修改用户属性  
  usermod –d /home/myusers username  
  * id username  
  查看用户UID，GID及所属用户组  
* **ACL**  
以针对任意指 定的用户/组分配 rwx 权限  
getfacl 获取ACL权限  
setfacl 设置某个文件/目录的ACL权限  
chacl 修改ACL权限  
setfacl -m u:u1:rw /etc/fstab 设置普通用户u1可以读写文件/etc/fstab  
setfacl -m u:alice :--- /home/test.txt  设置普通用户alice不能读写文件  
* **用户组**  
  * groupadd \[选项\] groupname  
  -g 指定组群的gid  
  -f 如果组群存在,退出并显示错误  
  -r 建立系统用户组  
  * groupadd \[选项\] 新名称 旧名称  
  -n 更改组名称  
  -g 更改组GID  
  * groupdel 组名称  
  * gpassword \[选项\] groupname  
  * chmod g+s dirname  
  用户执行操作时临时拥有dirname的所属组权限  
  t:如果文件设置了t权限则只有属主和root才能删除文件   
  i:不可修改权限  
  a:让目标文件只能追加  
## LVM
LVM添加硬盘及扩容  
/dev/myvg/lv01 myvg卷组目录下存放着该卷组的所有逻辑卷  
* **添加硬盘**  
* **创建分区**  
* **分区类型**  
Command (m for help): t  
Hex code (type L to list all codes): 8e  
* **创建PV**  
pvcreate /dev/sdb1  
pvs  
pvdisplay  
* **创建VG**  
vgcreate myvg /dev/sdb1 ...  
vgextend myvg /dev/sdb2 ...  
vgs  
vgdisplay  
* **创建LV**  
lvcreate -L 1G -n lv01 myvg  
lvs  
lvdisplay  
* **使用**  
格式化、挂载  
mkfs.xfs /dev/myvg/lv01  
mount -t xfs /dev/myvg/lv01 /mnt/it  
逻辑卷扩容  
lvextend -L +2G /dev/myvg/lv01  
## 网络配置命令
相关配置文件：  
/etc/sysconfig/network-scripts/ifcfg-ens33 网卡配置文件  
/etc/resolv.conf 设置DNS客户端的文件，指定DNS服务器  
/etc/hosts 保存主机名和IP地址映射的静态文件, 本地DNS解析  
systemctl restart network 重启网络  
* **常用网络命令**  
ip  
ping  
netstat 联网状态  
hostname 主机名  
hostnamectl 主机名及相关系统信息  
* **域名查询**  
nslookup 主机名或ip  
dig 域名（推荐）  
都需要安装命令：yum -y install bind-utils  
* **网卡配置**  
vim /etc/sysconfig/network-scripts/ifcfg-ens33  
常见选项：  
BOOTPROTO=static(静态IP)  
IPADDR0=202.115.195.254  
NETMASK=255.255.255.0  
GATEWAY0=202.115.195.1  
* **DNS配置**  
vim /etc/resolv.conf  
* **nmcli网络管理命令**  
nmcli con 查看网络连接  
nmcli dev 查看设备状态  
  * nmcli con add/modify/del con-name “name” type “type” ifname “ifname” 添加/修改/删除连接  
  为ens33添加新连接并设置ip：  
  nmcli connection add con-name home type ethernet ifname ens33  
  cnmcli con mod home ipv4.addresses 10.0.0.1/24  
  nmcli con up home  
nmcli con modify ens33 +ipv4.address '192.169.92.100/24' 添加或删除ip  
nmcli con modify ens33 +ipv4.dns 10.0.0.10 添加或删除DNS  
nmcli con modify ens33 +ipv4/gateway '192.168.92.1' 添加或删除网关  
