# ubuntu-Android-studio
ubuntu Android studio
这年头，没有梯子真的是无法生存，连个android SDK都更新不了,好吧，接下来安装shadowsocks-qt5

sudo add-apt-repository ppa:hzwhuang/ss-qt5
sudo apt-get update
sudo apt-get install shadowsocks-qt5

适用于ubuntu14.04 及以上，全部说明请看https://github.com/shadowsocks/shadowsocks-qt5/wiki/%E5%AE%89%E8%A3%85%E6%8C%87%E5%8D%97
安装完以后chrome+SwitchySharp是可以科学上网的，但是ubuntu居然不支持shadowsocks的代理（实测LinuxMint是支持的）,android studio 也不支持，所以就需要另一个小软件：polipo,通过它把shadowsocks的 socks5代理转换成http代理
安装
sudo apt-get install polipo
配置
`sudo gedit /etc/polipo/config'
用以下内容替换（just copy）

# This file only needs to list configuration variables that deviate
# from the default values.  See /usr/share/doc/polipo/examples/config.sample
# and "polipo -v" for variables you can tweak and further information.

logSyslog = true
logFile = /var/log/polipo/polipo.log

proxyAddress = "0.0.0.0"

socksParentProxy = "127.0.0.1:1080"
socksProxyType = socks5

chunkHighMark = 50331648
objectHighMark = 16384

serverMaxSlots = 64
serverSlots = 16
serverSlots1 = 32

重启服务使生效
sudo /etc/init.d/polipo restart
测试

export http_proxy="http://127.0.0.1:8123/"
curl  ifconfig.me

如果正常的话，会返回SS当前连接的服务器的地址
下一步是配置android studio的代理
