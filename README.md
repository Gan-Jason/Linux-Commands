## 命令的基本格式  

* [root@localhost~]
* root为用户名
* ～表示当前所在位置
* localhost主机名
* '#'超级用户
* '$' 普通用户  

**命令基本格式：命令 [选项] [参数]**  

## 查看Linux发行版本  
* cat /etc/os-release
* 查看Linux版本：uname -r
* 查看Linux版本全部信息：uname -a


## 查询目录的内容  
**命令格式：ls [选项] [文件或者目录]**  
* 选项：
  * -a 所有文件
  * -l 查看详情
  * -d查看目录属性
  * -h显示文件大小

## 文件处理命令  
### 建立目录  
* mkdir -p [目录名],(注：-p表述递归建文件夹)  
### 切换目录
* cd [目录]  
* cd ~ 进入当前用户目录
* cd - 上次目录
* cd .. 进入上一级目录
* pwd 查看当前目录所在位置  
### 删除目录  
* rmdir [目录] 
### 删除目录下所有文件 
* rm -rf [目录]  
### 复制目录  
* cp[选项][原文件目录][目标目录]
* 选项：
  * -r复制目录
  * -p连文件属性一起复制
  * -a 相当于-pdr  
### 剪切、改名  
* mv[原文件目录][目标文件目录]
### 常见目录的含义  
* / 根目录
* /bin 命令保存目录
* /boot 启动目录
* /dev 设备文件命令
* /etc 配置文件保存目录
* /home 家目录
* /lib 系统库保存命令
* /mnt 系统挂载目录  
## 文件搜索命令  
* locate [文件名]  
### 命令搜索  
* which [选项][命令名]
* 选项：
  * -b 只查找可执行文件
  * -m 只查找帮助文件  
### 文件搜索  
* find [搜索范围][选项][条件]  
* 举例子：   
  * 在根目录下查找名为install.log文件:find  /  -name install.log  
  * 忽略大小写查找文件:find /root  -inname install.log
  * find /var/log -mtime +10
    其中-mtime 文件修改时间
    -atime 文件访问时间
    -ctime 改变文件属性时间
    +10 10天前
    10  10天
    -10 10天内
  * 查找文件大于20M的文件:find /etc -size +20M  
## 压缩与解压缩命令  
* 常见压缩格式：(.zip),(.gz),(.bz2),(.tar.gz),(.tar.bz2)  
### zip格式  
* 压缩文件：zip [压缩文件名][原文件]  
* 压缩目录：zip -r  [压缩文件名][原文件]  
* 举例子：  
  * touch jp/cangls
  * touch jp/longls
  * zip -r jp.zip jp  
* 解压：unzip [压缩文件名]  
### gz格式  
* 压缩为.gz格式，源文件不保留：gzip [文件名]  
* 压缩为.gz格式，源文件保留：gzip -c [原文件] > [压缩文件]  
* 压缩目录：gzip -r  [目录]  
* 直接解压：guzip [文件]  
* 解压为目录：guzip -r [目录]  
### tar格式  
* 压缩：tar -cvf [打包文件名] [原文件]  
* 解压：tar -xvf [文件名]  
### tar.gz格式  
* 压缩：tar -zcvf [打包文件名] [原文件]  
* 解压：tar -zxvf  [压缩包名.tar.gz] 
## 关机和重启  
### 关机  
* shutdown [选项][时间]

* 选项：
  *  -c 取消前一个关机命令
  *  -h 关机
  *  -r 重启  
* 重启：init 6  
* 关机：init 0  
* 退出登陆：logout  
## 查看用户信息  
* w  
* who  
* last  
* lastlog
* 都敲一遍就知道是什么格式的命令了  
## shell基础  
* shell是命令行解释器，逻辑上是一层壳，是用户与操作系统内核进行交互的接口。  
* 输出：echo[选项][输出内容]  
* 选项：
  * -e:支持转义  
### 创建一个sh脚本  
```
# 进入编辑(如果文件不存在，则新建文件并进入编辑该文件)：
vim hello.sh

#!/bin/bash
# the first program

echo "hello world!" 
```  
### 执行脚本  
```
chmod 755 hello.sh

./hello.sh
```
* 或者  
```
bash hello.sh
```
* 
### 时间  
* 查看系统时间：date  
* 查看硬件时间：hwclock  


## 进程
### 查进程
* ps命令查找与进程相关的PID号：
* ps a 显示现行终端机下的所有程序，包括其他用户的程序。
* ps -A 显示所有程序。
* ps c 列出程序时，显示每个程序真正的指令名称，而不包含路径，参数或常驻服务的标示。
* ps -e 此参数的效果和指定"A"参数相同。
* ps e 列出程序时，显示每个程序所使用的环境变量。
* ps f 用ASCII字符显示树状结构，表达程序间的相互关系。
* ps -H 显示树状结构，表示程序间的相互关系。
* ps -N 显示所有的程序，除了执行ps指令终端机下的程序之外。
* ps s 采用程序信号的格式显示程序状况。
* ps S 列出程序时，包括已中断的子程序资料。
* ps -t<终端机编号> 指定终端机编号，并列出属于该终端机的程序的状况。
* ps u 以用户为主的格式来显示程序状况。
* ps x 显示所有程序，不以终端机来区分。
**最常用的方法是ps aux,然后再通过管道使用grep命令过滤查找特定的进程,然后再对特定的进程进行操作。
    ps aux | grep program_filter_word,ps -ef |grep tomcat**  
    
**ps -ef|grep java|grep -v grep 显示出所有的java进程，去处掉当前的grep进程。**
### 杀进程  
* 使用kill命令结束进程：kill xxx
* 常用：kill －9 324
* Linux下还提供了一个killall命令，可以直接使用进程的名字而不是进程标识号，例如：# killall -9 NAME







