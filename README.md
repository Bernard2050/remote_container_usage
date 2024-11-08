## 说明
远程lxd容器cpu环境ubuntu_xfce_xrdp_matlab
默认普通用户名：newuser
默认密码：666666

## 通过 SSH 使用公钥和私钥访问

生成 SSH 密钥对
```shell
ssh-keygen -t rsa -b 4096 -C "<此处为注释>"
```
在 ~/.ssh/ 目录下生成一个公钥 (id_rsa.pub) 和私钥 (id_rsa) 文件。按照提示为密钥设置一个密码保护，然后记下生成路径。

生成的公钥内容复制到服务器的 authorized_keys 文件中。可以使用以下命令直接传输公钥：

linux/macos:
```shell
ssh-copy-id username@your_server_ip
```

win:
```powershell
Get-Content C:\Users\YourUsername\.ssh\id_rsa.pub
```
将输出文本发送给管理员

直接使用终端，或使用图形化的客户端
[finalshell(Windows,macOS,Linux)](https://www.hostbuf.com/t/988.html)集成ftp、文本编辑
[tabby(Windows,macOS,Linux)](https://github.com/Eugeny/tabby)全开源、ftp
[vscode(Win/Mac/Linux)](https://code.visualstudio.com/download)IDE

## zerotier

zerotier提供内网穿透，在本地和远程都安装zerotier，zerotier会创建一个虚拟网卡，只要加入到同一个zerotier网络，所有设备都会得到一个zerotier局域网ip，可以通过这个IP在任意互联网环境访问zerotier局域网内的其他ip

创建zerotier账号，[zerotier网络管理](https://my.zerotier.com/)
登陆后创建网络Create A Network，记下Network ID
<img src="pics\create_zerotier_network.png" alt="示例图片" width="800"/>

在本地和远程都安装！

### win安装zerotier
[zerotier_win_ui](https://download.zerotier.com/dist/ZeroTier%20One.msi)
安装完成后默认会最小化到托盘！
Join Network,输入Network ID并确认
<img src="pics\win_join_zerotier.png" alt="示例图片" width="300"/>

### linux安装zerotier
安装
```
curl -s https://install.zerotier.com | sudo bash
```
Join Network
```
sudo zerotier-cli join <id> #将<id>替换为zerotier网络id
```
查询zerotier网络状态
```
zerotier-cli listnetworks
```

### zerotier管理页面授权！

authorize本地主机和远程主机
<img src="pics\zerotier_zuthorize.png" alt="示例图片" width="300"/>
Managed IPs是zerotier局域网ip，随机分配的静态ip

授权后等待一段时间查看本地主机和远程主机是否已经显示zerotierip
ping查看链接延迟
```
ping <zerotier ip>
```

### 可以直接通过zerotier ip使用微软远程桌面使用图形桌面

## matlab

容器内已安装了edge浏览器

下载安装包,需要使用bjtu邮箱注册
```url
https://www.mathworks.com/downloads/
```
<img src="pics\download_matlab_packge.png" alt="示例图片" width="800"/>

解压安装包，默认下载路径为/home/newuser/Downloads/
<img src="pics\extract_matlab_packge.png" alt="示例图片" width="800"/>


安装
```shell
cd /home/newuser/Downloads/matlab_R2024b_Linux/
./install
```

<img src="pics\start_install.png" alt="示例图片" width="800"/>

选择安装路径
```
/home/newuser/MATLAB/R2024b
```

<img src="pics\select_destination_path.png" alt="示例图片" width="800"/>

 启动matlab
```
/home/newuser/MATLAB/R2024b/bin/matlab
```

<img src="pics\start_install.png" alt="示例图片" width="800"/>

## 本地matlab通过ssh调用远程主机

待更新