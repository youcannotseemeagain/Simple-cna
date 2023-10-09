# KeepKit插件

插件含8种不同方式的权限维持方式，都是比较容易操作，容易实现的。写的比较粗糙。

## Schtasks

给目标添加一个定时任务

TaskName：计划任务名称

User：运行的用户

pathORcmd：可以运行程序或命令。运行程序需要指定绝对路径，运行命令如有引号"，则需要\来转义。

minute：计划任务运行的间隔分钟数

schtasksName：需要删除的计划任务名

## Service

给目标添加一个自启动系统服务

serviceName：服务名称

command：运行的命令。Windows服务在启动后会给系统一个服务运行正常的返回码，一般的exe没有返回码，这样会导致Windows系统启动后等待30s超时并终止服务启动。也就是说你的shell只有30s，所以最好是运行命令。利用powershell启动后进程会转移到powershell。或许还可以用cmd /k ？？。

## Registry

给目标从注册表添加自启动项，需要手动上传马。

KeyName：键名

FilePath：文件路径

## GuestBk

该选项会启用目标上的guest用户并尝试将其加入管理组

GroupName：管理组名

GuestPass：为guest设置一个密码

## AppInitDLLs

AppInitDLLs注入，该选项会劫持目标上的所有新启动的进程，DLL以新进程名运行。

TargetPath：目标DLL的路径，可以自己上传到一个隐蔽的目录，取一个隐蔽的名字。

删除选项会自动清除存在的注入，但不会清除dll文件。

## CLRHijack

该选项会劫持目标上新运行的.net程序

TargetPath：目标DLL的路径，可以自己上传到一个隐蔽的目录，取一个隐蔽的名字。

删除选项会自动清除存在的劫持，但不会清除dll文件。

## MSDTC

该选项会劫持Windows自带服务Distributed Transaction Coordinator。该服务启动时会加载oci.dll，但系统目录无此文件。

利用前需要手动上传oci.dll到system32目录下，oci.dll不用做，改个名就行。

## ADS

使用..:方式为目标添加一个难以删除且隐蔽性强的ADS流文件，并使用WMIC加载运行。可以将wmic命令创建一个计划任务。

Upload：选择上传的文件，并为其在system32目录下创建一个ADS流

FileName：给定目标系统上的全路径


# QuickWmic

整了几个常用的wmic命令到插件方便执行