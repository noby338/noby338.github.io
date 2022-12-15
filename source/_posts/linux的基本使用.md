---
title: linux的基本使用
date: 2022-12-12 22:30:20
categories: 
- linux
---

* 目录结构

  * 只有一个根目录，/ 表示根目录，其下的目录
    * bin 系统的可执行文件(一般不操作)
    * boot 系统启动相关文件
    * dev 设备文件
    * etc 系统配置文件
    * home 一般用户的根目录(root用户的根目录位于 root)
    * lib 系统的库文件
    * opt 官方建议存放用户软件(也可以放在 /usr/local/scr/)
    * sbin 专供 root 用户使用的目录
* vim(linux 的文件编辑器)

  * 输入 vimtutor 进入 linux 自带的练习
  * 一般模式
    * 编辑模式或底行模式下，按 esc 退出到一般模式
      * 常用命令
        * y数字y(数字yy)：复制行
        * y$：复制光标位置到行末
        * y^：复制光标位置到行首
        * yw：复制当前单词
        * 数字p：粘贴
        * 数字dd：删除行
        * d$：删除光标位置到行末
        * d^：删除光标位置到行首
        * dw：删除单词
        * u：撤销
        * x：删除字符
        * X：退回字符
        * r：字符替换
        * R：依次替换
        * w：移动到下个词首
        * e：移动到下个词尾
        * b：移动到上个词首
        * gg：移动到文件开头
        * G：移动到文件结尾
        * 数字G：移动到指定行(可通过:set nu命令打开行编号，:set nu为关闭行编号)
  * 编辑模式
    * i/a/o/I/A/O 进入编辑模式
  * 底行模式 
    * :q!：退出不保存
    * :wq：退出保存
    * :wq!：强制退出保存只读文件
    * :w：保存
    * :q：退出
    * :set nu：显示行号(:set nonu：取消行号)
    * /单词：查找单词
      * n/N：跳转查找词
    * :s/老单词/新单词：本行第一个单词替换
    * :s/老单词/新单词/g：本行所有单词替换
    * :%s/老单词/新单词：所有行第一个单词替换
    * :%s/老单词/新单词/g：所有行所有单词替换
* 网络配置
  * ![image-20220725102856808](D:/markdown/linux/Image notes/image-20220725102856808.png)
  * 命令：
    * 查看ip：ipconfig(win)、ifconfig(linux)
    * 查看网络连接：ping ip

  * 三种模式：
    * 桥接模式：
      * VMnet0：vm直接连接pc所在的网段

    * NAT模式：
      * VMnet8：上一个网段的ip不能访问下一个网段的ip，为实现pc访问vm，网络设置中的VMnet8是用于将pc虚拟成NAT中的子ip，以实现pc和vm同网段，(若没有VMnet8，vm可以ping pc，但pc 不可以 ping vm)

    * 仅主机模式：
      * VMnet1：类似NAT模式可实现pc和vm的相互访问，vm不能访问外网




* 文件的权限

  * ```
    使用ll 查看，第一列一共是10个字符
    
    例：drwxr-xr-x
    
    第一个字符:类型	d -	l		目录	文件	快键方式链接
    后面的9位和权限相关,三位是一组，代表一组用户的三种不同权限
    	
    	第一组三位:	属主权限	文件的所有者			rwx	read write execute
    	第二组三位:	属组权限	和文件所有者同一个组的用户拥有的权限
    	第三组三位:	其它用户权限 
    	
    	
    chmod	
    
    chmod u=rwx,g=rwx,o=rwx a.txt 修改文件 a.txt 的权限
    
    权限		  rwx	rwx
    二进制      111   101
    十进制		 7     5
    
    chomd 777 a.txt 第二种修改方法，同以上作用
    ```

