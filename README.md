# nvjdc

Net core5  vue3 puppeteer sharp的一次尝试

## 提示

Third party extension interface for sillyGirl.
https://github.com/ufuckee/jd_cookie

环境：centos x86

## 就是个文档，请不要Fork

## 安装教程 

# [1.2之前版本安装](#1)

## 小白一键快捷启动docker方式的最后版本 $ 1.1  或者  [dockr 部署](#1)
root 运行脚本，按提示输入自己的参数即可

```
bash <(curl -sL https://git.io/JMWTL)
```

# 1.2及之后版本安装

如果你是装过旧版本 nvjdc 先看看后面  * [1.2以前如何更新至1.2](#2) 升级说明

1、拉源码

国内
```
git clone -b main https://ghproxy.com/https://github.com/King-stark/NvJDCloud.git ~/nvjdc
```
国外
```
git clone -b main https://github.com/King-stark/NvJDCloud.git ~/nvjdc
```

2、拉取基础镜像以后不需要拉取镜像了 如果需要拉取我会通知

```
docker pull nolanhzy/nvjdc:latest
```

3、执行命令

```
yum install wget unzip -y
```

4、创建一个目录放配置

```
cd nvjdc
```
```
mkdir -p  Config && cd Config
```

5、下载Config.json 配置文件 并且修改自己的配置 不能缺少

```
wget -O Config.json  https://raw.githubusercontent.com/King-stark/NvJDCloud/doc/Config.json
```
国内请使用
 ```
wget -O Config.json  https://ghproxy.com/https://raw.githubusercontent.com/King-stark/NvJDCloud/doc/Config.json
```

6、回到 nvjdc 目录创建chromium文件夹并进入

```
cd ~/nvjdc && mkdir -p  .local-chromium/Linux-884014 && cd .local-chromium/Linux-884014
```

7、下载 chromium 

```
wget https://mirrors.huaweicloud.com/chromium-browser-snapshots/Linux_x64/884014/chrome-linux.zip && unzip chrome-linux.zip
```

8、删除刚刚下载的压缩包 

```
rm  -f chrome-linux.zip
```

9、回到nvjdc主目录

```
cd  ~/nvjdc
```


10、启动镜像

```
docker run   --name nvjdc -p 5701:80 -d  -v  "$(pwd)":/app \
-v /etc/localtime:/etc/localtime:ro \
-it --privileged=true  nolanhzy/nvjdc:latest
```

11、查看 日志 

```
docker logs -f nvjdc
```

出现 NETJDC  started 即可 


## <h2 id="2">1.2以前如何更新至1.2</h2>
如果你是装过NVjdc 并且存在nolanjdc 文件夹

并且你的浏览器和配置已经在nolanjdc文件夹下了

请你将你现有的nolanjdc更换名称 如nolanjdcdb
```
mv ~/nolanjdc /root/nolanjdcdb
```

然后执行步骤一 拉取代码
国内
```
git clone -b main https://ghproxy.com/https://github.com/King-stark/NvJDCloud.git ~/nvjdc
```
国外
```
git clone -b main https://github.com/King-stark/NvJDCloud.git ~/nvjdc
```


然后将刚刚更换名称文件夹 如nolanjdcdb中的 配置文件放到nvjdc/Config 文件夹中
```
 cd ~/nvjdc &&  mkdir -p  Config &&  mv ~/nolanjdcdb/Config.json ~/nvjdc/Config/Config.json
```

将刚刚更换名称文件夹 如nolanjdcdb 中的浏览器所有文件放到~/nvjdc/.local-chromium/Linux-884014 文件夹中
```
 cd ~/nvjdc &&  mv ~/nolanjdcdb/.local-chromium ~/nvjdc/.local-chromium
```

删除容器
```
docker rm -f nolanjdc 
```
然后从步骤9开始即可

后续更新只需要按照下方代码更新即可


## 更新

```
cd ~/nvjdc
```
```
docker stop nvjdc
```
```
git pull
```
```
docker start nvjdc
```


# <h2 id="1">1.1及以下 docker 版本安装</h2>

1 拉镜像

```
sudo docker pull clearloves/nvjdc:1.1   --（输入选择想要的 tar ）
```

2 部署容器

```
sudo docker run -dit \
  -v $PWD/nvjdc/Config:/app/Config \
  -v $PWD/nvjdc/.local-chromium:/app/.local-chromium \
  -p 5701:80 \
  --privileged=true \
  --name nvjdc \
  --hostname nvjdc \
  --restart always \
  nolanhzy/nvjdc:1.1
```
3、下载config.json 配置文件 并且修改自己的配置 不能缺少

```
cd ~/nvjdc/Config
```
```
wget -O Config.json  https://raw.githubusercontent.com/King-stark/NvJDCloud/doc/Config.json
```
国内请使用
```
wget -O Config.json  https://ghproxy.com/https://raw.githubusercontent.com/King-stark/NvJDCloud/doc/Config.json
```

3 查看 日志

```
docker logs -f nvjdc 
```

出现 NETJDC  started 即可

## 更新

停止容器

```
docker stop nvjdc 
```

删除容器

```
docker rm -f nvjdc 
```

删除镜像

```
docker rmi -f nolanhzy/nvjdc:1.1   --（输入选择想要的 tar ）
```

然后重复上面步骤即可

## 注意事项

容器启动后第一次获取验证码的时候可能卡住刷新一下即可

Config.json 是配置文件 可以热更新 修改后不用重启容器

## 最后

鸣谢：
原作 Nolanhzy
https://hub.docker.com/r/nolanhzy/nvjdc

备份 clearloves
https://hub.docker.com/r/clearloves/nvjdc



## 特别声明:

* 本仓库涉仅用于测试和学习研究，禁止用于商业用途，不能保证其合法性，准确性，完整性和有效性，请根据情况自行判断.
* 本项目内所有资源文件，禁止任何公众号、自媒体进行任何形式的转载、发布。
* 本人对任何代码问题概不负责，包括但不限于由任何脚本错误导致的任何损失或损害.
* 间接使用本仓库搭建的任何用户，包括但不限于建立VPS或在某些行为违反国家/地区法律或相关法规的情况下进行传播, Nolan对于由此引起的任何隐私泄漏或其他后果概不负责.
* 请勿将本项目的任何内容用于商业或非法目的，否则后果自负.
* 如果任何单位或个人认为该项目的脚本可能涉嫌侵犯其权利，则应及时通知并提供身份证明，所有权证明，我们将在收到认证文件后删除相关代码.
* 任何以任何方式查看此项目的人或直接或间接使用本仓库项目的任何脚本的使用者都应仔细阅读此声明。Nolan 保留随时更改或补充此免责声明的权利。一旦使用并复制了任何本仓库项目的规则，则视为您已接受此免责声明.

**您必须在下载后的24小时内从计算机或手机中完全删除以上内容.**  </br>

> ***您使用或者复制了本仓库且本人制作的任何脚本，则视为`已接受`此声明，请仔细阅读***

## 多谢
