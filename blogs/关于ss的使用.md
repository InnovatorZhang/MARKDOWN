---
title: 关于$hadow$ocks在ubuntu上的安装与使用
date: 2018-05-29 21:05:14
tags: ubuntu
---

# 关于$hadow$ocks

## 重新安装SS的原因

    今天重装了一次$hadow$ocks,因为开始是直接用的 sudo apt-get install shadowsocks命令直接装的,
    并且也没什么问题，因为开始一直是用的别人的￥hadow$ocks服务器和账号，
    他是使用的aes-256-cfb方式加密，而我自己的服务器使用的chacha20-ietf-poly1305方式加密。
    而我在ubuntu上安装的SS不支持chacha20-ietf-poly1305加密，所以选择使用python pip安装支持的SS版本

## 这里写一写ubuntu中apt-get的默认安装路径

    apt-get的安装路径在我的电脑中是/var/cache/apt/archives这个目录；
    apt-get install安装目录是包的维护者确定的，不是用户；

    ubuntu系统的最原始的PATH为/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin；
    系统安装软件一般在/usr/share，可执行的文件在/usr/bin，配置文件可能安装到了/etc下等；
    文档一般在 /usr/share；
    可执行文件 /usr/bin；
    配置文件 /etc；
    lib文件 /usr/lib；

    
    所以我一开始用apt-get装的$hadow$socks就在/var/cache/apt/archives/目录下；
    然后使用pip装的$hadow$ocks装的就在/usr/local/lib/python2.7/dist-packages/目录下；

## 插入一点关于软件安装位置的知识

> 例如安装jdk
>> 如果你认为jdk是系统提供给你可选的程序，放在opt里
如果你认为这是你个人行为，自主安装的，放在usr/local里，具体是usr/local/lib
如果你觉得jdk对你来说是必不可少的运行库，放在lib里
上面三句是最开始的想法，
其实我也想找出一个最佳实践，后来看了看linux的目录结构，发现就算是同一个东西，系统自带和你手动安装，就不应该在同一个目录里。同样是浏览器，系统自带的firefox就在/usr/lib里，而后来通过软件包安装的chrome就在/opt里。
如果系统自带java，我觉得他会在lib里或者/usr/lib，看它对java的定义是必需的库还是
如果能在软件管理器里安装，那么会安装在/usr/lib
如果oracle给你的是deb，那么会被安装在opt
所以自己安装，就要放在/usr/local/lib里比较合适了


## ss的安装
    
### 第一种

#### 如果你是ubuntu 16.04或以上的直接可以执行

```
sudo apt install shadowsocks
```

### 第二种（通过pip安装）

```
sudo apt-get update
sudo apt-get install python-pip
sudo apt-get install python-setuptools m2crypto
```

## ss的使用

### 通过配置文件使用

> 因为我将配置文件放在了/home/zhang/OverWall/$hadow$ocks.json 所以每次使用的命令为sslocal -c /home/zhang/OverWall/shadowsocks.json
>> 配置文件的内容
>>> 格式为json
>>>> ```json
{
"server": "120.44.33.22",
"server_port": 443,
"local_port": 2080,
"password": "sdsgdfgdfg",
"timeout": 300,
"method": "chacha20-ietf-poly1305"
}
```

### 通过参数配置使用

比如：
------

```
sslocal -s 11.22.33.44 -p 50003 -k "123456" -l 1080 -t 600 -m aes-256-cfb
```

参数代表的意思：
----------------
```
-s表示服务IP, -p指的是服务端的端口，-l是本地端口默认是1080, -k 是密码（要加” ”）, -t超时默认300,-m是加密方法默认aes-256-cfb
```

## 配置Google浏览器

参考资料：[ubuntu使用$hadow$ocks](https://www.sundabao.com/ubuntu%E4%BD%BF%E7%94%A8shadowsocks/)






























    

  


