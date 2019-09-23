# Linux_loraserver_tomcat
this is my study project

## 利用Linux系统搭建 Loraserver 以及 Tomcat 配置java项目
### 首先到阿里云购买一个阿里云服务器
1. 选择Linux CentOS7.6 系统 配置随意
2. 然后搭建完成后需要进行以下的操作 
因为权限限制，所以我们需要进入 root 模式，开机使用 root 登陆或者系统运行中切换为 root 用户均可。

安装  X 窗口系统

1、首先安装X(X Window System)，命令为

yum groupinstall "X Window System" 　//注意有引号
然后系统会自动寻找最近的网络进行相关文件的下载
选择 y ，然后开始下载需要的 packag
选择 y，开始进行安装
当出现 Complete！说明这里安装成功了。

在这里我们可以检查一下我们已经安装的软件以及可以安装的软件，命令为

yum grouplist

安装图形界面软件 GNOME
然后我们开始安装我们需要的图形界面软件，GNOME(GNOME Desktop)
特别注意！！！！一定要注意名称必须对应，否则会出现No packages in any requested group available to install or update 的错误。这是因为不同版本的CentOS的软件名可能不同（其他 Linux 系统也是类似的）
如上图，安装命令为：

yum groupinstall "GNOME Desktop" "Graphical Administration Tools"

选择 y 开始下载需要安装的 package

完成后可以重启下 直接进入桌面化操作

安装的如下网址：https://www.linuxidc.com/Linux/2018-04/152000.htm

### 安装LoraServer
首先到 http://www.rimecloud.com/ DIY 部署 LoRaServer 选择相应的版本下载
选择下载好后边看文档边配置安装 按照文档一步一步的操作基本不会错

关键部分 修改端口 8080改为 9090 需要到 Linux系统下 /opt/loraserver/lora-app-server.toml文件中更改
安装了窗体界面虚拟机 选择 Places ->Computer->选择 opt/loraserver/ lora-app-server.toml文件进行修改就可以了 图形界面直接找到直接用Text文本打开更改
还有配置 jwt密钥也是在里面修改 原代码是 jwt="www.rimecloud.com" 改成你需要的密钥 这个是为了做APP获取api接口使用的必须要的
然后重启 sudo systemctl restart lora-app-server.service 然后输入 sudo firewall-cmd —state
选择阿里云开放9090端口的 安全规则

进入阿里云选择 更多->网络和安全组->添加安全组规则 ->添加 9090端口 具体可以百度看图片操作过程
端口范围选择 9090/9090 授权对象为 0.0.0.0/0 优先级 1
到这里基本完成操作

### 配置Tomcat

按照这个网址操作 https://www.cnblogs.com/skyflask/p/9023749.html
注意点 安装了 CentOS桌面版本后 是自带 JAVA的可以省去Java的安装操作
直接安装 Tomcat
可以直接到官网下载 Tomcat最新的安装包 注意必须要选择 上面的哪个 不是带Soruce的哪个 不然安装包解压不完整启动不了的

1、下载安装包

wget http://mirror.bit.edu.cn/apache/tomcat/tomcat-8/v8.5.31/bin/apache-tomcat-8.5.31.tar.gz
tar xf apache-tomcat-8.5.31.tar.gz -C /usr/local/
cd /usr/local/
ln -sv apache-tomcat-8.5.31 tomcat

2.配置环境变量

vim /etc/profile.d/tomcat.sh

CATALINA_BASE=/usr/local/tomcat
PATH=$CATALINA_BASE/bin:$PATH
export PATH CATALINA_BASE

让配置生效：

source  /etc/profile.d/tomcat.sh

3.查看tomcat版本状态

catalina.sh version

其它的 请看上面的网址

### mysql的安装













