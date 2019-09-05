1.安装Ubuntu18.04.10


	//ip设置后不生效的处理办法
	ip addr flush dev ens33
	ifdown ens33
	ifup ens33

2.安装搜狗输入法
   	登录root用户,输入 su即可切换root
	卸载ibus

	    ubuntu默认使用ibus管理输入法,官方推荐使用fcitx.我们先卸载ibus

	sudo apt-get remove ibus

	清除ibus配置,如果没有设置

	sudo apt-get purge ibus

	卸载顶部面板任务栏上的键盘指示

	sudo  apt-get remove indicator-keyboard

	安装fcitx输入法框架

	sudo apt install fcitx-table-wbpy fcitx-config-gtk

	切换为 Fcitx输入法

	im-config -n fcitx

	配置完成最好重启系统,确保可以生效

	sudo shutdown -r now

	安装搜狗

	搜狗良心,有Linux版输入法,网站https://pinyin.sogou.com/linux/?r=pinyin

	用浏览器或者wget下载下来,mv或者cp到指定目录

	安装搜狗输入法

	sudo dpkg -i sogoupinyin_2.2.0.0108_amd64.deb

	修复损坏缺少的包

	 sudo apt-get install -f

	再次安装搜狗

	sudo dpkg -i sogoupinyin_2.2.0.0108_amd64.deb

	5.输入法设置

	点击--右上角开关机的地方有一个螺丝刀加扳手的图标
	在输入法这里点击 -配置当前输入法

	将搜狗挪到第一个,体验搜狗的便利之处,另外可以自行设置皮肤.