* linux 命令

  * ```
    ifconfig 查看 IP(centos 最小版，没有网络工具包)
    ip addr	查看 IP(centos 最小版可用)
    ping ip 查看网络是否相通
    curl url 查看网络是否能够访问
    pwd 查看当前目录路径
    ls 查看当前目录的下的目录
    ls noby 查看 noby 目录的下的目录
    ls -l 查看当前目录的下的目录的详细信息(简写为 ll)
    ls -l 查看当前目录的下的隐藏目录的详细信息
    cd / 退回到根目录
    cd ../ 退回到上级目录(cd /usr/local/src 表示进入根目录下的路径，cd local/src 表示进入当前目录下的路径)
    cd ~ 进入该用户的根目录(root 用户的根目录为 /root，非 root 用户的根目录为 /home/用户名)
    cd - 退回上次记录径路
    clear 清屏
    history 查看历史命令 !数字 执行历史命令
    history -c 清除历史
    mkdir a 创建目录a
    mkdir -p a/b/c 一次性创建多层目录
    find /noby -name 'a*' 查找 noby 目录下的名称为 a 开头的文件或文件夹
    mv b bb 将当前目录文件或文件夹 b 重复名为 bb (当前路径必须为被修改文件的上一级目录)
    mv d /noby/b 将当前目录文件 d 剪切到绝对路径 /noby/b
    mv -r d /noby/b 将当前目录文件夹 d 剪切到绝对路径 /noby/b (-r 表示递归，因为目录下还有目录)
    rm -rf e 删除当前目录的 e 文件夹(-rf 表示所有目录，如果使用 -r 将会逐级询问)
    touch file.txt 创建文件 file.txt 到当前目录
    find / -name <file> 根据文件名查找文件
    
    cat		查看文件内容，全部展示
    more	查看文件内容，空格翻页
    less	查看文件内容，pageup pagedown 退出q
    tail    查看文件内容，tail -n	文件，查看最后n行，tail -f 查看系统文件，监控日志文件
    
    
    tar -zcvf b.tar.gz  b/* 	将 b 目录下的所有文件压缩打包(文件名中 gz 表示压缩，tar 表示打包)
    	z	启用压缩(可以不压缩)
    	c	打包
    	v   显示详细信息
    	f	指定文件名
    	
    tar -xvf b.tar.gz	解压到当前目录	（解压的文件，必须使用启用了压缩格式才能使用）
    tar -xvf b.tar.gz -C /noby 解压到指定目录 noby
    
    ps -ef | grep -i vim 查看包含 vim 的进程
    	| grep 表示管道命令(筛选条件)
    	-i 表示忽略大小写
    rpm -qa | grep vim	查看包含 vim 的安装程序
    		
    kill -pid	杀死进程
    
    netstat -anp	查看端口占用
    
    systemctl status 服务名 查看服务状态
    systemctl enable 服务名 设置服务开机自启
    systemctl list-unit-files | grep enabled 查看自启服务
    systemctl disable 服务名 取消开机自启
    systemctl start 服务名 开启服务
    systemctl stop 服务名 关闭服务
    systemctl restart 服务名 重启服务
    
    
    firewall-cmd --zone=public --add-port=8080/tcp --permanent （–permanent永久生效，没有此参数重启后失效）添加开放端口
    firewall-cmd --reload 重新载入--重启防火墙
    firewall-cmd --zone=public --query-port=8080/tcp 查看端口
    firewall-cmd --zone=public --remove-port=6379/tcp --permanent 删除端口
    ```

* linux 中的快捷键

* ```
  Ctrl L ：清屏
  Ctrl C : 中断正在当前正在执行的程序
  Ctrl R，再按历史命令中出现过的字符串：按字符串寻找历史命令(继续Ctrl R 切换匹配项)
  Tab : 自动补齐
  Ctrl PageUp : 屏幕输出向上翻页
  Ctrl PageDown : 屏幕输出向下翻页
  Ctrl Z : 把当前进程放到后台（之后可用''fg''命令回到前台）
  Ctrl w : 删除词
  ```

  

  ​	

* 程序的安装

  * 安装命令

    * ```
      rpm命令:
      通过本地已存在的安装包安装
      本地程序安装: rpm -ivh 程序名。
      本地程序查看: rpm -qa
      本地程序卸载: rpm -e --nodeps 程序名。
      
      yum命令:	
      相当于可以联网的rpm命令：自动搜索安装包，自动安装。自动下载当前安装包的依赖包
      相当于先联网下载程序安装包、程序的更新包
      自动执行rpm命令。
      
      ```


* linux

  * linux 版本
    * 内核版
    * 发行版
      * ubuntu
      * Red Hat
      * CentOS
        * 通过 VMware 安装在 application centos 文件夹

* VMware

  * 用于 window 安装其他系统的虚拟机
  * 快照：
    * 用于备份系统

* 安装步骤

  * VMWare装好以后，系统会多两块虚拟网卡
    VMnet1	直接禁用
    VMnet8	这个是给NAT模式时

  * 进入BISO，启用主板的虚拟化设置

  * ![image-20220621144721757](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/libaisong/20220621144721.png)

    ![image-20220621144800290](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/libaisong/20220621144800.png)

    ![image-20220621144826896](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/libaisong/20220621144826.png)

    ![image-20220621144849683](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/libaisong/20220621144849.png)

    ![image-20220621144938688](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/libaisong/20220621144938.png)

    ![image-20220621145105656](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/libaisong/20220621145105.png)

    ![image-20220621145255893](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/libaisong/20220621145255.png)

    ![image-20220621145323729](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/libaisong/20220621145323.png)

    ![image-20220621145540140](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/libaisong/20220621145540.png)

    ![image-20220621145621885](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/libaisong/20220621145621.png)

    ![image-20220621145724138](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/libaisong/20220621145724.png)

    ![image-20220621151324911](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/libaisong/20220621151324.png)

    ![image-20220621151524655](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/libaisong/20220621151524.png)

    ![image-20220621151731946](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/libaisong/20220621151732.png)

    ![image-20220621151918035](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/libaisong/20220621151918.png)

    ![image-20220621151835006](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/libaisong/20220621151835.png)

    ![image-20220621152037890](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/libaisong/20220621152038.png)

 
