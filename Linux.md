# notes
some notes for Linux


## 一些热键
Ctrl+C 退出前台执行程序  
Ctrl+D 离当前shell  
Ctrl+L 清屏  
Tab:按一次 命令后自动补全  
Tab:按两次列出以输入开头的所有命令  
## 常用命令  
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
* **统计文件行数、字数和字符数 **  
wc filename   
* **查看文件**  
file filename 查看文件详细信息  
head filename  
tail filename  
tail -f filename 循环显示最新添加内容  
