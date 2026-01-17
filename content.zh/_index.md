---
title: vless reality代理节点搭建教程
type: docs
---


## vless介绍

VLESS 是一个轻量级的代理协议，由 [V2Ray](https://en.wikipedia.org/wiki/V2Ray) 项目开发。它是 VMess 协议的简化版本。vless结构更简单，处理开销更小，依赖传输层（如 TLS）来提供加密保护，速度更快、cpu占用更小，支持多种传输方式包括：[TCP](https://en.wikipedia.org/wiki/Transmission_Control_Protocol)、mKCP、WebSocket、HTTP/2、gRPC 等，通常与 TLS 配合使用以确保安全性，支持回落（fallback）机制，可以伪装成正常网站。几乎所有的代理软件客户端都支持vless，比如[v2rayNG](https://getfreevpn.info/zh/docs/vpn%E6%95%99%E7%A8%8B/%E4%B8%8B%E8%BD%BD%E5%92%8C%E4%BD%BF%E7%94%A8v2rayNG-VPN/)、[v2box](https://v2box.pro/zh)、[hiddify](https://hiddify.me/zh)、[karing](https://karing.biz/zh)、[sing-box](https://sing-box.info/zh)、[shadowrocket](https://shadowrocket.ink/zh)和[stash](https://apps.apple.com/us/app/stash-rule-based-proxy/id1596063349)。

## vless reality代理节点搭建流程

### 1、vps介绍

首先，根据自己的需要，准备一台vps，比如台湾、美国、日本、香港等地的vps都可以，一般来说，距离所居住国家越近的vps往往速度越快。我搜集几家比较便宜的vps厂家，可以参考一下：

| 名称 | cpu | 内存 | 硬盘 | 月流量 | 优惠码 | 价格 |
|-----|-----|-----|-----|-----|-----|-----|
| racknerd | 1核 | 1G | 24G | 2T |  | [11.29美金/年](https://my.racknerd.com/index.php?rp=/store/new-year-specials&aff=6665) |
| hostdare | 1核 | 1.5G | 10G | 1T | DEAL50 | [12.99美金/年](https://bill.hostdare.com/aff.php?aff=3766&pid=113) |
| cloudcone | 2核 | 2G | 27G | 2T |  | [13.9美金/年](https://app.cloudcone.com.cn/vps/435/create?ref=11035&token=halloween-25-fs-ssd-vps-2) |
| rarecloud | 1核 | 768M | 15G | 1T | SNOWMICRO1072 | [10.72美金/年](https://rarecloud.io/clients/aff.php?aff=738&pid=1) |

### 2、购买vps

我们按照上面的价格，以rarecloud为例，购买vps，支持支付宝付款，使用上面提供的优惠代码，点击打开购买链接，
- 点击右上角，设置自己的语言
- 系统选择debian-12，地区选择日本或者罗马尼亚

![vless-1003.jpg](https://vless.app/img/vless-1003.jpg)
- 输入促销代码以后，可看到实际价格

![vless-1003.jpg](https://vless.app/img/vless-1001.jpg)

- 进入结算页面，可以选择支付方式paypal、支付宝、信用卡

![vless-1003.jpg](https://vless.app/img/vless-1002.jpg)

### 3、连接vps

- 付款成功以后
- 邮箱中会收到一份ip地址和密码的邮件，打开注册邮箱即可看到

![vless-1003.jpg](https://vless.app/img/vless-1004.jpg)



- 下载连接vps的软件：[点击下载finalshell](https://dl.hostbuf.com/finalshell3/finalshell_windows_x64.exe)
- [finalshell官方网站](https://www.hostbuf.com/t/988.html)
- 安装完成以后，打开软件，点做左上角的文件夹图标，会有弹窗出现
- 再点击弹窗左上角的图标，如图
- 选择SSH连接(linux）

![vless-1003.jpg](https://vless.app/img/vless-1005.jpg)

- 名称，随便写，主机，填入邮箱中的ip地址，用户名，写root，密码，填写邮箱中的密码
- 填写完毕以后，点击确定，即可快速连接

![vless-1003.jpg](https://vless.app/img/vless-1006.jpg)

- 连接成功以后，界面是这样的
- 至此，vps连接成功

![vless-1007.jpg](https://vless.app/img/vless-1007.jpg)





### 4、购买域名

- 打开网址：https://porkbun.com/
- 注册账号，登录，点击右上角，点击账户，选择域管理

![vless-1008.jpg](https://vless.app/img/vless-1008.jpg)

- 搜索，域名名称
- 找一个便宜点的，可以用支付宝付款

![vless-1009.jpg](https://vless.app/img/vless-1009.jpg)

- 付款成功以后，等待系统返回，不要关闭窗口，耐心等待
- 找到域名的dns选项

![vless-10091.jpg](https://vless.app/img/vless-10091.jpg)

- 在图中1的位置填入名称，比如3xui
- 在途中2的位置填入vps的ip地址，然后点击add



![vless-10092.jpg](https://vless.app/img/vless-10092.jpg)



### 5、安装3x-ui

- 打开finalshell，连接vps
- 以此执行下面两条命令
- 复制到命令行，按回车键即可，没有复杂操作

```
apt install curl
```

![vless-10093.jpg](https://vless.app/img/vless-10093.jpg)

```
VERSION=v2.5.5 && bash <(curl -Ls "https://raw.githubusercontent.com/mhsanaei/3x-ui/$VERSION/install.sh") $VERSION
```

- 出现下图的提示，按回车键即可

![vless-10094.jpg](https://vless.app/img/vless-10094.jpg)

- 之后会出现安装成功的提示
- 找到下图中出现的账号密码和url，保存，以后登录要用到

![vless-10095.jpg](https://vless.app/img/vless-10095.jpg)

### 6、申请域名证书

- 连接vps，执行命令

```
apt install certbot python3-certbot-nginx
```

- 执行命令

```
certbot --nginx -d 3xui.你的域名
```

- 比如你的域名是nihao.com，那么命令是：certbot --nginx -d 3xui.nihao.com
- 当然这个3xui是前面你自己设置的
- 执行结果是这样的，途中标注1的是公钥，标注2的是私钥

![vless-10097.jpg](https://vless.app/img/vless-10097.jpg)

### 7、配置3x-ui

- 打开谷歌浏览器，输入前面记录的url
- 如图输入前面记录的账号和密码

![vless-10098.jpg](https://vless.app/img/vless-10098.jpg)

- 点击右上角，面板设置
- 选择证书，输入前面申请的公钥和私钥

![vless-10099.jpg](https://vless.app/img/vless-10099.jpg)

- 输入完成以后，右上角点击保存，然后点击重启面板


![vless-100991.jpg](https://vless.app/img/vless-100991.jpg)

- 将原来的url中的ip地址，替换为自己的子域名
- 原来的url地址是这样的：http://我的ip地址:52983/TkH2Qe01Bore3k0
- 新的url地址是这样的：http://3xui.vless.app:52983/TkH2Qe01Bore3k0
- 访问新的url，输入原来的账号和密码
- 点击入站列表，点击添加入站

![vless-100992.jpg](https://vless.app/img/vless-100992.jpg)

- 在备注选项，随便写入名字

![vless-100993.jpg](https://vless.app/img/vless-100993.jpg)

- 点击下方，reality选项，再点击get new cert,如图
- 然后，点击添加

![vless-100994.jpg](https://vless.app/img/vless-100994.jpg)


- 这样一个vless reality节点就建立完成了
- 建立好的节点是这样的

![vless-100995.jpg](https://vless.app/img/vless-100995.jpg)

- 下面就是复制节点，导入节点
- 点击右边的小加号，点击二维码，点击二维码的中心，这样就复制了节点


![vless-100996.jpg](https://vless.app/img/vless-100996.jpg)

- 复制出来的节点是这样的，可以直接导入手机

```
vless://931884c4-494f-4f35-ae55-10ae38f3da95@bjly.mene.lol:53518?encryption=none&flow=xtls-rprx-vision&security=reality&sni=tesla.com&fp=random&pbk=zFZlzd84FwymBun_YXSLNNz83vGJnUGi_34doZWr3Ac&sid=b83ffb&spx=%2F&type=tcp&headerType=none#%E4%BF%9D%E5%8A%A0%E5%88%A9%E4%BA%9A--rea--%E5%AE%A2%E6%88%B7001%20-%20Cloned-200G
```

### 8、推荐机场

* 以下机场按照流量付费，网站里有软件的使用和安装教程
* 购买流量以后，不限制时间，流量用完为止
* 如果网站无法访问，则说明已经被墙，更换其他网站即可

| 名 称 | 价 格 | 流 量 | 节点数 |
| :--- | :--- | :--- | :--- |
| [北美机场](https://www.northamericanairport-official-mirror.hair/#/register?code=j2rr2X4T) | 10元 | 1000G | 35个 |
| [一元中转](https://yyzz.ink/#/register?code=mqini9Q0) | 12元 | 1年 | 40个 |
| [996云](https://dash.996cloud.top/#/register?code=WO0oVqnE) | 12元 | 1年 | 42个 |
| [一分](https://xn--4gqx1hgtfdmt.com/#/register?code=Aqr3awfK) | 12元 | 100G | 40个 |
| [牛逼](https://6666b.idsduf.com/#/login?code=sT9kLfc6) | 13元 | 200G | 41个 |
| [魔戒](https://mojie.xn--yrs494l.com/register?aff=BpCuERz0) | 15元 | 130G | 48个 |
| [speedy](https://cloud.speedypro.xyz/#/register?code=RTSPWuvE) | 15元 | 100G | 42个 |
| [农夫山泉](https://www.nfsq.us/#/register?code=i1fXTMYk)    | 15元   | 200G |32个|
| [网际快车](https://wjkc66.vip?c=REZUOC) | 16元 | 100G | 54个 |
| [赔钱机场](https://www.xn--mes358aby2apfg.site/register?code=OufF6cCL) | 19元 | 1000G | 37个 |
| [kitty](https://kitty.su/#/register?code=FodKng1b) | 24元 | 1年 | 42个 |
| [渔云机场](https://cloudfisher.net/web/#/login?code=NatdlqpR) | 40元 | 300G | 32个 |
| [ofopp](https://kk.ofopp.net/#/register?code=A2UmuXR8) | 40元 | 100G | 70个 |
| [超实惠](https://cshjc.shop/register?code=GadIbTHc) | 51元 | 666G | 40个 |
| [宝贝云](https://web1.bby011.com/#/register?code=8xTTMr2f) | 55元 | 600G | 64个 |
| [千速猫](https://tmsreta.top/#/register?code=mmgD0jY7) | 68元 | 512G | 46个 |
| [奈云](https://www.v2ny.me?path=register&code=05XjPGu5) | 98元 | 280G | 140个 |
| [墨菲云](https://portal.mofeiyun.com/#/register?code=ugmD3VWT) | 0.5元 | 100G | 33个 |

- 关于安卓手机和苹果手机如何导入节点，可以看这里
- [安卓手机v2rayng购买和导入节点教程](https://v2rayng.4566.lol/zh)
- [苹果手机shadowrocket购买和导入节点教程](https://shadowrocket.4566.lol/zh)
- 如有任何问题，请发邮件：[leeulen60@gmail.com](leeulen60@gmail.com)







