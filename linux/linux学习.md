# linux学习

## 1.linux目录结构

1.1.linux只有一个根目录 “/”

1.2层级式子目录

​	/bin->usr/bin:系统的可执行文件，可以在任何目录下执行

​	usr/local/bin:用户自己的可执行文件，可以在任何目录下执行

​	etc：存放配置文件，配置环境变量（/etc/profile）

​	home:每一个用户的根目录，用来保存用户私人数据，默认情况下，目录名和自己的用户名相同

​	opt：存档额外安装的软件。相当于windows系统中的program files

1.3linux远程操作：

​	1.3.1.Xshell:linux的终端模拟软件

​		连接远程linux系统，创建会话，

​		查看linux的ip地址：ifconfig

​	1.3.2.Xftp:传输文件

## 2.命令

### 	2.1磁盘管理

​		tmp系统存临时文件

​		ll列出文件时，

​		-表示文件

​		d表示文件夹

​		l表示快捷方式		

| 动作         | 命令    |      |
| ------------ | ------- | ---- |
| 列出目录     | ls      |      |
| 观察详细信息 | ll      |      |
|              | cd      |      |
| 回到上一级   | cd ..   |      |
| 切换用户     | su 用户 |      |
|              |         |      |
|              |         |      |
|              |         |      |

### 	2.2文件管理

home是自己的家；其他的不要乱动

| 动作                   | 命令                           |
| ---------------------- | ------------------------------ |
| 创建文件夹             | mkdir 文件名                   |
| 删除                   | rm                             |
| echo "abc" > abc.txt   | 将abc字符串放到abc.txt中       |
| cat 文件夹             | 查看                           |
| rm abc.txt             | 删除当前文件                   |
| rm -f abc.txt          | 不询问直接删除（f不确认 ）     |
| rm -rf test01          | 删除目录（r代表递归删除）      |
| cp aaa.txt bbb.txt     | 复制aaa.txt文件到bbb.txt文件中 |
| cp -rf 文件夹 新文件夹 | 复制目录到新目录               |
| more aaa.txt           | 分页显示内容                   |
| head -n 数字           | 查看n行数                      |
|                        |                                |

| 动作                    | 命令                             |
| ----------------------- | -------------------------------- |
| grep java  ccc.txt      | 在ccc.txt 搜索java               |
| grep java               |                                  |
| grep “java is” aa.txt   | 在aa.txt搜java                   |
| grep -w java aa.txt     | 搜索这个单词                     |
| cat aa.txt \| grep java | 读取aa.txt详细信息，然后搜索java |

### 2.3系统设置

| 命令            | 动作         |
| --------------- | ------------ |
| reboot          | 重启         |
| shutdown -h now | 关机         |
| ps -ef          | 看进程       |
| kill pid        | 杀掉进程     |
| kill -9 pid     | 强制杀掉进程 |
|                 |              |

​	-e:显示当前所有进程

​	-f:显示UID，PPID，C与STIME栏位信息

​	UID：改程序的用户

​	PPID：父进程

​	C：cpu所占资源

​	

### 2.4解压缩

参数说明：

z:使用压缩

c:创建压缩文件

v:显示压缩，解压过程中处理的文件名

f:指定归档文件名，tar参数后面是归档文件名

x:归档文件中释放文件，就是解压

t:列出归档文件内容，查看文件内容



| 命令                                | 动作               |
| ----------------------------------- | ------------------ |
| tar -zcvf 归档文件名 要归档文件列表 | 压缩(归档)         |
| tar -zxvf                           | 解压               |
| tar -tf 压缩文件                    | 列出压缩文件的内容 |

### 	2.5网络通讯

| 命令     | 动作         |
| -------- | ------------ |
| ifconfig | 看IP地址     |
| ping     | 查看         |
| wget url | 指定网址下载 |

### 	2.6网络访问

### 	2.7权限管理

-rwxr-xr-x

| 字符 | 动作                              |
| ---- | --------------------------------- |
| -    | 文件类型                          |
| rwx  | r(读)，w(写)，x(执行) rwx(拥有者) |
| r-x  | r-x(所属用户组)                   |
| r-x  | r-x(其他)                         |

r-read 读权限 4

w-write 写权限 2

x-execute 执行权限 1



> 权限更改：

u:表示文件或目录的属主

g:表示同组其他成员

o:表示其他用户

a:表示所有用户



改变：

+：增加

-：取消

=：修改成后续值

1.执行

2.写

3 1+2 写，执行

4 读

5 1+4 执行+读

6 2+4 写+读

7 1+2+4 读+写+执行



常见权限：

rwx = 4+2+1 =7

644 、755、777

创建文件用户就是文件的拥有者，用户所在的组就是文件所在组。除创建文件的用户都是其他用户，root有最高权限



chmod:修改权限

语法：chmod 606 aa.txt



chown:修改文件拥有者

chown galahad aa.txt



### 	2.8管道和重定向

重定向输出覆盖：

">":可以覆盖原有的

">>":原有的基础上追加



管道：

echo "aaa" >> abc.txt|grep a in abc.txt

### 	2.9vi/vim命令

> 启动：

vi 文件

> 操作

