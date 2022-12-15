---
title: cmd
date: 2022-12-12 22:24:08
categories: 
- windows
---

## bat 脚本

```bat
::Windows 系统命令行默认使用 GBK 编码（编号: 936），如果需要显示中文，编写的脚本可以使用 ANSI 或 GB2312 编码。
::第二个方法是文件头加上 chcp 65001，让终端显示为utf8编码

::echo off关闭该文件中命令回显，@关闭echo off命令的回显
@echo off
::设置命令行窗口的标题
TITLE nobytest
::当前文件，以及当前文件路径
echo Current script is: %0,Current script path is: %~dp0
::运行程序时输入的第一个参数，和第二个参数
echo First param is: %1,Second param is: %2
::if
if 1==1 (echo ok) else (echo fail)
::设置变量
set name=noby
::控制台输入参数
@REM set /p age=please input age for %name%:
::涉及计算时
set /a calculate=(1+2)*3
set /a sum=0
::for循环(起始值，累加，条件)
for /l %%i in (0,1,5) do (
    set /a sum=sum+%%i
)
::跳转的标签
:again
::跳转到again
@REM goto :again
::跳转到结尾
@REM goto :eof
::一些系统变量
echo random=%random%,time=%time%,date=%date%,JAVA_HOME=%JAVA_HOME%
::暂停执行
@REM pause
::输出空行
echo.
echo The name is %name%,The age is %age%,The calculate is %calculate%,The sum is %sum%
::打开其他软件
@REM start D:\application(GREEN)\SpaceSniffer.exe
@REM start C:\WINDOWS\System32\SndVol.exe
::调用其他 bat ，call 后填写路径
@REM call otherbat
::taskkill /f /t /im 进程名称
::                        /f 杀死所有进程及子进程
::                        /t 强制杀死
::                        /im 用镜像名称作为进程信息   
::                        /pid 用进程id作为进程信息
tasklist | findstr "uTools.exe"
if %errorlevel%==0 ( 
	echo "yes"
    taskkill /f /im "uTools.exe" /t
) else (
	echo "No" 
    start C:\Users\13269\AppData\Local\Programs\utools\uTools.exe
)

echo 运行成功，按任意键退出 && pause > nul

mshta vbscript:msgbox("内容",0,"标题")(window.close)



```

## cmd 常用命令

```bat
rem 管道命令查看进程
tasklist | findstr msedge
rem 结束所有的edge.exe进程
taskkill /f /im msedge.exe

rem 启用管理员账户
net user administrator /active:yes
```

## schtasks 函数

```bat
rem 查找任务名为noby的任务
SCHTASKS /Query /TN notepad
schtasks /query | findstr note*

rem 创建一个名字叫notepad的计划任务，每天从8点50开始，每隔2小时执行notepad.exe文件
SCHTASKS /Create /TN notepad /TR c:\windows\system32\notepad.exe /ST 08:50 /SC HOURLY /MO 2

schtasks /create /tn "SHUTDOWN" /tr "shutdown /s"  /sc once /st 22:30
schtasks /create /tn NobyAlert /tr "mshta vbscript:msgbox('schtask',0,'test')(window.close)" /st 20:47 /sc once

rem 删除任务
SCHTASKS /Delete /TN notepad





```

## 符号变量

```bat
mklink /r "C:\Program Files (x86)\Microsoft" D:\Application\Microsoft
mklink /r "C:\Program Files\Microsoft Office\root\Office16" D:\Application\Office16
```



## 常用系统变量

| 变量名              | 变量值(默认值)                         | 变量描述                                                     |
| ------------------- | -------------------------------------- | ------------------------------------------------------------ |
| %UserName%          | Administrator                          | 用户名                                                       |
| %HomePath%          | \Users\Administrator                   | 用户主路径（此变量有时会替代%UserProfile%来定位到用户目录）  |
| %UserProfile%       | C:\Users\Administrator                 | 用户配置路径                                                 |
| %LocalAppData%      | C:\Users\UserFolder\AppData\Local      | 应用程序用户本地数据存储目录（如Chrome谷歌浏览器插件）       |
| %AppData%           | C:\Users\UserFolder\AppData\Roaming    | 应用程序配置及缓存存储目录（如Chrome谷歌浏览器保存的网站信息） |
| %HomePath%          | \Users\UserFolder                      | 用户目录路径                                                 |
| %SystemDrive%       | C:\                                    |                                                              |
| %ProgramFiles%      | C:\Program Files                       |                                                              |
| %ProgramFiles(x86)% | C:\Program Files (x86)                 |                                                              |
| %AllUsersProfile%   | C:\ProgramData                         |                                                              |
| %SystemRoot%        | C:\Windows                             |                                                              |
| %WinDir%            | C:\Windows                             |                                                              |
| %DriverData%        | C:\Windows\System32\Drivers\DriverData |                                                              |

