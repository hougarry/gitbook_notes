---
description: Bypass GFW+ Transform IPV4 to IPV6 + Speed up traffic
---

# V2ray+Warp+BBR

### 1. **Bypass GFW—SSH**

* SSH login to server 45.77.211.156:22&#x20;

```bash
sudo apt update
sudo apt upgrade
```

1.  **Install V2ray/Trojan/Xray on VPS**

    Principle: Install V2ray on your VPS and set up a proxy to bypass the Great Firewall (GFW). At this point, you'll only have an IPv4 address. Cloudflare can detect that you're not in the USA, so you need to use Warp to generate an IPv6 address, known as a native IP. Warp is also developed by Cloudflare, which makes Cloudflare believe you are in the USA. It's a way to use magic to defeat magic.

    [Link to a server setup tutorial](https://github.com/Alvin9999/new-pac/blob/master/%E8%87%AA%E5%BB%BAssr%E6%9C%8D%E5%8A%A1%E5%99%A8%E6%95%99%E7%A8%8B.md)

    SSH login to the VPS, then enter the following:

    ```bash
    source <(curl -sL https://multi.netlify.app/v2ray.sh) --zh

    # Or use another one: Eight-in-one script
    wget -P /root -N --no-check-certificate "https://raw.githubusercontent.com/mack-a/v2ray-agent/master/install.sh" && chmod 700 /root/install.sh && /root/install.sh
    ```

    Successfully installed V2ray!

Choose transmission method 5: WebSocket.

Enter the pre-resolved domain name: vv02.garyhou.top.

Then, enable TLS by entering v2ray, and choose 6 for enable.

{% hint style="info" %}
I strongly recommend the use of Websocket+TLS
{% endhint %}

Import vmess address into the proxy client. /v2rayNG/&#x20;

Or use Manual configuration for Shadowsocks

Enter the ShadowsocksR account password (default: root):

Password: root

Configuration information for ShadowsocksR account:

IP: 45.77.211.156&#x20;

* Port: 2333 Password: root Encryption: aes-256-cfb Protocol: auth\_sha1\_v4\_compatible Obfuscation: plain Device limit: 0 (unlimited) Single-threaded speed limit: 0 KB/S Port total speed limit: 0 KB/S&#x20;
*   SS Link: ss://YWVzLTI1Ni1jZmI6cm9vdEA0NS43Ny4yMTEuMTU2OjIzMzM SS QR Code: [Link](http://doub.pw/qr/qr.php?text=ss://YWVzLTI1Ni1jZmI6cm9vdEA0NS43Ny4yMTEuMTU2OjIzMzM) SSR Link: ssr://NDUuNzcuMjExLjE1NjoyMzMzOmF1dGhfc2hhMV92NDphZXMtMjU2LWNmYjpwbGFpbjpjbTl2ZEE SSR QR Code: [Link](http://doub.pw/qr/qr.php?text=ssr://NDUuNzcuMjExLjE1NjoyMzMzOmF1dGhfc2hhMV92NDphZXMtMjU2LWNmYjpwbGFpbjpjbTl2ZEE)

    Note: In the browser, open the QR code link to view the QR code image. The "\_compatible" in the protocol and obfuscation means compatible with the original version.

Remember to open the port in the firewall.

For CentOS:

```bash
sudo firewall-cmd --zone=public --add-port=27302/tcp --permanent
sudo firewall-cmd --zone=public --add-port=22/tcp --add-port=443/tcp --permanent
sudo firewall-cmd --zone=public --add-port=3000/tcp --add-port=8000/tcp --permanent --ipv6
sudo firewall-cmd --reload
```



## **2. Install Warp to Unlock IPv6**

Click here for detailed info.

[WARP one-click script](https://github.com/fscarmen/warp)

After V2ray, then start to install warp , enter:

```bash
wget -N https://gitlab.com/fscarmen/warp/-/raw/main/menu.sh && bash menu.sh d

#choose ipv6 /  choose 11 onclick unlock + telegram bot reminder! 

# after first install,  you can use warp o to turn on or turn off
# Check
systemctl status warp_unlock

# Disable
systemctl disable --now warp_unlock

# Check [pgrep -laf warp_unlock], and close [kill -9 $(pgrep -f warp_unlock)]

```





## **3. Install BBR Traffic Acceleration**

```bash
wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh"
chmod +x tcp.sh
./tcp.sh
```

As an example, let's install the enhanced BBR modification for acceleration. First, install the corresponding kernel by entering 1.

After the kernel installation is complete, enter 'y' to restart. The kernel needs to be restarted to take effect.

After the restart, enter 6 to enable the enhanced BBR modification for acceleration.

\[I have used BBR Plus]

Please note that these instructions involve setting up and configuring various components on a server and should be performed with caution and in compliance with applicable laws and policies.
