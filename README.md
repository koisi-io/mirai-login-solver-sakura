# mirai-login-solver-sakura

--------------------------

这是另外的一整套验证处理工具，主要是为了优化和方便处理各种验证码

>
本项目前身: [TxCaptchaHelper](https://github.com/mzdluo123/TxCaptchaHelper)

### 预览

<details>
<summary>点击展开</summary>

![](.images/main-snapshot/img.webp)

![](.images/main-snapshot/img_1.webp)

![](.images/main-snapshot/img_2.webp)

![](.images/main-snapshot/img_3.webp)

</details>

### 下载

Way 1:
从 [Releases](https://github.com/KasukuSakura/mirai-login-solver-sakura/releases)
下载

- `mirai-login-solver-sakura-XXX.mirai2.jar` -> mirai-console 插件
- `apk-release.apk` 安卓应用程序

Way 2: 从最新构建下载

<details>
<summary>点击展开</summary>

![](.images/download-from-ci/img.webp)

![](.images/download-from-ci/img_1.webp)

![](.images/download-from-ci/img_2.webp)

下载的压缩包里有全部的最新构建成果

</details>

---------

> 以下内容只适合需要对接 mirai-login-solver-sakura 的开发者参考

## 数据交换

### `<QR CODE>`

显示给 APP 扫描的二维码内容是一个 json, 格式如下

```json5
{
    "port": 8080, // 数据交换的 http 服务器的端口
    "server": [   // 全部可能的 ip 地址 (内网)
        "192.168.2.123",
        "192.168.5.148",
    ],
    "id": "AAAAAAAAAAAAAAA", // 本次请求的 id
}
```

### `/request/request/$id`

```json5
{
    "reqid": "AAAAAAAAAAAAAA", // 请求的 id  (not in use)
    "rspuri": "/request/complete/AAAAAAAAAAAAAA", // 回调, 只有 path, POST 请求, 无编码
    "create-time": 10086, // 时间戳, ms      (not in use)
    "data": { // 请求的数据体
        "type": "slider", // 这次请求的类型
        //..... 请求的其他数据
    },
}
```

#### `slider`

REQ

```json5
{
    "data": {
        "type": "slider",
        "url": "https://ssl.captcha.qq.com/template/wireless_mqq_captcha.html?style=simple&aid=16&uin=.....",
    }
}
```

RSP:

```text
t105.............
```
