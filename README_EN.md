<img src="https://github.com/snail007/goproxy/blob/master/docs/images/logo.jpg?raw=true" width="200"/>  
Proxy is a high performance HTTP, HTTPS, HTTPS, websocket, TCP, UDP, Socks5 proxy server implemented by golang. It supports parent proxy,nat forward,TCP/UDP port forwarding, SSH transfer. you can expose a local server behind a NAT or firewall to the internet.  
  
---  
  
[![stable](https://img.shields.io/badge/stable-stable-green.svg)](https://github.com/snail007/goproxy/) [![license](https://img.shields.io/github/license/snail007/goproxy.svg?style=plastic)]() [![download_count](https://img.shields.io/github/downloads/snail007/goproxy/total.svg?style=plastic)](https://github.com/snail007/goproxy/releases) [![download](https://img.shields.io/github/release/snail007/goproxy.svg?style=plastic)](https://github.com/snail007/goproxy/releases)  
  
[中文手册](/README.md)  

### Features  
- chain-style proxy: the program itself can be a primary proxy, and if a parent proxy is set, it can be used as a second level proxy or even a N level proxy.  
- Encrypted communication: if the program is not a primary proxy, and the parent proxy is also the program, then it can communicate with the parent proxy by encryption. The TLS encryption is high-intensity encryption, and it is safe and featureless.  
- Intelligent HTTP, SOCKS5 proxy: the program will automatically determine whether the site which it access is blocked, if the site is blocked, the program will use parent proxy (the premise is you set up a parent proxy) to access the site. If the site isn't blocked, in order to speed up the access, the program will directly access the site and don't use parent proxy.  
- The black-and-white list of domain: It is very flexible to control the way which you visite site.  
- Cross platform: no mater what the os (such as Linux, windows, and even Raspberry Pi) you use, you always can use proxy well.  
- Multi protocol support: the program support HTTP (S), TCP, UDP, Websocket, SOCKS5 proxy. 
- The TCP/UDP port  forwarding is supported. 
- Nat forwarding in different network is supported: the program support TCP protocol and UDP protocol.  
- SSH forwarding: HTTP (S), SOCKS5 proxy support SSH transfer, parent Linux server does not need any server, a local proxy can be happy to access the Internet.  
- [KCP](https://github.com/xtaci/kcp-go) protocol is supported: HTTP (S), SOCKS5 proxy supports the KCP protocol which can transmit data, reduce latency, and improve the browsing experience.  
- The integrated external API, HTTP (S): SOCKS5 proxy authentication can be integrated with the external HTTP API, which can easily control the user's access through the external system.  
  
### Why need these?  
- Because for some reason, we cannot access our services elsewhere. We can build a secure tunnel to access our services through multiple connected proxy nodes.  
- WeChat interface is developed locally, which is convenient to debug.  
- Remote access to intranet machines.  
- Play with partners in a LAN game.  
- something used to be played only in the LAN, now it can be played anywhere.  
- Instead of 剑内网通,显IP内网通,花生壳,frp and so on.
- ...  

 
This page is the v4.0-v4.1 manual, and the other version of the manual can be checked by the following link.  
- [v3.9 manual](https://github.com/snail007/goproxy/tree/v3.9)
- [v3.8 manual](https://github.com/snail007/goproxy/tree/v3.8)
- [v3.6-v3.7 manual](https://github.com/snail007/goproxy/tree/v3.6)
- [v3.5 manual](https://github.com/snail007/goproxy/tree/v3.5)
- [v3.4 manual](https://github.com/snail007/goproxy/tree/v3.4)
- [v3.3 manual](https://github.com/snail007/goproxy/tree/v3.3)
- [v3.2 manual](https://github.com/snail007/goproxy/tree/v3.2)
- [v3.1 manual](https://github.com/snail007/goproxy/tree/v3.1)
- [v3.0 manual](https://github.com/snail007/goproxy/tree/v3.0)
- [v2.x manual](https://github.com/snail007/goproxy/tree/v2.2)  

### How to find the organization?  
[Click to join the communication organization](https://gitter.im/go-proxy/Lobby?utm_source=share-link&utm_medium=link&utm_campaign=share-link)  

### Installation
- [Quick installation](#quick-installation)
- [Manual installation](#manual-installation)

### First use must be read
- [Environmental Science](#environmental-science)
- [Use configuration file](#use-configuration-file)
- [Debug output](#debug-output)
- [Using log files](#using-log-files)
- [Daemon mode](#daemon-mode)
- [Monitor mode](#monitor-mode)
- [Generating a communication certificate file](#generating-a-communication-certificate-file)
- [Safety advice](#safety-advice)

### Manual catalogues
- [1.HTTP proxy](#1http-proxy)
    - [1.1 Common HTTP proxy](#11common-http-proxy)
    - [1.2 Common HTTP second level proxy](#12common-http-second-level-proxy)
    - [1.3 HTTP second level proxy(encrypted)](#13http-second-level-encrypted-proxy)
    - [1.4 HTTP third level proxy(encrypted)](#14http-third-level-encrypted-proxy)
    - [1.5 Basic Authentication](#15basic-authentication)
    - [1.6 HTTP proxy traffic force to go to parent http proxy](#16http-proxy-traffic-force-to-go-to-parent-http-proxy)
    - [1.7 Transfer through SSH](#17transfer-through-ssh)
        - [1.7.1 The way of username and password](#171the-way-of-username-and-password)
        - [1.7.2 The way of username and key](#172the-way-of-username-and-key)
    - [1.8 KCP protocol transmission](#18kcp-protocol-transmission)
    - [1.9 View help](#19view-help)
- [2.TCP proxy](#2tcp-proxy)
    - [2.1 Common TCP first level proxy](#21common-tcp-first-level-proxy)
    - [2.2 Common TCP second level proxy](#22common-tcp-second-level-proxy)
    - [2.3 Common TCP third level proxy](#23common-tcp-third-level-proxy)
    - [2.4 TCP second level encrypted proxy](#24tcp-second-level-encrypted-proxy)
    - [2.5 TCP third level encrypted proxy](#25tcp-third-level-encrypted-proxy)
    - [2.6 View help](#26view-help)
- [3.UDP proxy](#3udp-proxy)
    - [3.1 Common UDP first level proxy](#31common-udp-first-level-proxy)
    - [3.2 Common UDP second level proxy](#32common-udp-second-level-proxy)
    - [3.3 Common UDP third level proxy](#33common-udp-third-level-proxy)
    - [3.4 UDP second level encrypted proxy](#34udp-second-level-encrypted-proxy)
    - [3.5 UDP third level encrypted proxy](#35udp-third-level-encrypted-proxy)
    - [3.6 View help](#36view-help)
- [4.Nat forward](#4nat-forward)
    - [4.1 Principle explanation](#41principle-explanation)
    - [4.2 TCP common usage](#42tcp-common-usage)
    - [4.3 Local development of WeChat interface](#43local-development-of-wechat-interface)
    - [4.4 UDP common usage](#44udp-common-usage)
    - [4.5 Advanced usage 1](#45advanced-usage-1)
    - [4.6 Advanced usage 2](#46advanced-usage-2)
    - [4.7 -r parameters of server](#47-r-parameters-of-server)
    - [4.8 View help](#48view-help)
- [5.SOCKS5 proxy](#5socks5-proxy)
    - [5.1 Common SOCKS5 proxy](#51common-socks5-proxy)
    - [5.2 Common SOCKS5 second level proxy](#52common-socks5-second-level-proxy)
    - [5.3 SOCKS5 second level proxy(encrypted)](#53socks-second-level-encrypted-proxy)
    - [5.4 SOCKS third level proxy(encrypted)](#54socks-third-level-encrypted-proxy)
    - [5.5 SOCKS proxy traffic force to go to parent socks proxy](#55socks-proxy-traffic-force-to-go-to-parent-socks-proxy)
    - [5.6 Transfer through SSH](#56transfer-through-ssh)
        - [5.6.1 The way of username and password](#561the-way-of-username-and-password)
        - [5.6.2 The way of username and key](#562the-way-of-username-and-key)
    - [5.7 Authentication](#57authentication)
    - [5.8 KCP protocol transmission](#58kcp-protocol-transmission)
    - [5.9 View help](#59view-help)

### Fast Start  
tips:all operations require root permissions.   
#### Quick installation
#### **0. If your VPS is a linux64 system, you can complete the automatic installation and configuration by the following sentence.**  
```shell  
curl -L https://raw.githubusercontent.com/snail007/goproxy/master/install_auto.sh | bash  
```  
The installation is completed, the configuration directory is /etc/proxy, more detailed use of the method referred to the following manual for further understanding.  
If the installation fails or your VPS is not a linux64 system, please follow the semi-automatic step below:  
  
#### Manual installation 

#### **1.Download proxy**  
Download address: https://github.com/snail007/goproxy/releases  
```shell  
cd /root/proxy/  
wget https://github.com/snail007/goproxy/releases/download/v4.0/proxy-linux-amd64.tar.gz  
```  
#### **2.Download the automatic installation script**  
```shell  
cd /root/proxy/  
wget https://raw.githubusercontent.com/snail007/goproxy/master/install.sh  
chmod +x install.sh  
./install.sh  
```  
  
## **First use must be read**  
  
### **Environmental Science**  
The following tutorial, the default system is Linux, the program is proxy; all operations require root permissions.   
If the system are windows, please use proxy.exe.  
  
### **Use configuration file**  
The following tutorial is to introduce the use method by the command line parameters, or by reading the configuration file to get the parameters.  
The specific format is to specify a configuration file by the @ symbol, for example, ./proxy @configfile.txt.   
configfile.txt's format: The first line is the subcommand name, and the second line begins one line: the long format of the parameter = the parameter value, there is no space and double quotes before and after.  
The long format of the parameter's beginning is always --, the short format of the parameter's beginning is always -. If you don't know which short form parameter corresponds to the long format parameter, please look at the help command.  
For example, the contents of configfile.txt are as follows:
```shell
http
--local-type=tcp
--local=:33080
```
### **Debug output**   
By default, the log output information does not contain the number of file lines. In some cases, in order to eliminate and positione the program problem, You can use the --debug parameter to output the number of lines of code and the wrong time.   

### **Using log files**   
By default, the log is displayed directly on the console, and if you want to save it to the file, you can use the --log parameter.  
for example, --log proxy.log, The log will be exported to proxy.log file which is easy to troubleshoot.   

### **Generating a communication certificate file**  
HTTP, TCP, UDP proxy process will communicate with parent proxy. In order to secure, we use encrypted communication. Of course, we can choose not to encrypted communication. All communication with parent proxy in this tutorial is encrypted, requiring certificate files.    
The OpenSSL command is installed on the Linux and encrypted certificate can be generated directly through the following command.    
`./proxy keygen`  
By default, the certificate file proxy.crt and the key file proxy.key are generated under the current program directory.  
  
### **Daemon mode**
After the default execution of proxy, if you want to keep proxy running, you can't close the command line. 
If you want to run proxy in the daemon mode, the command line can be shut down, just add the --daemon parameter at the end of the command.    
for example: `./proxy http -t tcp -p "0.0.0.0:38080" --daemon`   

### **Monitor mode**  
Monitor mode parameter --forever, for example: `proxy http --forever`,  
Proxy will fork subprocess, then monitor the child process, if the subprocess exits, restarts the subprocess after 5 seconds.  
This parameter, with the parameter --daemon and the log parameter --log, can guarantee that the proxy has been ran in the background and not exited accidentally.  
And you can see the output log of proxy through the log file.   
for example: `proxy http -p ":9090" --forever --log proxy.log --daemon`  

### **Safety advice**
When vps is behind the NAT, the network card IP on VPS is an internal network IP, and then you can add the VPS's external network IP to prevent the dead cycle by -g parameter.  
Assuming that your VPS outer external network IP is 23.23.23.23, the following command sets the 23.23.23.23 through the -g parameter.  
`./proxy http -g "23.23.23.23"`  

### **1.HTTP proxy**  
#### **1.1.common HTTP proxy**  
`./proxy http -t tcp -p "0.0.0.0:38080"`  
  
#### **1.2.Common HTTP second level proxy**  
Using local port 8090, assume the parent HTTP proxy is: `22.22.22.22:8080`  
`./proxy http -t tcp -p "0.0.0.0:8090" -T tcp -P "22.22.22.22:8080" `  
The connection pool is closed by default. If you want to speed up access speed, -L can open the connection pool, the 10 is the size of the connection pool, and the 0 is closed.  
It is not good to stability of connection pool when the network is not good.  
`./proxy http -t tcp -p "0.0.0.0:8090" -T tcp -P "22.22.22.22:8080" -L 10`  
We can also specify the black and white list files of the domain name, one line for one domain name. The matching rule is the most right-hand matching, for example, baidu.com, which matches *.*.baidu.com. The domain name of the blacklist is directly headed by the parent proxy, and the domain name of the white list does not go to the parent proxy.  
`./proxy http -p "0.0.0.0:8090" -T tcp -P "22.22.22.22:8080"  -b blocked.txt -d direct.txt`  
  
#### **1.3.HTTP second level encrypted proxy**  
HTTP first level proxy(VPS,IP:22.22.22.22)    
`./proxy http -t tls -p ":38080" -C proxy.crt -K proxy.key`  
  
HTTP second level proxy(local Linux)  
`./proxy http -t tcp -p ":8080" -T tls -P "22.22.22.22:38080" -C proxy.crt -K proxy.key`  
accessing the local 8080 port is accessing the proxy port 38080 above VPS.  
  
HTTP second level proxy(local windows)  
`./proxy.exe http -t tcp -p ":8080" -T tls -P "22.22.22.22:38080" -C proxy.crt -K proxy.key`  
In your windos system, the mode of the program that needs to surf the Internet by proxy is setted up as HTTP mode, the address is 127.0.0.1, the port is: 8080, the program can go through the encrypted channel through VPS to surf on the internet.  
  
#### **1.4.HTTP third level encrypted proxy**  
HTTP first level proxy VPS_01,IP:22.22.22.22    
`./proxy http -t tls -p ":38080" -C proxy.crt -K proxy.key`  
HTTP second level proxy VPS_02,IP:33.33.33.33   
`./proxy http -t tls -p ":28080" -T tls -P "22.22.22.22:38080" -C proxy.crt -K proxy.key`  
HTTP third level proxy(local)   
`./proxy http -t tcp -p ":8080" -T tls -P "33.33.33.33:28080" -C proxy.crt -K proxy.key`  
Then access to the local 8080 port is access to the HTTP first level proxy which port is 38080.  
  
#### **1.5.Basic Authentication**  
We can do Basic authentication for the HTTP proxy, The authenticated username and password can be specified at the command line.  
`./proxy http -t tcp -p ":33080" -a "user1:pass1" -a "user2:pass2"`  
If you need multiple users, repeat the -a parameters.   
You can also be placed in a file, which is a line, a ‘username: password’, and then specified in -F.    
`./proxy http -t tcp -p ":33080" -F auth-file.txt`   
  
In addition, the HTTP (s) proxy also integrates external HTTP API authentication, and we can specify a HTTP URL interface address by the --auth-url parameter.  
When somebody connect the proxy, which will request this URL by GET way, with the following four parameters, and if the HTTP state code 204 is returned, the authentication is successful.  
In other cases, authentication failed.  
for example:  
`./proxy http -t tcp -p ":33080" --auth-url "http://test.com/auth.php"`  
When the user connecte the proxy, which will request this URL by GET way("http://test.com/auth.php"),  
 with user, pass, IP, and target four parameters:  
http://test.com/auth.php?user={USER}&pass={PASS}&ip={IP}&target={TARGET}  
user:username  
pass:password  
ip:user's IP,for example: 192.168.1.200  
target:URL user connect to, for example: http://demo.com:80/1.html  or  https://www.baidu.com:80  

If there is no -a or -F or --auth-url parameters, Basic authentication is closed.   

#### **1.6.HTTP proxy traffic force to go to parent http proxy**  
By default, proxy will intelligently judge whether a domain name can be accessed. If it cannot be accessed, it will access to parent HTTP proxy.    
Through --always, all HTTP proxy traffic can be coercion to the parent HTTP proxy.  
`./proxy http --always -t tls -p ":28080" -T tls -P "22.22.22.22:38080" -C proxy.crt -K proxy.key`  
  
#### **1.7.Transfer through SSH**  
Explanation: the principle of SSH transfer is to take advantage of SSH's forwarding function, which is, after you connect to SSH, you can access to the target address through the SSH proxy.  
Suppose there is a vps  
- IP is 2.2.2.2, ssh port is 22, ssh username is user, ssh password is demo  
- The SSH private key of the user is user.key    

##### ***1.7.1.The way of username and password***   
Local HTTP (S) proxy use 28080 port,excute:  
`./proxy http -T ssh -P "2.2.2.2:22" -u user -A demo -t tcp -p ":28080"`  
##### ***1.7.2.The way of username and key***   
Local HTTP (S) proxy use 28080 port,excute:  
`./proxy http -T ssh -P "2.2.2.2:22" -u user -S user.key -t tcp -p ":28080"`  

#### **1.8.KCP protocol transmission**  
The KCP protocol requires a -B parameter to set a password which can encrypt and decrypt data.  

Http first level proxy(VPS,IP:22.22.22.22)  
`./proxy http -t kcp -p ":38080" -B mypassword`  
  
Http second level proxy(os is Linux)  
`./proxy http -t tcp -p ":8080" -T kcp -P "22.22.22.22:38080" -B mypassword`  
Then access to the local 8080 port is access to the proxy's port 38080 on the VPS, and the data is transmitted through the KCP protocol.  

#### **1.9.view help**  
`./proxy help http`  
  
### **2.TCP proxy**  
  
#### **2.1.Common TCP first level proxy**  
Local execution:  
`./proxy tcp -p ":33080" -T tcp -P "192.168.22.33:22" -L 0`  
Then access to the local 33080 port is the 22 port of access to 192.168.22.33.  
  
#### **2.2.Common TCP second level proxy**  
VPS(IP:22.22.22.33) execute:  
`./proxy tcp -p ":33080" -T tcp -P "127.0.0.1:8080" -L 0`  
local execution:  
`./proxy tcp -p ":23080" -T tcp -P "22.22.22.33:33080"`  
Then access to the local 23080 port is the 8080 port of access to 22.22.22.33.  
  
#### **2.3.Common TCP third level proxy**  
TCP first level proxy VPS_01,IP:22.22.22.22  
`./proxy tcp -p ":38080" -T tcp -P "66.66.66.66:8080" -L 0`  
TCP second level proxy VPS_02,IP:33.33.33.33  
`./proxy tcp -p ":28080" -T tcp -P "22.22.22.22:38080"`  
TCP third level proxy (local)  
`./proxy tcp -p ":8080" -T tcp -P "33.33.33.33:28080"`  
Then access to the local 8080 port is to access the 8080 port of the 66.66.66.66 by encrypting the TCP tunnel.  
  
#### **2.4.TCP second level encrypted proxy**  
VPS(IP:22.22.22.33) execute:  
`./proxy tcp --tls -p ":33080" -T tcp -P "127.0.0.1:8080" -L 0 -C proxy.crt -K proxy.key`  
local execution:  
`./proxy tcp -p ":23080" -T tls -P "22.22.22.33:33080" -C proxy.crt -K proxy.key`  
Then access to the local 23080 port is to access the 8080 port of the 22.22.22.33 by encrypting the TCP tunnel.  
  
#### **2.5.TCP third level encrypted proxy**  
TCP first level proxy VPS_01,IP:22.22.22.22  
`./proxy tcp --tls -p ":38080" -T tcp -P "66.66.66.66:8080" -C proxy.crt -K proxy.key`  
TCP second level proxy VPS_02,IP:33.33.33.33  
`./proxy tcp --tls -p ":28080" -T tls -P "22.22.22.22:38080" -C proxy.crt -K proxy.key`  
TCP third level proxy (local)  
`./proxy tcp -p ":8080" -T tls -P "33.33.33.33:28080" -C proxy.crt -K proxy.key`  
Then access to the local 8080 port is to access the 8080 port of the 66.66.66.66 by encrypting the TCP tunnel.  
  
#### **2.6.view help**  
`./proxy help tcp`  
  
### **3.UDP proxy**  
  
#### **3.1.Common UDP first level proxy**  
local execution:  
`./proxy udp -p ":5353" -T udp -P "8.8.8.8:53"`  
Then access to the local UDP:5353 port is access to the UDP:53 port of the 8.8.8.8.  
  
#### **3.2.Common UDP second level proxy**  
VPS(IP:22.22.22.33) execute:  
`./proxy tcp -p ":33080" -T udp -P "8.8.8.8:53"`  
local execution:  
`./proxy udp -p ":5353" -T tcp -P "22.22.22.33:33080"`  
Then access to the local UDP:5353 port is access to the UDP:53 port of the 8.8.8.8 through the TCP tunnel.  
  
#### **3.3.Common UDP third level proxy**  
TCP first level proxy VPS_01,IP:22.22.22.22  
`./proxy tcp -p ":38080" -T udp -P "8.8.8.8:53"`  
TCP second level proxy VPS_02,IP:33.33.33.33  
`./proxy tcp -p ":28080" -T tcp -P "22.22.22.22:38080"`  
TCP third level proxy (local)  
`./proxy udp -p ":5353" -T tcp -P "33.33.33.33:28080"`  
Then access to the local 5353 port is access to the 53 port of the 8.8.8.8 through the TCP tunnel.  
  
#### **3.4.UDP second level encrypted proxy**  
VPS(IP:22.22.22.33) execute:  
`./proxy tcp --tls -p ":33080" -T udp -P "8.8.8.8:53" -C proxy.crt -K proxy.key`  
local execution:  
`./proxy udp -p ":5353" -T tls -P "22.22.22.33:33080" -C proxy.crt -K proxy.key`  
Then access to the local UDP:5353 port is access to the UDP:53 port of the 8.8.8.8 by the encrypting TCP tunnel. 
  
#### **3.5.UDP third level encrypted proxy**  
TCP first level proxy VPS_01,IP:22.22.22.22  
`./proxy tcp --tls -p ":38080" -T udp -P "8.8.8.8:53" -C proxy.crt -K proxy.key`  
TCP second level proxy VPS_02,IP:33.33.33.33  
`./proxy tcp --tls -p ":28080" -T tls -P "22.22.22.22:38080" -C proxy.crt -K proxy.key`  
TCP third level proxy (local)  
`./proxy udp -p ":5353" -T tls -P "33.33.33.33:28080" -C proxy.crt -K proxy.key`  
Then access to the local UDP:5353 port is access to the UDP:53 port of the 8.8.8.8 by the encrypting TCP tunnel. 
  
#### **3.6.view help**  
`./proxy help udp`  
  
### **4.Nat forward**  
#### **4.1、Principle explanation**  
Nat forward, divided into two versions, "multi-link version" and "multiplexed version", generally like web services Which is not a long time to connect the service recommended "multi-link version", if you want to keep long Time connection, "multiplexed version" is recommended.
1. Multilink version, the corresponding subcommand is tserver，tclient，tbridge。  
1. Multiplexed version, the corresponding subcommand is server，client，bridge。  
1. the parameters and use of Multilink version and multiplexed is exactly the same.  
1. **Multiplexed version of the server, client can open the compressed transmission, the parameter is --c.**   
1. **Server, client or both are open compression, either do not open, can not only open one.**    

The following tutorial uses "Multiplexing Versions" as an example to illustrate how to use it.    
Nat forward consists of three parts: client-side, server-side, bridge-side; client and server take the initiative to connect the bridge to bridge.    
When the user access the server side, the process is:   
1. Server and bridge initiative to establish a link;  
1. Then the bridge notifies the client to connect the bridge, and connects the intranet target port;  
1. Then bind the client to the bridge and client to the internal network port connection;  
1. Then the bridge of the client over the connection and server-side connection binding;  
1. The entire channel is completed;  
  
#### **4.2.TCP common usage** 
Background:  
- The company computer A provides the 80 port of the web service  
- There is one VPS, which public IP is 22.22.22.22  

Demand:  
You can access the 80 port of the company's computer by access to VPS's 28080 port when you are at home.  
  
Procedure:  
1. Execute on VPS  
    `./proxy bridge -p ":33080" -C proxy.crt -K proxy.key`  
    `./proxy server -r ":28080@:80" -P "127.0.0.1:33080" -C proxy.crt -K proxy.key`  
  
1. Execute on the company's computer A  
    `./proxy client -P "22.22.22.22:33080" -C proxy.crt -K proxy.key`  

1. complete  
  
#### **4.3.Local development of WeChat interface**  
Background:  
- My own computer provides the 80 port of nginx service  
- There is one VPS, which public IP is 22.22.22.22  

Demand:  
Fill out the Web callback interface configuration address of WeChat Development Account: http://22.22.22.22/calback.php  
Then you can access the calback.php under the 80 port of the computer, and if you need to bind the domain name, you can use your own domain name.  
for example: Wx-dev.xxx.com is resolved to 22.22.22.22, and then configure the domain name wx-dev.xxx.com into a specific directory in the nginx of your own computer.  

  
Procedure:  
1. Execute on VPS and ensure that the 80 port of VPS is not occupied by other programs.  
    `./proxy bridge -p ":33080" -C proxy.crt -K proxy.key`  
    `./proxy server -r ":80@:80" -P "22.22.22.22:33080" -C proxy.crt -K proxy.key`  

1. Execute it on your own computer  
    `./proxy client -P "22.22.22.22:33080" -C proxy.crt -K proxy.key`  

1. compolete  
  
#### **4.4.UDP common usage**  
Background:  
- The company computer A provides the DNS resolution, the UDP:53 port.  
- There is one VPS, which public IP is 22.22.22.22.  
  
Demand:  
You can use the company computer A for domain name resolution services by setting up local DNS as 22.22.22.22 at home.  
  
Procedure:  
1. Execute on VPS  
    `./proxy bridge -p ":33080" -C proxy.crt -K proxy.key`  
    `./proxy server --udp -r ":53@:53" -P "127.0.0.1:33080" -C proxy.crt -K proxy.key`  

1. Execute on the company's computer A  
    `./proxy client -P "22.22.22.22:33080" -C proxy.crt -K proxy.key`  

1. compolete  
  
#### **4.5.Advanced usage 1**  
Background:  
- The company computer A provides the 80 port of the web service  
- There is one VPS, which public IP is 22.22.22.22  
  
Demand:  
For security, it doesn't want to be able to access the company's computer A on VPS. At home, it can access the 80 port of the company's computer A through the encrypted tunnel by accessing the 28080 port of you own computer.  
  
Procedure:  
1. Execute on VPS  
    `./proxy bridge -p ":33080" -C proxy.crt -K proxy.key`  
  
1. Execute on the company's computer A  
    `./proxy client -P "22.22.22.22:33080" -C proxy.crt -K proxy.key`  
  
1. Execute it on your own computer  
    `./proxy server -r ":28080@:80" -P "22.22.22.22:33080" -C proxy.crt -K proxy.key`  
  
1. compolete  
  
#### **4.6.Advanced usage 2**  
Tips:  
If there are multiple client connected to the same bridge at the same time, you need to specify different key, which can be set by --k parameter. --k must be a unique string on the same bridge.  
When server is connected to bridge, if multiple client is connected to the same bridge at the same time, you need to use the --k parameter to select client.   
Repeating -r parameters can expose multiple ports: -r format is "local IP: local port @clientHOST:client port".   
  
Background:  
- The company computer A provides the web service 80 port and the FTP service 21 port  
- There is one VPS, which public IP is 22.22.22.22  
  
Demand:  
You can access the 80 port of the company's computer by access to VPS's 28080 port at home.  
You can access the 21 port of the company's computer by access to VPS's 29090 port at home.  
  
Procedure:  
1. Execute on VPS  
    `./proxy bridge -p ":33080" -C proxy.crt -K proxy.key`  
    `./proxy server -r ":28080@:80" -r ":29090@:21" --k test -P "127.0.0.1:33080" -C proxy.crt -K proxy.key`  

1. Execute on the company's computer A  
    `./proxy client --k test -P "22.22.22.22:33080" -C proxy.crt -K proxy.key` 

1. complete  
  
#### **4.7.-r parameters of server**  
  The full format of the -r is:`PROTOCOL://LOCAL_IP:LOCAL_PORT@[CLIENT_KEY]CLIENT_LOCAL_HOST:CLIENT_LOCAL_PORT`  
  
  4.7.1.PROTOCOL is tcp or udp.  
  for example: `-r "udp://:10053@:53" -r "tcp://:10800@:1080" -r ":8080@:80"`  
  If the --udp parameter is specified, PROTOCOL is UDP by default, then `-r ": 8080@: 80"` is UDP.  
  If the --udp parameter is not specified, PROTOCOL is TCP by default, then `-r ": 8080@: 80"` is TCP.  
  
  4.7.2.CLIENT_KEY by default is 'default'.  
  for example: -r "udp://:10053@[test1]:53" -r "tcp://:10800@[test2]:1080" -r ":8080@:80"  
  If the --k parameter is specified, such as --k test, then `-r ":8080@:80"` CLIENT_KEY is 'test'.  
  If the --k parameter is not specified,then `-r ":8080@:80"`CLIENT_KEY is 'default'.  
  
  4.7.3.LOCAL_IP is empty which means LOCAL_IP is `0.0.0.0`, CLIENT_LOCAL_HOST is empty which means LOCAL_IP is `127.0.0.1`. 

#### **4.8.view help**  
`./proxy help bridge`  
`./proxy help server`  
`./proxy help server`  
  
### **5.SOCKS5 proxy**  
Tips: SOCKS5 proxy, support CONNECT, UDP protocol and don't support BIND and support username password authentication.  
#### **5.1.Common SOCKS5 proxy**  
`./proxy socks -t tcp -p "0.0.0.0:38080"`  
   
#### **5.2.Common SOCKS5 second level proxy**  
Using local port 8090, assume that the parent SOCKS5 proxy is `22.22.22.22:8080`  
`./proxy socks -t tcp -p "0.0.0.0:8090" -T tcp -P "22.22.22.22:8080" `  
We can also specify the black and white list files of the domain name, one line for one domain name. The matching rule is the most right-hand matching. For example, baidu.com is *.*.baidu.com, the domain name of the blacklist is directly accessed by the parent proxy, and the domain name of the white list does not access to the parent proxy.  
`./proxy socks -p "0.0.0.0:8090" -T tcp -P "22.22.22.22:8080"  -b blocked.txt -d direct.txt`  
  
#### **5.3.SOCKS second level encrypted proxy**  
SOCKS5 first level proxy(VPS,IP:22.22.22.22)  
`./proxy socks -t tls -p ":38080" -C proxy.crt -K proxy.key`  
  
SOCKS5 second level proxy(local Linux)  
`./proxy socks -t tcp -p ":8080" -T tls -P "22.22.22.22:38080" -C proxy.crt -K proxy.key`  
Then access to the local 8080 port is access to the proxy port 38080 above VPS.  
  
SOCKS5 second level proxy(local windows)  
`./proxy.exe socks -t tcp -p ":8080" -T tls -P "22.22.22.22:38080" -C proxy.crt -K proxy.key`  
Then set up your windows system, the proxy that needs to surf the Internet by proxy is Socks5 mode, the address is: 127.0.0.1, the port is: 8080. the program can surf the Internet through the encrypted channel which is running on VPS.  
  
#### **5.4.SOCKS third level encrypted proxy**  
SOCKS5 first level proxy VPS_01,IP:22.22.22.22  
`./proxy socks -t tls -p ":38080" -C proxy.crt -K proxy.key`  
SOCKS5 second level proxy VPS_02,IP:33.33.33.33  
`./proxy socks -t tls -p ":28080" -T tls -P "22.22.22.22:38080" -C proxy.crt -K proxy.key`  
SOCKS5 third level proxy(local)  
`./proxy socks -t tcp -p ":8080" -T tls -P "33.33.33.33:28080" -C proxy.crt -K proxy.key`  
Then access to the local 8080 port is access to the proxy port 38080 above the SOCKS first level proxy.  
  
#### **5.5.SOCKS proxy traffic force to go to parent socks proxy**  
By default, proxy will intelligently judge whether a domain name can be accessed. If it cannot be accessed, it will go to parent SOCKS proxy. Through --always parameter, all SOCKS proxy traffic can be coercion to the parent SOCKS proxy.  
`./proxy socks --always -t tls -p ":28080" -T tls -P "22.22.22.22:38080" -C proxy.crt -K proxy.key`  
  
#### **5.6.Transfer through SSH**  
Explanation: the principle of SSH transfer is to take advantage of SSH's forwarding function, which is, after you connect to SSH, you can access the target address by the SSH.  
Suppose there is a vps  
- IP is 2.2.2.2, SSH port is 22, SSH username is user, SSH password is Demo
- The SSH private key name of the user is user.key   

##### ***5.6.1.The way of username and password***  
Local SOCKS5 proxy 28080 port, execute:  
`./proxy socks -T ssh -P "2.2.2.2:22" -u user -A demo -t tcp -p ":28080"`  
##### ***5.6.2.The way of username and key***  
Local SOCKS5 proxy 28080 port, execute:  
`./proxy socks -T ssh -P "2.2.2.2:22" -u user -S user.key -t tcp -p ":28080"`  

Then access to the local 28080 port is to access the target address through VPS.  

#### **5.7.Authentication**  
For socks5 proxy protocol we can use username and password authentication, username and password authentication can be specified on the command line.  
`./proxy socks -t tcp -p ":33080" -a "user1:pass1" -a "user2:pass2"`  
If you need multiple users, repeat the -a parameters.   
You can also be placed in a file, which is a line, a ‘username: password’, and then specified in -F.  
`./proxy socks -t tcp -p ":33080" -F auth-file.txt`  

In addition, socks5 proxy also integrates external HTTP API authentication, we can specify a http url interface address through the --auth-url parameter,  
Then when the user is connected, the proxy GET request this url, with the following four parameters, if the return HTTP status code 204, on behalf of the authentication is successful.  
In other cases, the authentication fails.  
for example:  
`./proxy socks -t tcp -p ":33080" --auth-url "http://test.com/auth.php"`  
When the user is connected, the proxy will request this URL ("http://test.com/auth.php") by GET way.  
With user, pass, IP, three parameters:  
http://test.com/auth.php?user={USER}&pass={PASS}&ip={IP}  
user:username  
pass:password  
ip: user's IP, for example: 192.168.1.200  

If there is no -a or -F or --auth-url parameters, it means to turn off the authentication.    

#### **5.8.KCP protocol transmission**  
The KCP protocol requires a -B parameter to set a password to encrypt and decrypt data.  

HTTP first level proxy(VPS,IP:22.22.22.22)  
`./proxy socks -t kcp -p ":38080" -B mypassword`  
  
HTTP two level proxy(local os is Linux)  
`./proxy socks -t tcp -p ":8080" -T kcp -P "22.22.22.22:38080" -B mypassword`  
Then access to the local 8080 port is access to the proxy port 38080 on the VPS, and the data is transmitted through the KCP protocol.  

#### **5.9.view help**  
`./proxy help socks`  

### TODO  
- Welcome adding group feedback...

### How to use the source code?   
use command cd to enter your go SRC directory and then git clone https://github.com/snail007/goproxy.git and execute ./proxy.   
Direct compilation: go build     
execution: go run *.go    
Utils is a toolkit, and service is a specific service class.  

### License  
Proxy is licensed under GPLv3 license.  
### Contact  
QQ exchange group:189618940  
  
  
  