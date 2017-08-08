## 基本命令

```bash
	$ cd / 			## 进入根目录

	$ cd ..         ## 回到上一级

	$ cat 			## 查看文件内容

	$ ls *.cpp      ## 列出所有后缀名为.cpp 文件

	$ ls text?      ## 列出所有以text开头而后跟一个字符的文件

	$ ls text[1A]   ## 列出所有以text开头而仅以1或A结束的文件名

	$ ls text[1-3]

	$ ls text[A-C]

	$ who           ## 有哪些人登录，他们都工作在哪个控制器上

	$ whoami     	## 我是谁

	$ uname         ## 当前系统的版本信息

	$ uname -a      ## 当前系统的版本信息 -a 所有信息

	$ uname -r      ## 当前系统的版本信息 -r 内核信息

	$ whatis uname  ## 满足好奇心

	$ apropos search   ## 反查 

```
## 寻求帮助

```bash
	$ man find 
```

<p class="tip">
	J(向下)<br>
	K(向上)<br>
	space(向下翻一页)<br>
	Q(退出)
</p>

## 查看目录和文件

```bash
	$ pwd 			## 显示当前所在目录

	$ cd .. / ..    ## 回到该子目录的根目录

	$ ls            ## 列出文件和目录

	$ ls -F  		## 目录’/‘，可执行文件'*'，链接文件@

	$ ls -a     	## 显示隐藏文件

	$ ls -l / vdir  ## 查看文件属性

	$ ls -ld  		## 查看目录属性

	$ cat -n        ## 显示行符

	$ more  	 	## 查看文件，一页一页显示

	$ head -n       ## 查看文件开头

	$ tail -n       ## 查看文件结尾

	$ less       	## 没有编辑功能的文本编辑器

	$ grep un day   ## 搜索文件内容 un(关键词) day(文件名)

	$ grep un day weather ## 指定多个文件进行搜索

	$ grep 'struct list' stack.h  ## 搜索有空格的关键词需要加引号

	$ find /usr/bin -name zip -print  ## 路径 名字 打印

	$ locate *.doc  ## 定位所有.doc 后缀的文件

	$ whereis find  ## 查找程序文件并提供这个文件的二进制可执行文件、源代码文件和使用手册存放位置

	$ whereis -b find  ## 只查二进制可执行文件
```
## 建立文件和目录

```bash

	$ mkdir d1 d2        ## 创建一个目录,可并列

	$ mkdir -p ~/tempx/job  ## 创建完整的树结构

	$ touch hello        ## 创建一个空文件/更新文件的创建日期

	$ mv hello bin/      ## 移动（同名文件直接覆盖没有任何警告）

	$ mv -i hello bin/   ## 移动（询问同名是否覆盖）

	$ mv -b hello bin/   ## 移动（自动改名 '~' ）

	$ mv hello ~ hello_bak  ## 重命名

	$ cp test.php bin/   ## 复制（覆盖同名文件）

	$ cp -i test.php bin/  ## 复制（询问同名）

	$ cp -b test.php bin/  ## 复制（自动改名 '~' ）

	$ rmdir              ## 删除目录（只能删除空目录）

	$ rm      			 ## 一次删除一个或几个

	$ rm -i              ## 询问式

	$ rm -f              ## 默认确认删除

	$ rm -r              ## 递归删除

```
## 权限控制

<p class="tip">
	rwxr-xr-x</br>
	rwxr - 属主  xr- 属组   x - 其它人</br>
	r - 可读取</br>
	w - 可写</br>
	x - 可执行</br>
</p>

```bash

	$ chown [OPTION] ... [OWNER][:[GROUP]] FILE

	$ sudo chown lewis:root hello   ## 属主改为Lewis，属组改为root组

	$ sudo chown peter hello        ## 属主改为Peter，属组不变

	$ sudo chown workgroup          ## 属组改为workgroup

	$ sudo chown -R                 ## 递归修改属组/属组

	$ sudo chgrp / -R chgrp         ## 单一修改属组功能

```

<p class="tip">
	u - 文件属主</br>
	g - 文件属组</br>
	o - 其它人</br>
	a - 所有人
</p>

```bash
	$ chmod u+x hello               ## 

	$ chomd a-x hello               ##

	$ chomd ug=rw,o=r hello 	    ##

	$ chomd o-u hello               ##
```

