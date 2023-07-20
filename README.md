# V2ray Edge (Beta)

> Due to limitations of deno deploy, free users cannot currently deploy.
> Looks like the title of Render.

> Due to restrictions of deno deploy, free users can't deploy currently. Please check the Telegram group for more information.
> https://deno.com/deploy/docs/pricing-and-limits#tls-proxying

> Seems Render also banned this project..

As we all know, V2ray is based on `go`, which makes the original version of V2ray unable to be deployed on platforms based on `javaScript (V8)`.

This project is passed, using `js` to implement the `VLESS` protocol, so that **V2ray** can be deployed on some Edge or Serverless platforms.

> For international user, I write this readme in Chinese. But I understand English pretty well, if you have any issue, please open it in Github.

> This project is purely technical verification, exploring the latest web standard. Do not misuse, no guarantees are given.

## ~~V2ray Edge server --- Deno deploy~~

> Due to limitations of deno deploy, free users cannot currently deploy.
> https://deno.com/deploy/docs/pricing-and-limits#tls-proxying

Edge tunnel service uses [Deno deploy](https://deno.com/deploy).

### risk warning

`Deno deploy` adopts [fair use policy](https://deno.com/deploy/docs/fair-use-policy), translated into Chinese is `see conscience use`. Violations may result in banning.
According to my understanding, this project should violate the fair use policy. Please **use as appropriate**.

### How to deploy the service

~~Please check the tutorial below. ~~

~~[Deno deploy Install](./doc/edge-tunnel-deno.md)~~

## V2ray Edge server --- Cloudflare Worker (stay tuned)

This needs to wait for Cloudflare to release the following technology.
https://blog.cloudflare.com/introducing-socket-workers/

> Cloudflare's generous free policy, plus preferred IPs. It makes deploying V2ray extremely simple.

> This is not to use Worker for reverse generation, but to directly deploy V2ray (js version) to Worker.

## V2ray Edge server --- Node.js

Many Node.js platforms support docker, so the original version can be deployed directly. But since many people want it, I will write one. I currently only maintain documentation for the render platform. In theory, other platforms are the same.

### ~~render.com~~

> Looks like the title of Render.
> Seems Render also banned this project..

~~[render](./doc/render.md)~~

###Docker

```bash
docker run -d -p 4600:4100 -e UUID=ce6d9073-7085-4cb1-a64d-382489a2af94 zizifn/node-vless:latest
```

> If you want DNS IPV4 first, please set the environment variable DNSORDER=ipv4first

###Command

```bash
export UUID=ce6d9073-7085-4cb1-a64d-382489a2af94 PORT=4100 node ./dist/apps/node-vless/main.js
```

Small memory:

```bash
export UUID=ce6d9073-7085-4cb1-a64d-382489a2af94 PORT=4100 SMALLRAM=true node ./dist/apps/node-vless/main.js
```

> If you want DNS IPV4 first, please set the environment variable DNSORDER=ipv4first

## Client v2rayN configuration

> ⚠️ Due to edge platform limitations, UDP packets cannot be forwarded. Please change the DNS policy to "Asis" when configuring, otherwise the speed will be affected.
> Please do not enable ipv6 priority.

> [DNS popular science article](https://tachyondevel.medium.com/%E6%BC%AB%E8%B0%88%E5%90%84%E7%A7%8D%E9%BB%91%E7% A7%91%E6%8A%80%E5%BC%8F-dns-%E6%8A%80%E6%9C%AF%E5%9C%A8%E4%BB%A3%E7%90%86%E7 %8E%AF%E5%A2%83%E4%B8%AD%E7%9A%84%E5%BA%94%E7%94%A8-62c50e58cbd0)

### Windows version

https://github.com/2dust/v2rayN
Others' configuration tutorial reference, https://v2raytech.com/v2rayn-config-tutorial/.

For specific configuration, please refer to the home page of the deployment service.

### android

[v2rayNG](https://github.com/2dust/v2rayNG)

[SagerNet](https://github.com/SagerNet/SagerNet)

If Android cannot be used, please refer to the following configuration and try more DNS settings.

v2rayNG settings.
![andriod-v2ray](./doc/andriod_v2rayn.jpg)

### IOS

> US account required

[shadowrocket](https://apps.apple.com/us/app/shadowrocket/id932747118)

## Create cloudflare worker counter generation (optional)

```js
const targetHost = 'xxx.xxxx.dev'; //hostname of your edge function
addEventListener('fetch', (event) => {
   let url = new URL(event.request.url);
   url.hostname = targetHost;
   // url.protocol = 'http';
   // url.pathname = '/index';
   // url.port = '443';
   let request = new Request(url, event.request);
   event.respondWith(fetch(request));
});
```

Preferred IP https://github.com/XIU2/CloudflareSpeedTest

# FAQ

## Which platforms can be used?

To judge whether a platform can support, there are two necessary conditions,

1. Is websocket supported?
    - Or support, HTTP request stream is also possible. https://developer.chrome.com/articles/fetch-streaming-requests/
2. Can create raw tcp socket?

> Although Cloudflare Worker supports websocket, the runtime of Worker does not support API for creating raw tcp socket.

## does not support UDP

UDP packets cannot be forwarded due to edge platform limitations. So please set the DNS policy to `Asis`.

## VMESS is not supported

The VMESS protocol is too complicated, and all edge platforms support HTTPS, so there is no need for VMESS.

# Feedback and communication

If you have questions, use https://t.me/edgetunnel to communicate.

triiger build
