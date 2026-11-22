---
title: "VLESS + Reality Anti-Blocking Setup Guide: Baota + 3X-UI “Steal Yourself” Complete Tutorial (2026)"
description: "Step-by-step guide to building a high-camouflage VLESS + Reality node using Baota Panel + 3X-UI. Uses the “steal yourself” method combining a real website with Reality to reduce detection risk, plus AI residential IP routing and technical explanations."
keywords:
  - VLESS Reality setup
  - 3X-UI Reality
  - Baota 3X-UI
  - Reality anti-block
  - steal yourself Reality
  - VLESS node tutorial
  - Reality camouflage
  - 3X-UI tutorial
weight: 10
---

# Nodes Keep Getting TCP Blocked? The Correct Way to Set Up Reality: Baota + 3X-UI “Steal Yourself” In-Depth Guide

Recently many users have encountered a strange issue: the server can be pinged and UDP works normally, but all new TCP connections (even SSH) are interrupted. Many people suspect that the Reality protocol has failed, but that is not the case — the problem often lies in a “shortcut” setup method that fails to fully utilize Reality’s camouflage capabilities.

![vless-3xui-feng1001.png](https://vless.app/img/vless-3xui-feng1001.png)

The first half of this tutorial walks you through building a high-camouflage “steal yourself” Reality node using **Baota Panel + 3X-UI** (including an AI residential IP routing solution). The second half thoroughly explains the technical principles behind each step.

---

## 1. Practical Tutorial: Building a “Steal Yourself” Reality Node from Scratch

### Step 1: Prepare the Server and Reinstall a Clean System

Prepare an overseas VPS. To ensure a clean environment, it is recommended to shut down the server in the control panel and reinstall the system first.

| VPS Provider | Lowest Price | Features | Payment Methods |
| :------------------------------------------------------------ | :-------- | :------------------ | :---------------------- |
| [BandwagonHost (BWG)](https://1.jnk.ink/kNQBo) | $49.99/year | **Fastest and most stable** | WeChat, Alipay, PayPal, Credit Card |
| [DMIT](https://1.jnk.ink/yeLEg) | $36.9/year | CN2 GIA routes, Hong Kong CMI routes | **Alipay**, PayPal, Credit Card |
| [hostdare](https://1.jnk.ink/RjBnn) | $25/year | High traffic, fast speed, CMI routes | **Alipay**, PayPal, Credit Card |
| [BuyVM](https://1.jnk.ink/U2Ikm) | ¥2/month | Large storage, unlimited traffic, streaming unlock | **Alipay**, PayPal, Credit Card, Cryptocurrency |
| [RackNerd](https://1.jnk.ink/wdqkS) | $21.99/year | **Cheap**, high traffic, high configuration | **Alipay**, PayPal, Credit Card, Cryptocurrency |
| [CloudCone](https://1.jnk.ink/H4z6h) | $20.25/year | **Cheap**, high traffic, large storage | **Alipay**, PayPal, Credit Card |

### Step 2: SSH into the Server

After the system reinstall is complete, connect using the system’s built-in tools (Terminal on Mac, PowerShell on Windows). Enter the following command and press Enter, then enter the password when prompted (the password will not be visible while typing).  
You can also use a graphical SSH client such as [FinalShell](https://www.hostbuf.com/t/988.html).

```bash
ssh root@YOUR_SERVER_IP
```

![vless-3xui-feng1002.png](https://vless.app/img/vless-3xui-feng1002.png)

### Step 3: Install Firewall and Baota / aaPanel

1. **Install UFW firewall**: Enter `apt install ufw` in the terminal and confirm installation.
2. **Install a management panel**: Baota Panel can be used; if binding a Chinese phone number is inconvenient, alternatives such as aaPanel or 1Panel can be used instead.

```bash
URL=https://www.aapanel.com/script/install_panel_en.sh && if [ -f /usr/bin/curl ];then curl -ksSO $URL ;else wget --no-check-certificate -O install_panel_en.sh $URL;fi;bash install_panel_en.sh dbbd1c69
```

### Step 4: Install 3X-UI and Temporarily Allow the Panel

1. After logging into Baota, open the built-in terminal and run the 3X-UI installation script.
2. Because the firewall was installed earlier, the newly installed 3X-UI panel cannot be accessed by default. Go to Baota’s **Security** page, temporarily disable the firewall (or open the corresponding port), then log in to the 3X-UI panel with the account and password.

```bash
bash <(curl -Ls https://raw.githubusercontent.com/mhsanaei/3x-ui/master/install.sh)
```

### Step 5: Install the Website Environment (Nginx, PHP, MySQL)

Return to Baota’s **App Store** and quickly install **Nginx**. To build a realistic camouflage website, it is also recommended to install **PHP** and **MySQL** (security and complexity increase together).

![vless-3xui-feng1004.png](https://vless.app/img/vless-3xui-feng1004.png)

### Step 6: Domain Resolution and Website Setup (Critical Anti-Pitfall Points)

1. **Configure DNS resolution**: It is recommended to use an independent top-level domain (free second-level domains are not recommended). Add an A record pointing to your server IP; the hostname can be something common like `api`.
2. **Disable proxy (gray cloud)**: If using Cloudflare, **be sure to turn off the proxy status (the cloud icon should be gray)** and use DNS only.
3. **Create the site and apply for a certificate**: In Baota’s “Website” section, add the resolved domain, apply for a free SSL certificate, and enable **Force HTTPS**.
4. **Replace the webpage content**: Replace the default page in the website root directory with real website content or a custom single page.

![vless-3xui-feng1005.png](https://vless.app/img/vless-3xui-feng1005.png)

### Step 7: Modify Nginx Configuration to Free Port 443

This is the core of the “steal yourself” method. Go to Baota “Website” → click the site’s **Settings** → **Configuration File**, make the following two changes, and save:

1. **Change the listening port**: Change the original `443` listening port to `8443` (you can further restrict it to the local loopback address `127.0.0.1:8443`), freeing the standard port 443.
2. **Modify the force-redirect rule**: Find the line that says “redirect if port is not equal to 443” (containing `!= 443`), **remove the exclamation mark `!` and change `443` to `80`** (i.e., only redirect to HTTPS when the port is 80).

> After saving, the website will temporarily be inaccessible. This is normal because port 443 has been freed but has not yet been taken over by 3X-UI.

![vless-3xui-feng1006.png](https://vless.app/img/vless-3xui-feng1006.png)

### Step 8: Create a Reality Inbound Node in 3X-UI

Return to the 3X-UI panel, click **Inbounds** → **Add Inbound**, and configure with the following parameters:

- **Port**: Must be set to `443`
- **Security**: Select `Reality`
- **Dest**: Fill in `127.0.0.1:8443` (must match the port in the Nginx configuration from the previous step)
- **Scan and keys**: Click Scan (a certificate error will appear at this point — this is normal, just confirm), then obtain a new key pair, create it, and add a client

After creation, refresh your camouflage website. The webpage should now be accessible again, and the node should connect normally.

![vless-3xui-feng1007.png](https://vless.app/img/vless-3xui-feng1007.png)

### Step 9: Re-enable the Firewall and Tighten Exposed Ports

Return to Baota’s **Security** page, re-enable the firewall, and batch-delete unnecessary open ports (such as 20, 21, 888, FTP, etc.), keeping only necessary ports (such as 22, 80, 443, and the Baota panel port).

- The 3X-UI panel port should not be exposed externally under normal circumstances. Temporarily add an allow rule only when configuration changes are needed, and remove it immediately afterward.

![vless-3xui-feng1008.png](https://vless.app/img/vless-3xui-feng1008.png)

---

## 2. Advanced Configuration: Residential IP Routing for AI Services

If your node needs to access AI services that are strict about datacenter IPs, you can mount a static residential IP through 3X-UI’s outbound routing:

1. **Purchase a static residential IP**: Besides the United States, Singapore or Japan can also be considered (UTC+8 timezone aligns better with domestic usage patterns; confirm the region is on the target AI service’s supported list before purchasing).
2. **Add a SOCKS5 outbound**: After obtaining the SOCKS5 proxy information for the residential IP, create a new `socks` protocol outbound in 3X-UI’s **Outbounds** (the tag can be customized as `us-home`), fill in the address, port, username, and password, test the real latency, and save.
3. **Set AI-specific routing rules**: Go to **Routing** → **Routing Rules**, create a new rule, browse categories in the domain field and select `AI`, then point the outbound tag to the residential IP outbound you just created and save. This achieves “only AI traffic goes through the residential IP, other traffic connects directly to the server,” balancing speed and traffic cost.

![vless-3xui-feng1009.png](https://vless.app/img/vless-3xui-feng1009.png)

---

## 3. Principle Analysis: Why Go Through All This Trouble?

### 1. Why Was “Stealing Microsoft/Apple” Easily Blocked in the Past?

Reality’s working mechanism embeds a secret in the first packet of the TLS handshake: if the secret matches, proxy traffic is forwarded; if it does not match (e.g., active probing), the server forwards the entire connection unchanged to the target website.

In the past, people filled in large sites such as Microsoft or Apple as the target for convenience, but this had three hidden risks:

- **Identity and address mismatch**: The server has a BandwagonHost Los Angeles IP but claims to be Microsoft. A DNS lookup quickly shows the IP does not belong to Microsoft.
- **Abnormal handshake latency**: Each probe requires the server to connect across the network to the remote Microsoft site and return the result, producing unnatural latency.
- **Becoming a public relay**: If the borrowed target site is behind Cloudflare, the server may become a public jump host.

With the **“steal yourself”** approach, the domain, DNS resolution, SSL certificate, and the real running website are all on the same server. No matter how external parties probe, the information is completely consistent, and the target is on localhost (`127.0.0.1`), so forwarding latency is extremely low.

![vless-3xui-feng10091.png](https://vless.app/img/vless-3xui-feng10091.png)

### 2. Since We Already Have a Real Certificate, Why Not Use Traditional TLS Fallback?

There are two core reasons:

- **Eliminate server-side TLS fingerprint**: In traditional TLS schemes, Xray itself always handles the handshake with the prober and only falls back to Nginx after decryption. Reality does not decrypt unknown connections at all — it hands them over to Nginx as-is, so the prober is always shaking hands with a real Nginx website, completely eliminating the server-side TLS fingerprint.
- **Minimal changes to the website environment**: Traditional TLS fallback passes plaintext to Nginx, requiring an extra plaintext port and easily conflicting with Baota’s force-HTTPS setting. Under the Reality scheme, Nginx continues to run HTTPS normally and only needs to be moved to local port 8443, without affecting certificate renewal or site maintenance.

![vless-3xui-feng10092.png](https://vless.app/img/vless-3xui-feng10092.png)

### 3. Reasons Behind Several “Counter-Intuitive” Operations

- **Why install PHP/MySQL and build a real website?** If a prober opens your domain and only sees a blank or default page, there is almost no camouflage. A website with normal content is the least conspicuous.
- **Why must the Cloudflare cloud be turned off?** Reality itself cannot pass through a CDN. In addition, when the proxy is enabled, domain resolution becomes Cloudflare’s IP, which again fails to match the real server IP that the client connects to directly.
- **Why must Reality occupy 443 and Nginx move to `127.0.0.1:8443`?** Normal HTTPS websites run on port 443; non-443 ports increase the chance of being blocked. Restricting Nginx to the local loopback prevents external scanners from discovering a second identical website on port 8443.
- **Why delete the exclamation mark in the Nginx configuration?** Baota’s default rule is “force redirect to HTTPS if the port is not 443.” After changing Nginx to 8443, leaving this rule unchanged causes an infinite redirect loop. Changing it to “redirect only when the port is 80” solves the problem.
- **Why ignore the certificate error during scanning?** Scanning uses `127.0.0.1` to verify the certificate of your domain, so the hostname naturally does not match. As long as the scan result shows support for TLS 1.3 and ALPN `h2`, it fully meets Reality’s requirements.
- **Why must the firewall be re-enabled and extra ports closed at the end?** The more ports and management panels exposed externally, the more the server looks like a dedicated proxy node machine, and the higher the risk of brute-force attacks on the panel.

![vless-3xui-feng10093.png](https://vless.app/img/vless-3xui-feng10093.png)