## 文件类型

| 文件类型 | 符号 | 文件类型 | 符号 |
|-------|:------|:-------|:-----|
| 普通文件 | -   | 本地域套接口 | s|
| 目录    |  d  | 有名管道 | p    |
| 字符设备文件 | c | 符号链接 | l  |
| 块设备文件  | b  | 　| 　  |

## 建立链接：ln

```bash
	$ ln -s TARGET LINK_NAME 

	$ ln -s days my_days         ## 建立一个名为 my_days 的符号链接指向文本文件 days（目录也没问题）

	$ ls -l my_days              ## 查看 my_days 的属性

	$ ln days hard_days          ## 硬链接，做映射
```

## 输出/输入重定向

```bash
	$ ls > ~/ls_out       	     ## 把本来应该打印在屏幕上面的内容输出到 ls_out 文件（如果没有，则建立）

	$ ls >> ~/ls_out             ## 同上，不覆盖，而是追加

	$ ls < days                  ## 将文件作为输入传递给 cat 命令，然后输入内容

	$ ls << EOT                  ## EOF、END、eof

	$ cat << END > hello         
```

##  管道

```bash
	$ ls | grep ay               ## 列出目录下所有文件名，管道接收到这些输出，查找出含有ay的文件名
```
##  挂载文件系统

```bash
	$ sudo mount                 ## 挂载

	$ sudo umount                ## 卸载

	$ sudo umount -r             ## 只读方式重新挂载
``` 

##  查看磁盘使用情况

```bash
	$ df                         ## 查看磁盘

	$ df -t ext4                 ## 显示挂载在ext4 文件系统
```

##  检查和修复文件系统

```bash
	$ sudo fsck                  ## 检查

	$ sudo fack -p               ## 根据 fstab 文件来检查文件系统
```

##  建立文件系统

```bash
	$ sudo mkfs -t ext3 /dev/sdb1   ## 将第二块硬盘的第一分区（sdb1）格式化为 ext4

	$ sudo mkfs -t ext4 -c          ## 检查 /dev/adb1
```

##  压缩工具

```bash
	$ gzip linux_book_bak.tar     	    ## 压缩

	$ gunzip linux_book_bak.tar.gz      ## 解压

	$ gzip -l linux_book_bak.tar.gz     ## 解压

	$ gzip -t linux_book_bak.tar.gz     ## 检查完整性
	$ gzip -tv linux_book_bak.tar.gz    ## 如果一定要让压缩说点什么

	$ bzip2 

	$ bunzip2  /  bzip2 -d

	$ bzip2 -t /  bzip2 -tv
```
##  存档工具

```bash
	$ tar -cvf shell.tar shell/         ## 打包shell目录

	$ tar -xvf shell.tar                ## 解压

	$ tar -cvxf shell.tar shell/        ## 询问每个文件是否加入

	$ tar -xvwf shell.tar               ## 询问每个文件是否抽出

	$ tar -czvf shell.tar.gz shell      ## 打包目录然后压缩

	$ tar -xzf shell.tar.gz             ## 先解压再解开

	$ tar -xjf shell.gz                 ## ??? 
```

##  转移文件

```bash
	$ dd if=/dev/cdrom of=CD.iso
```
##  使用 fdisk 建立分区表

```bash
	$ fdisk /dev/sdb
```

| 命令全称 | 缩写形式 | 含义 |
|:-------|:-------|:-----|
| new | n | 创建一个新分区 |
| print | p | 显示当前分区设置 |
| type | t | 设置分区类型 |
| new | n | 把分区表写入硬盘 |

## 用户与用户组基础

```bash
	$ sudo useradd -m john     ## 新建一个用户名为 john 的用户，并自动建立主目录

	$ sudo passwd john         ## 更改 john 的登录密码

	$ sudo useradd -g users mike     ## 新建用户，指定 users 组

	$ sudo groupadd newgroup   ## 新建组

	$ sudo   
```

## 记录用户操作

```bash
	$ history                  ## 用户操作记录

	$ history 10               ## 用户操作记录（前十条）

	$ cd /home/john/ >
	  sudo cat .bash_history   ## 查看记录文件
```

##  删除用户

```bash
	$ sudo userdel mike          ## 删除账号

	$ sudo userdel -r john       ## 删除账户包括所有文件
```




















