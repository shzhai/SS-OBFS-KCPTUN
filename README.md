## shadowsocks-libev-v2ray-kcptun

Build integrated shadowsocks-libev-v2ray-plugin-with-kcptun on ubuntu 18.04 based on https://github.com/shadowsocks/shadowsocks-libev/releases/ and https://github.com/xtaci/kcptun/releases

[![](https://images.microbadger.com/badges/image/shzhai/shadowsocks-libev-v2ray-kcptun.svg)](https://microbadger.com/images/shzhai/shadowsocks-libev-v2ray-kcptun "Get your own image badge on microbadger.com") [![](https://images.microbadger.com/badges/version/shzhai/shadowsocks-libev-v2ray-kcptun.svg)](https://microbadger.com/images/shzhai/shadowsocks-libev-v2ray-kcptun "Get your own version badge on microbadger.com")

### support version

- Ubuntu 18.04
- Shadowsocks-libev version 3.3.1
- Kcptun version 20180905

### How to use this repo

```sh
docker run -d -p 2222:2222 -p 2222:2222/udp -p 3333:3333/udp --restart always --env-file ss-kcp.config shzhai/shadowsocks-libev-v2ray-kcptun
```

> The first and second -p parameter will use to map shadowsockcs tcp/udp port
> 2222 to external, and the third -p parameter will use to map kcptun udp port
> 3333 to external, we will use an environment file ss-kcp.config to config
> shadowsocks and kcptun parameters include the ports above.
> For detail of the configurable parameters will list down below.
> You can also use -e to override the settings but that won't be necessary.

*Download this environment config file from https://raw.githubusercontent.com/shzhai/shadowsocks-libev-v2ray-kcptun/master/ss-kcp.config and change the settings according to your need.*

### Configurable Parameters for ss-kcp.config

#### Shadowsocks

| Parameter | Default value | Common setting | May Modify |
| ------ | ------ |------ |------ |
| SHADOWSOCKS | | | |
| SERVER_ADDR | 0.0.0.0 | | |
| SERVER_PORT | 2222 | | ✅ |
| LOCAL_PORT | 1080 | | |
| PASSWORD | examplepwd | | ✅ |
| METHOD | chacha20-ietf-poly1305 |rc4-md5,aes-256-cfb,chacha20-ietf,chacha20-ietf-poly1305 | ✅ |
| TIMEOUT | 60 | | ✅ |
| FASTOPEN | --fast-open | | |
| UDP_RELAY | -u | | ✅ |

#### V2Ray

| Parameter | Default value | Common setting | May modify  |
| ------ | ------ |------ |------ |
| PLUGIN | v2ray-plugin | PLUGIN_OPTS=server, server;tls;host=yourdomain.com;path=/v2ray;cert=/root/.acme.sh/yourdomain.com/yourdomain.com.cer;key=/root/.acme.sh/yourdomain.com/yourdomain.com.key -u restart: always  | ✅ |

#### KCPTUN

| Parameter | Default value | Common setting | May modify  |
| ------ | ------ |------ |------ |
| KCP_LISTEN | 3333 | | ✅ |
| KCP_PASS | examplepwd | | ✅ |
| KCP_ENCRYPT | salsa20 | aes, aes-128, aes-192, salsa20 | ✅ |
| KCP_MODE | fast2 | fast,fast2 | |
| KCP_MTU | 1350 | | ✅ |
| KCP_SNDWND | 2048 | tune from 1024 (Bandwidth > 100M)| ✅ |
| KCP_RCVWND | 2048 | tune from 1024 (Bandwidth > 100M)| ✅ |
| KCP_DSCP | 46 | | ✅ |
| KCP_NOCOMP | false | | ✅ |

### KCPTun tunning Reference Blog

- https://blog.kuoruan.com/102.html

### Change log

- 2018-4-14 Initialize this repository from github automation build.
- 2018-4-16 Correct ss-kcp.config and update ReadMe.
- 2018-4-17 Enable Simple-OBFS configuration.
- 2018-9-6 Reduce layers to shrink size of this image and update to ss-server 3.2.0 and kcptun 20180810.
- 2019-9-6 Update to ss-server 3.3.1 and kcptun 20190906.
- 2019-9-19 Replace simple-obfs to v2ray plugin as simple-obfs project is obsoleted.

### Feedback & Thanks :)

- <Shawn.zhai@gmail.com>