命令模式：按esc键，进入命令模式，命令模式无法编辑

编辑模式：按a或者i字母键，进入编辑模式（此时底部出现insert）。命令模式下按:wq（冒号键w键q键）保存退出，按:q!不保存退出

从命令模式进入编辑模式按a或者i字母键

从编辑模式键入命令模式按esc键



> 命令

1.dd

2.yy

3.gg

4.GG



:w	可以保存但不退出

​	



shift+insert粘贴

tab补全代码

上下箭头访问历史命令



## 3.下载jdk

1.用xftp传输，记得要把那个文件给用户

**sudo chown -R username:username 文件夹路径**

解压：

tar -zxvf jdk-8u361-linux-x64.tar.gz -C /usr/local/

2.在etc的profile文件末尾加上

```
export JAVA_HOME=/usr/local/jdk1.8.0_361
export PATH=$JAVA_HOME/bin:$PATH
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JAVA_HOME/jre/lib/rt.jar
```

3.修改完成

执行source /etc/profile 让配置生效



## 4.启动tomcat

按上面的之后在bin里 ./startup.sh

可以logs/catalina.out中查看日志



## 5.安装mysql

照常，下载解压

卸载mariadb

yum list installed | grep mariadb



修改名字

```
mv mysql-5.7.36-linux-glibc2.12-x86_64 mysql-5.7.36
```

之后照常

> 搭建mysql

1.在mysql目录下创建data文件

```
mkdir data
```

2.增加用户 

```
useradd mysql
```

3.之后进入bin进行初始化

```
mysqld --initialize --user=mysql --basedir=/usr/local/mysql --datadir=/usr/local/mysql/data 
```

4.执行加密

./mysql_ssl_rsa_setup --datadir=/usr/local/mysql/data

5.修改mysql权限

chown -R mysql:mysql /usr/local/mysql/

6.安全启动mysql

./mysqld_safe & 



7.查看进程

ps -ef | grep mysql



8.进入mysql客户端

./mysql -uroot -p

SynxjwL8vg&4



9.进入mysql

alter user 'root'@'localhost' identified by 'root'；

> tips

MySQL问题：
-bash: ./mysqld: 没有那个文件或目录

mysql安装路径：/usr/local/mysql/bin

vi /etc/profile
添加环境变量：
 export PATH=$PATH:/usr/local/mysql/bin
重启环境变量
再使用命令
mysqld --initialize --user=mysql --basedir=/usr/local/mysql --datadir=/usr/local/mysql/data 



## 6.用户管理

普通用户由root管理，由root创建普通用户



更改密码

sudo passwd root *#回车*

```
1. [sudo] password for kerwin: #输入当前用户密码
2. New password: #输入root新密码
3. Retype new password: #再次输入root密码
4. passwd: password updated successfully #密码更新成功
```





1.

> 添加用户：useradd 用户名

​	1.1useradd lisi

​		1->创建一个用户lisi

​		1->/home目录下创建用的根目录，目录名与用户名相同

​		1->在linux中任何一个用户都至少属于一个组，新建用户时如不指定组，会新建一个组，组名和用户名相同，并且将用户添加到该组

​	1.2useradd -d /home/ww wangwu 创建用户时，指定用户根目录

 2.

> 给用户设置密码：passwd 用户名

​	passwd lisi

3.

> 删除用户：userdel 用户名

​	userdel lisi

​	userdel -r lisi 删除用户同时级联删除它的主目录

4.

> 查看用户信息：id 用户名

​	id zhangsan

uid=1002(lisi) gid=1002(lisi) 组=1002(lisi)

每个用户都有个主组

5.

> 切换用户

su 用户名





6.

组管理：

​	1.linux的组相当于角色的概念，可以对有共性的用户进行统一管理；

​		每一个用户至少属于一个组，不能独立于组存在0

​	2.添加组：groupadd 组名

​		groupadd dev

​	3.删除组：groupdel 组名

​		

​	4.把用户添加到组中：gpasswd -a 用户名 组名

​		gpasswd -a zhangsan dev

​	5.把用户从组中移除：gpasswd -d 用户名 组名

​		gpasswd -d zhangsan dev

​	6.创建用户时，指定所属的组（主组）：useradd -g 组名 用户名

​		useradd -g dev lisi



## 7.帮助命令

​	1.查看linux系统手册上的帮助信息：man命令

​		man ls

​		分屏显示、回车翻一行，空格翻一页，

​	2.查看命名的内置信息：help



## 8.文件和目录操作命令

​	1.查看当前所在目录：pwd

​		pwd

​	2.查看指定目录下所有子目录或文件列表：ls [指定目录]

​		ls /home

​		ls

​		ls -l /home ：以列表显示

​		ls -a /home ：展示指定目录下所有子目录和文件（包括虚拟的目录）

​		ls -al /home :以列表显示

​	3.cd 切换目录

​		绝对目录：盘符开头

​			cd  /opt/test

​			cd ~直接进入当前用户根目录

​		相对目录：以目录名开始的目录

9.网络配置

10.进程管理

查看进程ps

ps-e显示所有进程

ps -ef //以全各式形式显示所有进程

ps -ef|grep fire //查询

​	
