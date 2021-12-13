# nvjdc安装教程   就是个文档，偶尔更改，请不要Fork
## 好消息！最新版本的nvjdc支持Arm了
* 目录 点击跳转你需要的安装方式
* [Windows安装教程](#7)
* [1.1及之前纯docker版本安装](#1)
* [1.1及以前如何升级至新版本](#3)
* [新版本安装](#2)
* [新版更新方式](#4)
* [Arm 安装教程](#5)
* [Arm 更新方式](#6)

## 注意事项

容器启动后第一次获取验证码的时候可能卡住刷新一下即可

Config.json 是配置文件 仅1.1及之前版本支持热更新 新版本每次修改后需要重启容器

环境：centos x86 arm

Third party extension interface for sillyGirl.
https://github.com/ufuckee/jd_cookie


# 安装教程开始

# <h2 id="1">1.1及之前纯docker版本安装</h2>

## 推荐 小白一键快捷启动 docker方式的最终版本 1.1

root运行脚本，按提示输入自己的参数即可

```
bash <(curl -sL https://git.io/JMWTL)
```

## 1.1及以下docker版本 命令安装

1 拉镜像

```
sudo docker pull clearloves/nvjdc:1.1   --（输入选择想要的 tag 仅限1.1及以下，推荐使用一键脚本安装最终版本 1.1 ）
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
  clearloves/nvjdc:1.1
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
docker restart nvjdc
```
```
docker logs -f nvjdc 
```

出现 NETJDC  started 即可

# <h2 id="2">新版本安装</h2>

如果你是装过旧版本 nvjdc 先看看后面 [1.1及以前如何升级至新版本](#3) 升级说明

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

3、没有wget工具请执行如下命令，否则跳过

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
wget http://npm.taobao.org/mirrors/chromium-browser-snapshots/Linux_x64/884014/chrome-linux.zip && unzip chrome-linux.zip
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


## <h2 id="3">1.1以前如何升级至新版本</h2>
如果你是装过Nvjdc 并且存在nolanjdc 或 nvjdc文件夹

并且你的Config.json和chromium已经在nolanjdc 或 nvjdc文件夹下了

请你将你现有的nolanjdc或nvjdc文件夹重命名 如nolanjdcdb,以下均以原文件夹名为nolanjdc演示
```
mv ~/nolanjdc ~/nolanjdcdb
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


然后将刚刚重命名的文件夹 如nolanjdcdb中的Config.json放到nvjdc/Config 文件夹中
```
 cd ~/nvjdc &&  mkdir -p  Config &&  mv ~/nolanjdcdb/Config.json ~/nvjdc/Config/Config.json
```

将刚刚更换名称文件夹 如nolanjdcdb 中的chromium所有文件放到~/nvjdc/.local-chromium/Linux-884014 文件夹中
```
 cd ~/nvjdc &&  mv ~/nolanjdcdb/.local-chromium ~/nvjdc/.local-chromium
```

删除容器
```
docker rm -f nolanjdc 
```
然后从步骤9开始即可

后续更新只需要按照下方代码更新即可

## <h2 id="4">新版本更新方式</h2>

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

# <h2 id="5">Arm 安装教程</h2>

1、拉源码

国内
```
git clone -b main https://ghproxy.com/https://github.com/King-stark/NvJDCloud.git ~/nvjdc
```
国外
```
git clone -b main https://github.com/King-stark/NvJDCloud.git ~/nvjdc
```

2、拉取基础镜像

```
docker pull nolanhzy/nvjdccaptcha:arm
```

3、运行基础镜像

```
docker run   --name nvjdccaptcha -p 5703:5000  --restart=always  -d   -it --privileged=true  nolanhzy/nvjdccaptcha:arm   
```

4、安装chromium-browser

```
apt-get install  chromium-browser
```

5、创建一个目录放配置
```
cd ~/nvjdc
```
```
mkdir -p  Config && cd Config
```

6、下载Config.json 配置文件 注意ARM多一个配置 Captchaurl 修改自己的配置
```
wget -O Config.json  https://raw.githubusercontent.com/King-stark/NvJDCloud/doc/Arm_Config.json
```
国内请使用
 ```
wget -O Config.json  https://ghproxy.com/https://raw.githubusercontent.com/King-stark/NvJDCloud/doc/Arm_Config.json
```

7、下载NET5.sh
```
 cd ~/nolanjdc && wget https://dot.net/v1/dotnet-install.sh && chmod 777 dotnet-install.sh
```

8、下载NET5
```
./dotnet-install.sh -c 5.0
```

9、设置 path
```
export PATH="$PATH:$HOME/.dotnet"
```
10、启动
```
nohup dotnet NETJDC.dll --urls=http://*:5701 1>"$(pwd)"/log 2>&1 & #ARM64
```

## <h2 id="6">Arm版更新</h2>
查询占用5701的端口进程  如果你的nvjdc是5701就查询 5701
```
netstat -lnp|grep 5701
```
假如显示如下内容
tcp6       0      0 :::5701                 :::*                    LISTEN      680536/dotnet  

杀死进程
```
kill -9 680536
```
```
cd /root/nolanjdc
```
```
git pull
```
```
export PATH="$PATH:$HOME/.dotnet"
```
```
nohup dotnet NETJDC.dll --urls=http://*:5701 1>"$(pwd)"/log 2>&1 & #ARM64
```
# <h2 id="7">Windows安装教程</h2>

* 1、安装ASP.NET Core Runtime 5.0.12

安装地址:https://dotnet.microsoft.com/download/dotnet/5.0
下载之后无脑下一步

* 2、下载当前项目源码解压

* 3、删除NETJDC.deps.json

* 4、根据自己系统将dll复制根目录即可

64位

复制runtimes\win-x64\native\OpenCvSharpExtern.dll到根目录

32位

复制runtimes\win-x86\native\OpenCvSharpExtern.dll到根目录

* 启动 

管理员打开CMD CD到源码文件夹中  输入 dotnet NETJDC.dll --urls=http://*:5000

后面那个是端口可以自己改
 

最后

鸣谢：
原作 Nolanhzy
https://hub.docker.com/r/nolanhzy/nvjdc

备份 clearloves
https://hub.docker.com/r/clearloves/nvjdc


# 特别声明:

* 本仓库涉仅用于测试和学习研究，禁止用于商业用途，不能保证其合法性，准确性，完整性和有效性，请根据情况自行判断.
* 本项目内所有资源文件，禁止任何公众号、自媒体进行任何形式的转载、发布。
* 本人对任何代码问题概不负责，包括但不限于由任何脚本错误导致的任何损失或损害.
* 间接使用本仓库搭建的任何用户，包括但不限于建立VPS或在某些行为违反国家/地区法律或相关法规的情况下进行传播, Nolan对于由此引起的任何隐私泄漏或其他后果概不负责.
* 请勿将本项目的任何内容用于商业或非法目的，否则后果自负.
* 如果任何单位或个人认为该项目的脚本可能涉嫌侵犯其权利，则应及时通知并提供身份证明，所有权证明，我们将在收到认证文件后删除相关代码.
* 任何以任何方式查看此项目的人或直接或间接使用本仓库项目的任何脚本的使用者都应仔细阅读此声明。Nolan 保留随时更改或补充此免责声明的权利。一旦使用并复制了任何本仓库项目的规则，则视为您已接受此免责声明.

**您必须在下载后的24小时内从计算机或手机中完全删除以上内容.**  </br>
> ***您使用或者复制了本仓库且本人制作的任何脚本，则视为`已接受`此声明，请仔细阅读***

# 多谢
