Linux基础命令

ls 查看当前目录

ls -l 查看当前目录下的详细信息

ls -a 查看当前目录下的所有文件

ls -la 查看当前目录下所有文件的详细信息

ls ../ 查看上一级目录

ls / 查看根目录下面的所有内容

ll 就是ls -l的缩写

pwd 查看当前目录 docher

~ 代表家目录

cd 进入某个目录

clear 清空当前可视窗口

exit 退出当前用户

su 切换到管理员(使用完之后应该立即退出)

su bigc 切换到bigc用户

shutdown -h 10 十分钟之后关机

shutdown -r 10 十分钟之后重启

shutdown -k 10 十分钟之后有动作

shutdown -c 结束其他用户的关机重启命令

ctrl+c 结束当前窗口进程,也可以终止关机,重启命令

ctrl+alt+(F2-F6)进入单窗口模式

ctrl+alt+F1 退出窗口模式

halt 立即关机 普通用户也有权限

reboot 立即重启 普通用户也有权限

grep size 文件名 文本查找工具,可也查找文件里面的信息

ls -a | grep s 搜索所有带s的文件名

vim 文件名 可以打开vim工具进行编辑

tail -n 3 文件 查看文件最后三行

head -n 3 文件 查看文件前三行

man 命令名称 查看命令参数注释以及详细介绍

命令 –h 命令的简略信息

passwd 用户名 给用户设置密码

passwd -S 用户名 查看密码状态

passwd -l 用户名 锁定用户

passwd -u 用户名 解锁用户

passwd -d 用户名 删除密码(删除密码之后记得锁定用户)

禁止所有普通用户登录

1,在/etc下创建一个nologin文件
2,使用vim打开这个文件vim /etc/nologin
3,保存退出即可
4,删除这个文件即可还原rm -rf /etc/nologin

vim有三种模式

普通模式:就是打开文件的默认模式,可以进行光标的移动和复制

x:删除光标所在当前单个字符
yy:复制 2yy:复制当前行到下一行
yw:复制一个单词
p:粘贴
dd:删除 3dd:删除当前行到下两行
u:还原
h:向左移动
l:向右移动
j:向下移动
k:向上移动
gg:移动到文件头
G:移动到文件末尾
10gg:以顶部为起点向下移动十行
/size:所有size
n:向下查找
N:向上查找

插入模式:就是把文本内容进行更新,或者新加内容

命令模式:可以实现普通模式的所有功能,并且还能完成高难度的操作

输入:可以进入命令模式
1copy 3:把第一行复制到第三行下面
1co 2:把第一行复制到第二行下面
1,3move 4:把第一行到第三行之间的数据移动到第四行下面
7,8m 1:把第七行和第八行移动到第一行的下面
set nu:显示行号
set nonu:取消行号
5,13d:删除第五行到第十三行的数据
w:保存
q:退出
w!:强制保存
q!:强制退出
wq!:强制保存退出
set hls:显示高亮
set nohls:取消高亮

vim +/size (文件名) 打开并且直接进入搜索模式

vim (文本文件) (文本文件) 打开多个文件

next:查看下一个文件
prev:查看上一个文件
last:查看左后一个文件
first:查看第一个文件

修复崩溃文件

1,打开文件 vim -r 文件名
2,回车,确定内容,然后保存退出
3,删除交换文件 rm -rf [.文件名.swp]

Linux快捷键

[ESC]+[.] 把上一条命令的最后一个参数,拿到当前命令行

[!]+一个字符 搜索最近的一次相匹配的命令

[ctrl]+a 光标移动到命令行的最前面

[ctrl]+e 光标移动到命令行的最后面

Linux软件安装与卸载

/media/ 光盘所在目录

rpm -qa 查询所有的安装程序

wc -l 统计文本内容的行数

rpm -qa | wc -l 统计系统安装程序的总数量

rpm -qa | grep vim 在安装的软件里寻找vim软件包

rpm -e 软件名 卸载

rpm -ivh 路径+安装包名 安装

-i安装 -v显示安装过程 -h以#号的方式显示安装过程

