# lldb 远程调试iOS程序

# 配置 debugserver
## 1. 导出 debugserver
在一部越狱的iPhone上运行Xcode 项目,运行后 debugserver 会被自动安装到 /Developer/usr/bin 目录.
scp -P 2222 root@localhost:/Developer/usr/bin/debugserver ./
导出debugserver 到电脑上

## 2. 给 debugserver 权限
由于debugserver 缺少 task_for_pid权限,只能调试自己的程序,如若要调试第三方应用就需要添加这个权限,
另外iOS 11 以后运行还需要 platform-application 权限
/usr/bin/codesign -f -s - --entitlements entitlements.plist ./debugserver

## 3. 把 debugserver 放回设备
scp -P 2222 ./debugserver root@localhost:/usr/bin/
为了在iOS系统任何地方都可以使用 debugserver,就放到 /usr/bin 目录下
在设备里给 debugserver 执行的权限
chmod +x /usr/bin/debugserver


# 使用 debugserver
## 1. 手机上启动 debugserver,有两种方式
### 1.1 启动可执行 Mach-O文件,并附加
debugserver -x backboard host:port /path/to/executable
如:
debugserver -x backboard 127.0.0.1:8090 /var/containers/Bundle/Application/24A5D963-2D45-4BA8-BD01-3532C4AD9AAD/TargetForInjectDyld.app/TargetForInjectDyld
### 1.2 附加到目标进程
debugserver host:port --attach=<process_name>
或
debugserver host:port -a [<pid> or <process_name>]
如:
debugserver 127.0.0.1:8090 -a 12316
## 2. 电脑上启动 lldb 连接 debugserver
### 2.1 进行端口转发
iproxy <port> <port>
如:
iproxy 8090 8090
### 2.2 进入 lldb 页面
lldb
### 2.3 连接 debugserver
process connect connect://<host>:<port>
如:
process connect connect://127.0.0.1:8090