3.安装v2ray应用软件并设置全局变量http用于下载go
	v2ray软件安装

	root@vrpro:/home/vrpro# bash <(curl -L -s https://install.direct/go.sh)

	Command 'curl' not found, but can be installed with:

	apt install curl

	root@vrpro:/home/vrpro# apt install curl
	Reading package lists... Done
	Building dependency tree       
	Reading state information... Done
	The following additional packages will be installed:
	  libcurl4
	The following NEW packages will be installed:
	  curl libcurl4
	0 upgraded, 2 newly installed, 0 to remove and 2 not upgraded.
	Need to get 373 kB of archives.
	After this operation, 1,036 kB of additional disk space will be used.
	Do you want to continue? [Y/n] y
	Get:1 http://cn.archive.ubuntu.com/ubuntu bionic-updates/main amd64 libcurl4 amd64 7.58.0-2ubuntu3.7 [214 kB]
	Get:2 http://cn.archive.ubuntu.com/ubuntu bionic-updates/main amd64 curl amd64 7.58.0-2ubuntu3.7 [159 kB]
	Get:2 http://cn.archive.ubuntu.com/ubuntu bionic-updates/main amd64 curl amd64 7.58.0-2ubuntu3.7 [159 kB]
	Get:2 http://cn.archive.ubuntu.com/ubuntu bionic-updates/main amd64 curl amd64 7.58.0-2ubuntu3.7 [159 kB]
	Fetched 313 kB in 2min 43s (1,917 B/s)                                         
	Selecting previously unselected package libcurl4:amd64.
	(Reading database ... 163820 files and directories currently installed.)
	Preparing to unpack .../libcurl4_7.58.0-2ubuntu3.7_amd64.deb ...
	Unpacking libcurl4:amd64 (7.58.0-2ubuntu3.7) ...
	Selecting previously unselected package curl.
	Preparing to unpack .../curl_7.58.0-2ubuntu3.7_amd64.deb ...
	Unpacking curl (7.58.0-2ubuntu3.7) ...
	Setting up libcurl4:amd64 (7.58.0-2ubuntu3.7) ...
	Processing triggers for libc-bin (2.27-3ubuntu1) ...
	Processing triggers for man-db (2.8.3-2ubuntu0.1) ...
	Setting up curl (7.58.0-2ubuntu3.7) ...
	root@vrpro:/home/vrpro# bash <(curl -L -s https://install.direct/go.sh)
	Installing V2Ray v4.20.0 on x86_64
	Downloading V2Ray: https://github.com/v2ray/v2ray-core/releases/download/v4.20.0/v2ray-linux-64.zip
	  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
		                         Dload  Upload   Total   Spent    Left  Speed
	100   608    0   608    0     0   1218      0 --:--:-- --:--:-- --:--:--  1216
	100 11.3M  100 11.3M    0     0   240k      0  0:00:48  0:00:48 --:--:--  255k
	Extracting V2Ray package to /tmp/v2ray.
	Archive:  /tmp/v2ray/v2ray.zip
	  inflating: /tmp/v2ray/config.json  
	   creating: /tmp/v2ray/doc/
	  inflating: /tmp/v2ray/doc/readme.md  
	  inflating: /tmp/v2ray/geoip.dat    
	  inflating: /tmp/v2ray/geosite.dat  
	   creating: /tmp/v2ray/systemd/
	  inflating: /tmp/v2ray/systemd/v2ray.service  
	   creating: /tmp/v2ray/systemv/
	  inflating: /tmp/v2ray/systemv/v2ray  
	  inflating: /tmp/v2ray/v2ctl        
	 extracting: /tmp/v2ray/v2ctl.sig    
	  inflating: /tmp/v2ray/v2ray        
	 extracting: /tmp/v2ray/v2ray.sig    
	  inflating: /tmp/v2ray/vpoint_socks_vmess.json  
	  inflating: /tmp/v2ray/vpoint_vmess_freedom.json  
	PORT:20652
	UUID:990d69f1-b398-4700-be2c-6f099a714ff4
	Created symlink /etc/systemd/system/multi-user.target.wants/v2ray.service → /etc/systemd/system/v2ray.service.
	V2Ray v4.20.0 is installed.
	root@vrpro:/home/vrpro# 



	以上为安装v2ray软件
	--=====================================================================================
	Linux 安装脚本 {#linuxscript}

	V2Ray 提供了一个在 Linux 中的自动化安装脚本。这个脚本会自动检测有没有安装过 V2Ray，如果没有，则进行完整的安装和配置；如果之前安装过 V2Ray，则只更新 V2Ray 二进制程序而不更新配置。

	以下指令假设已在 su 环境下，如果不是，请先运行 sudo su。

	运行下面的指令下载并安装 V2Ray。当 yum 或 apt-get 可用的情况下，此脚本会自动安装 unzip 和 daemon。这两个组件是安装 V2Ray 的必要组件。如果你使用的系统不支持 yum 或 apt-get，请自行安装 unzip 和 daemon

	bash <(curl -L -s https://install.direct/go.sh)

	此脚本会自动安装以下文件：

	    /usr/bin/v2ray/v2ray：V2Ray 程序；
	    /usr/bin/v2ray/v2ctl：V2Ray 工具；
	    /etc/v2ray/config.json：配置文件；
	    /usr/bin/v2ray/geoip.dat：IP 数据文件
	    /usr/bin/v2ray/geosite.dat：域名数据文件

	此脚本会配置自动运行脚本。自动运行脚本会在系统重启之后，自动运行 V2Ray。目前自动运行脚本只支持带有 Systemd 的系统，以及 Debian / Ubuntu 全系列。

	运行脚本位于系统的以下位置：

	    /etc/systemd/system/v2ray.service: Systemd
	    /etc/init.d/v2ray: SysV

	脚本运行完成后，你需要：

	    编辑 /etc/v2ray/config.json 文件来配置你需要的代理方式；
	    运行 service v2ray start 来启动 V2Ray 进程；
	    之后可以使用 service v2ray start|stop|status|reload|restart|force-reload 控制 V2Ray 的运行。

	以上为说明v2ray的linux安装方式go.sh
	--=============================================================================================

	在下载并安装了 V2Ray 之后，你需要对它进行一下配置。这里介绍一下简单的配置方式，只是为了演示，如需配置更复杂的功能，请参考后续的配置文件说明。
	客户端 {#client}

	在你的 PC （或手机）中，你需要运行 V2Ray 并使用下面的配置：

	{
	  "inbounds": [{
	    "port": 1080,  // SOCKS 代理端口，在浏览器中需配置代理并指向这个端口
	    "listen": "127.0.0.1",
	    "protocol": "socks",
	    "settings": {
	      "udp": true
	    }
	  }],
	  "outbounds": [{
	    "protocol": "vmess",
	    "settings": {
	      "vnext": [{
		"address": "server", // 服务器地址，请修改为你自己的服务器 ip 或域名
		"port": 10086,  // 服务器端口
		"users": [{ "id": "b831381d-6324-4d53-ad4f-8cda48b30811" }]
	      }]
	    }
	  },{
	    "protocol": "freedom",
	    "tag": "direct",
	    "settings": {}
	  }],
	  "routing": {
	    "domainStrategy": "IPOnDemand",
	    "rules": [{
	      "type": "field",
	      "ip": ["geoip:private"],
	      "outboundTag": "direct"
	    }]
	  }
	}

	上述配置唯一要改的地方就是你的服务器 IP，配置中已注明。上述配置会把除了局域网（比如访问路由器）之外的所有流量转发到你的服务器。

	以上为v2ray客户端的简单配置
	--=============================================================================================










	设置http代理全局变量
	$ export http_proxy="http://PROXY_SERVER:PORT"
	$ export https_proxy="https://PROXY_SERVER:PORT"
	$ export ftp_proxy="http://PROXY_SERVER:PORT"
	或
	$ export {http,https,ftp}_proxy="http://PROXY_SERVER:PORT"
	$ unset {http,https,ftp}_proxy --取消设置

	将改变保存到.bashrc环境变量文件
	If you use a proxy server often, you can create Bash functions as follows (add to your ~/.bashrc file):

	# Set Proxy
	function setproxy() {
	    export {http,https,ftp}_proxy="http://PROXY_SERVER:PORT"
	}

	# Unset Proxy
	function unsetproxy() {
	    unset {http,https,ftp}_proxy
	}

	Reload your ~/.bashrc file.

	$ source ~/.bashrc

	Now use the setproxy and unsetproxy commands to set and unset Linux proxy server settings.
	Lists of Free Public Proxy Servers

	WARNING: Free public proxy servers can insert your IP address into the headers of requests or sniff your traffic! Don’t use them to transfer sensitive data and do not expect anonymity!

	    Hide My Ass
	    Proxy Server List
	    Anonymous Public Proxy Servers
	    Daily HTTP Proxies

	Cool Tip: Even if you use proxy server, all your DNS queries still go to the name servers of your ISP (Internet Service Provider)! Improve anonymity, by using free public name servers! Read more →

	
	可设置不通过代理的ip或域名

	You can use no_proxy or NO_PROXY that includes a comma delimited list of domains, subdomains, hostnames, and/or IP addresses that are exempt from the {http{,s},ftp,rsync}_proxy variables.

	So something like
	export no_proxy=’localhost,127.0.0.1,.example.com,.shellhacks.com’





	检查代理设置是否成功Check your public IP address from the Linux command-line:

	$ wget -q -O - checkip.dyndns.org \
	| sed -e 's/.*Current IP Address: //' -e 's/<.*$//'

4.安装通过snap安装go

	安装最新版本
	sudo snap install go --classic
	或安装指定版本
	sudo snap install go --channel=1.11/stable --classic

5.通过snap安装vscode
	 snap remove vscode
	 snap install code --classic

6.安装git并设置git用户的全局变量

	Debian/Ubuntu

	For the latest stable version for your release of Debian/Ubuntu
	# apt-get install git

	For Ubuntu, this PPA provides the latest stable upstream Git version
	# add-apt-repository ppa:git-core/ppa # apt update; apt install git

	运行以下命令设置git的全局用户参数：
	  git config --global user.email "you@example.com"
	  git config --global user.name "Your Name"

7.安装vscode的go插件，并设置vscode与git，go的集成


8.安装gcc并将~/go/bin加入到LINUX的PATH路径中
	sudo apt install gcc
	export PATH=$PATH:~/go/bin

9.拉取v2ray的代码，并设置git，尝试push是否成功

V2ray更新到自己的fork主页

	1.先 Fork 本项目，创建你自己的 github.com/your/v2ray-core；
	2.在你的 Go workspace (~/go/src/)中运行：go get -u v2ray.com/core/...；
	3.在 go get 创建的 v2ray-core 目录(v2ray.com/core)中运行：git remote add fork https://github.com/you/cooltool.git；
	4.然后你可以在 v2ray-core 中修改代码，由于这是一个 v2ray 的 clone，import path 不受影响；
	5.运行以下命令设置git的全局用户参数：
	  git config --global user.email "you@example.com"
	  git config --global user.name "Your Name"
	6.修改完成之后，运行：
	  git commit -a -m ’更新原因' //commit 修改
	  git push 'https://github.com/feng613/v2ray-core.git' //你的fork主页

	7.如果贡献到origin，去你的 fork（就是 v2ray.com/core）中发一个 PR 即可；

https://github.com/feng613/v2ray-core.git

//需要安装的软件环境:github,go,输入法.
