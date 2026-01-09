---
title: VLESS Reality Proxy Node Setup Tutorial
type: docs
---

## Introduction to VLESS

VLESS is a lightweight proxy protocol developed by the [V2Ray](https://en.wikipedia.org/wiki/V2Ray) project. It is a simplified version of the VMess protocol. The VLESS structure is simpler, with lower processing overhead, relying on the transport layer (such as TLS) for encryption protection. It provides faster speed, lower CPU usage, and supports multiple transport methods including [TCP](https://en.wikipedia.org/wiki/Transmission_Control_Protocol), mKCP, WebSocket, HTTP/2, and gRPC. It is usually used with TLS for security and supports a fallback mechanism that can disguise the proxy as a normal website. Almost all proxy clients support VLESS, such as [v2rayNG](https://getfreevpn.info/zh/docs/vpn%E6%95%99%E7%A8%8B/%E4%B8%8B%E8%BD%BD%E5%92%8C%E4%BD%BF%E7%94%A8v2rayNG-VPN/), [v2box](https://v2box.pro/), [hiddify](https://hiddify.me/), [karing](https://karing.biz/), [sing-box](https://sing-box.info/), [shadowrocket](https://shadowrocket.ink/), and [stash](https://apps.apple.com/us/app/stash-rule-based-proxy/id1596063349).

## Steps to Set Up a VLESS Reality Proxy Node

### 1. VPS Introduction

First, prepare a VPS based on your needs. VPS from regions like Taiwan, the U.S., Japan, or Hong Kong are all fine. Generally, the closer the VPS is to your location, the faster the speed. Below are several affordable VPS providers for your reference:

| Name | CPU | RAM | Disk | Bandwidth | Coupon | Price |
|------|-----|-----|------|------------|---------|--------|
| hostdare | 1 Core | 768MB | 10G | 500G | B7H52ZQR1Z | [\$26/year](https://bill.hostdare.com/aff.php?aff=3766&pid=113) |
| cloudcone | 2 Core | 2G | 27G | 2T |  | [\$13.9/year](https://app.cloudcone.com.cn/vps/435/create?ref=11035&token=halloween-25-fs-ssd-vps-2) |
| lightlayer | 1 Core | 1G | 50G | 1T |  | [\$25/year](https://account.lightlayer.net/?cmd=cart&action=add&affid=677&id=363) |
| rarecloud | 1 Core | 768MB | 15G | 1T | SLICEDHALF50 | [\$20/year](https://rarecloud.io/clients/aff.php?aff=738&pid=16) |

### 2. Purchase a VPS

Using **rarecloud** as an example:
- Supports Alipay payment.
- Use the coupon code provided above.
- Set language preference, select **Debian 12**, and choose **Japan** or **Romania** as the location.

![vless-1003.jpg](https://vless.app/img/vless-1003.jpg)

After entering the promo code, you’ll see the discounted price.

![vless-1001.jpg](https://vless.app/img/vless-1001.jpg)

Proceed to checkout, and you can pay via PayPal, Alipay, or credit card.

![vless-1002.jpg](https://vless.app/img/vless-1002.jpg)

### 3. Connect to VPS

- After successful payment, you’ll receive an email containing the VPS IP and password.

![vless-1004.jpg](https://vless.app/img/vless-1004.jpg)

- Download [FinalShell](https://dl.hostbuf.com/finalshell3/finalshell_windows_x64.exe) and install it.  
- [FinalShell Official Website](https://www.hostbuf.com/t/988.html)
- Open the program → click the folder icon on the top left → select **SSH Connection (Linux)**.

![vless-1005.jpg](https://vless.app/img/vless-1005.jpg)

- Enter:
  - Name: any
  - Host: VPS IP from email
  - Username: root
  - Password: password from email  
- Click **OK** to connect.

![vless-1006.jpg](https://vless.app/img/vless-1006.jpg)

Once connected successfully, you’ll see the VPS interface.

![vless-1007.jpg](https://vless.app/img/vless-1007.jpg)

### 4. Purchase a Domain Name

- Go to [https://porkbun.com/](https://porkbun.com/)
- Register and log in.
- Navigate to your **Domain Management** section.

![vless-1008.jpg](https://vless.app/img/vless-1008.jpg)

Search for a cheap domain and pay via Alipay.

![vless-1009.jpg](https://vless.app/img/vless-1009.jpg)

After successful payment, locate the **DNS** settings.

![vless-10091.jpg](https://vless.app/img/vless-10091.jpg)

- Enter a subdomain name (e.g., `3xui`)
- Enter your VPS IP address in the value field and click **Add**.

![vless-10092.jpg](https://vless.app/img/vless-10092.jpg)

### 5. Install 3x-ui

Connect to your VPS via FinalShell and run the following commands:

```
apt install curl
```

![vless-10093.jpg](https://vless.app/img/vless-10093.jpg)

```
VERSION=v2.5.5 && bash <(curl -Ls "https://raw.githubusercontent.com/mhsanaei/3x-ui/$VERSION/install.sh") $VERSION
```

Press **Enter** when prompted.

![vless-10094.jpg](https://vless.app/img/vless-10094.jpg)

After installation, note down the **username, password, and URL** for later login.

![vless-10095.jpg](https://vless.app/img/vless-10095.jpg)

### 6. Apply for a Domain Certificate

Run the following commands:

```
apt install certbot python3-certbot-nginx
```

Then:

```
certbot --nginx -d 3xui.yourdomain.com
```

Replace `yourdomain.com` with your actual domain.

![vless-10097.jpg](https://vless.app/img/vless-10097.jpg)

### 7. Configure 3x-ui

Open Chrome and enter the URL you saved earlier.

![vless-10098.jpg](https://vless.app/img/vless-10098.jpg)

Go to **Panel Settings → Certificate**, enter your certificate and private key, then click **Save** and **Restart Panel**.

![vless-10099.jpg](https://vless.app/img/vless-10099.jpg)

Now replace the IP in the original URL with your subdomain:
- Old: `http://your.ip.address:52983/...`
- New: `http://3xui.yourdomain.com:52983/...`

Access the new URL, log in, and go to **Inbound List → Add Inbound**.

![vless-100992.jpg](https://vless.app/img/vless-100992.jpg)

Enter a name for your inbound.

![vless-100993.jpg](https://vless.app/img/vless-100993.jpg)

Under **Reality**, click **Get new cert**, then **Add**.

![vless-100994.jpg](https://vless.app/img/vless-100994.jpg)

Your VLESS Reality node is now set up successfully!

![vless-100995.jpg](https://vless.app/img/vless-100995.jpg)

You can copy the node by clicking the QR code button and scanning or copying it.

![vless-100996.jpg](https://vless.app/img/vless-100996.jpg)

Example node configuration:

```
vless://931884c4-494f-4f35-ae55-10ae38f3da95@bjly.mene.lol:53518?encryption=none&flow=xtls-rprx-vision&security=reality&sni=tesla.com&fp=random&pbk=zFZlzd84FwymBun_YXSLNNz83vGJnUGi_34doZWr3Ac&sid=b83ffb&spx=%2F&type=tcp&headerType=none#Poland--rea--Client001%20-%20Cloned-200G
```

### Recommended Proxy Providers

If setting up your own node is too complicated, here are some affordable proxy service providers.

* These providers charge based on data usage.
* Tutorials for software installation and use are available on their websites.
* No time limit — valid until your data quota runs out.

| Name | Price | Data | Nodes |
|------|--------|--------|--------|
| [Nongfu Spring](https://www.nfsq.us/#/register?code=RaUmorb2) | ¥15 | 200G | 30 |
| [Mojie](https://mojie.xn--yrs494l.com/register?aff=BpCuERz0) | ¥15 | 130G | 48 |
| [Pikachu](https://pkhub.net/#/register?code=A6O9EIj0) | ¥4.5 | 10G | 42 |
| [WJKC Express](https://wjkc66.vip?c=REZUOC) | ¥7 | 20G | 54 |
| [Top VPN](https://xn--mes358a9urctx.com/#/register?code=bnWsDzhG) | ¥12 | 200G | 43 |
| [NB VPN](https://6666b.idsduf.com/#/login?code=sT9kLfc6) | ¥13 | 200G | 41 |
| [Super Saver](https://cshjc.shop/register?code=GadIbTHc) | ¥34 | 666G | 40 |
| [Baby Cloud](https://web1.bby011.com/#/register?code=8xTTMr2f) | ¥55 | 600G | 64 |
| [Free Cat](https://us.freecat.cc/register?code=czdF7PXY) | ¥50 | 500G | 90 |
| [Naiyun](https://www.v2ny.me?path=register&code=05XjPGu5) | ¥98 | 280G | 140 |
| [Yifen](https://xn--4gqx1hgtfdmt.com/#/register?code=Aqr3awfK) | ¥20 | 1000G | 40 |

For tutorials on importing nodes:
- [Android (v2rayNG) Tutorial](https://v2rayng.4566.lol/)
- [iOS (Shadowrocket) Tutorial](https://shadowrocket.4566.lol/)

If you have any questions, contact: [leeulen60@gmail.com](mailto:leeulen60@gmail.com)
