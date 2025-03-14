### 群晖DDNS设置

> [!TIP]
作者：John Wei
链接：https://www.zhihu.com/question/515648497/answer/2364008242
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

一般情况下，自架的群晖服务器由于缺少固定的IP地址（这里指公有IP地址，如果没有公网IP，则可能需要采用内网穿透等方式才能在外部访问群晖服务器），需要依赖动态域名解析（DDNS）服务来保证域名的动态更新，这样，在外部IP地址发生变化时，可以通过DDNS服务及时将域名解析到新的IP地址上。但是群晖自带的DDNS默认更新频率（大约）是24小时，这导致如果网络服务商更换了IP地址，可能导致长时间无法访问服务器，为解决这一问题，可以考虑使用群晖内置的计划任务定时执行DDNS更新，这样可以缩短服务器外部IP变化时引起服务器无法访问的情况。在DSM7.0的控制面板，计划任务中，选择新增任务，任务名称可以随便填写，这里写DDNS update，用户需要切换为root，见下图：<img src="https://pic1.zhimg.com/50/v2-acf150bb005709f40e7dc0fdf6b1841b_720w.jpg?source=1def8aca" data-caption="" data-size="normal" data-rawwidth="1627" data-rawheight="817" data-original-token="v2-a1141b3ad51bbf203b00eaac266b5b52" class="origin_image zh-lightbox-thumb" width="1627" data-original="https://picx.zhimg.com/v2-acf150bb005709f40e7dc0fdf6b1841b_r.jpg?source=1def8aca"/><img src="https://pica.zhimg.com/50/v2-713c1bdca71d50fe987994cceb4153b8_720w.jpg?source=1def8aca" data-caption="" data-size="normal" data-rawwidth="540" data-rawheight="609" data-original-token="v2-e8e7ef9d694e7bfd27e72814fb4cb5e7" class="origin_image zh-lightbox-thumb" width="540" data-original="https://pic1.zhimg.com/v2-713c1bdca71d50fe987994cceb4153b8_r.jpg?source=1def8aca"/>在“计划”选项中，选择运行的频率，为了提高计划任务更新频率，可以将运行频率设置为每30分钟，或者1~2个小时，这样可以及时更新IP地址。<img src="https://picx.zhimg.com/50/v2-23abd34f26d83de18a7d6a9c9ffd9889_720w.jpg?source=1def8aca" data-caption="" data-size="normal" data-rawwidth="661" data-rawheight="705" data-original-token="v2-27470c0a45e04db414e20e17a9de8399" class="origin_image zh-lightbox-thumb" width="661" data-original="https://pic1.zhimg.com/v2-23abd34f26d83de18a7d6a9c9ffd9889_r.jpg?source=1def8aca"/>在任务设置中，用户定义的脚本，输入以下命令。也可以输入电子邮件地址，以便在运行发生错误时提醒管理员。synonet --dns update <img src="https://picx.zhimg.com/50/v2-15f74dc69aade8b0f5a76b55ced6fbf8_720w.jpg?source=1def8aca" data-caption="" data-size="normal" data-rawwidth="656" data-rawheight="712" data-original-token="v2-ec5b145f80bf9f733af192a574799e9d" class="origin_image zh-lightbox-thumb" width="656" data-original="https://picx.zhimg.com/v2-15f74dc69aade8b0f5a76b55ced6fbf8_r.jpg?source=1def8aca"/>

### 设置群晖反向代理服务器

> [!TIP]
来源：知乎
连接：https://zhuanlan.zhihu.com/p/453549877

![Image](https://github.com/user-attachments/assets/fd5dc4be-6112-4b25-af66-35e84230cb76)

由于很多地方的宽带80/443端口被封，所以无法做到无端口号访问nas服务。我一开始就想那利用反向代理服务的二级域名+端口和直接用自己的群晖域名+端口有啥区别？后来貌似想明白了，因为群晖服务变多后，端口号也相应的增加，总会记不住一些服务的端口号。所以可以利用反向代理服务统一一个好记的端口号，只改变前面的二级域名就行了。比如：[photo.xxx.com:666](https://link.zhihu.com/?target=http%3A//photo.xxx.com%3A666) video.xxx.com:666

废话不多说，开始！

首先我们打开域名DNS控制台（我的是腾讯云，别的平台操作类似）


添加一条CNAME记录

主机记录填kindle（就是二级域名kindle.xxxx.xyz的前缀）

记录类型选CNAME

记录值填写我们用作DDNS的那条二级域名，我这里是www.xxxx.xyz(这里一定要注意，和ddns那条主机记录名称要一致！！）

CNAME记录的意思就是，这条记录直接指向现有域名。

我们指向了用作DDNS的那条二级域名，访问CNAME记录域名的结果就和访问所指向域名是一样的（都是访问你的公网IP）。

下面开始设置群晖。

打开群晖的控制面板-登录门户-高级-反向代理服务器

规则很好理解，就是把上方来源处的域名+端口指向下方目的地的IP（域名）+端口

按照我的预想来配置，就是把kindle.xxx.xyz这个二级域名通过666端口，指向旁路由的服务IP192.168.2.15+端口。

目的地的填写规则，以旁路由为例。我们可以通过http协议访问，也可以通过https协议访问。如果是http协议访问，规则就选http 192.168.3.2 端口80；如果是https协议访问，规则就选https 192.168.3.2 端口443，都可以实现访问。(说简单点，就是你想http访问就http你想加密https就勾选协议的https）

1 2 3按步骤添加websocket，避免各种疑难杂症。

点确定。群晖端设置完毕！

最后路由器端口转发一下666这个端口就可以访问了！