rpm -qp –requires 安装包名 查询安装包的依赖关系

rpm -q –requires 软件名 查询安装包的依赖关系

rpm -qpl 路径+安装包名 安装的程序在哪里

rpm -ql 软件名 查询安装目录文件在哪里

rpm -qpi 路径+安装包名 查看安装包的简要信息

rpm -qi 软件名 查看软件的简要信息

rpm -qpd 路径+安装包名 查看安装包的帮助信息

rpm -qd 软件名 查看软件的帮助信息

–nodeps 忽略依赖

Linux组的相关命令

groupadd -g [组编号] 组名 创建一个组

groupmod -n 新名称 旧名称 修改组名

groupmod -g 新编号 组名 修改编号

groupdel 组名 删除组

gpasswd -a 用户名 附属组名 添加一个附属组

gpasswd -d 用户名 负数组名 删除一个附属组

Linux用户相关命令

useradd 用户名 添加用户(会自动创建一个与用户名相同的组)

usermod -c ‘注释’ 用户名 修改注释

usermod -l 新用户名 就用户名 修改用户名

usermod -u 新编号 用户名 修改编号

userdel -r 用户名 删除用户

Linux修改文件权限

chmod 777 a.html

r:读 w:写 x:执行 | u:属主 g:数组 o:其他 a:全部 | +:增加 -:减少

例如 chmod u-w a.html
chmod o+x a.html

-R 递归修改

chown 修改属主

chown:/chgrp 修改数组

同时修改属主和属组 chown bigc:bigc a.html

Linux目录操作

mkdir 文件名 创建目录

mkdir -p 文件名/文件名 递归创建

mkdir -m 777 abc 创建目录的时候指定权限

rmdir -p abc/ab/a 递归删除

touch text.txt 创建文件

rm text.txt 删除文件

rm -f text.txt 强制删除文件

rm -r abc 删除目录(需要进入文件才能删除)

rm -rf abc 强制删除目录

cp 复制的文件 复制到哪里 复制文件

cp text.txt php/ 复制文件到php文件下

cp text.txt php/aaa.txt 复制到php文件下并且改名

cp -R php java/ 复制php目录到java下(会修改属主和数组)

cp -p php java/ 复制php目录到java下(不会修改属主和数组)

mv a.html html/ 文件移动(移动的时候可以进行改名)

mv a.html b.html 文件重命名

wc -l:统计行数 -c:统计字符 -w:统计单词

grep div a.html 搜索

grep -n div a.html 搜索结果显示行号

grep -c div a.html 统计搜索次数(一行只算一次)

grep -i div a.html 搜索结果不区分大小

cat 打印文件内容到屏幕

tac 倒着打印内容到屏幕上

Linux软连接

ln 文件路径 /usr/bin/mysql 创建硬连接

ln -s 文件路径 /usr/bin/mysql 创建软连接
SET PASSWORD FOR ‘root’@’localhost’ = PASSWORD(‘新密码’);

在丢失root密码的时候，可以以安全模式进入进行修改密码
mysqld_safe –skip-grant-tables&
mysql -u root mysql
UPDATE user SET password=PASSWORD(“new password”) WHERE user=’root’;
FLUSH PRIVILEGES;

Linux文件查找

find 搜索的目录 搜索的选项参数 搜索的值

选项参数:

-name 文件名 可以使用*进行模糊搜索的

-group 属组

-user 属主

Linux显示磁盘信息

df [-h] [-T] 查看磁盘还有多少可用空间 设备的真实路径/硬盘的块/使用的量/空闲的量/使用的百分比/挂载点

-h 以1024的进制来显示空间大小

-H 以1000的进制来显示空间大小

-T 显示系统的文件类型

-t [文件类型] 显示指定文件类型的信息

-x [文件类型] 不显示指定文件类型的信息

du [-sh] 默认查看当前目录下的文件

-b 以B为单位来显示文件大小

-k(默认) 以k为单位来显示文件大小

-m 以m为单位来显示文件大小

-h 根据文件大小,自动转换单位

-s 显示当前目录的总大小