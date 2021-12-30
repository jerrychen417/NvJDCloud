<div align="center">
<h1>Nolanjdc：Arm 诺兰 安装问题集</h1>
  
测试环境：Ubuntu 20.04.3 LTS
</div>


>### 1、运行 NET5 WebApi 出现 The type initializer for 'Gdip' threw an exception. 报错解决办法

![示例图片1](https://raw.githubusercontent.com/King-stark/NvJDCloud/doc/screenshots/%E7%A4%BA%E4%BE%8B1.png)

运行含图片处理时发生异常，解决方式：
```
apt-get install libgdiplus  -y
```
然后重启 诺兰 
