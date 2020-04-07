[![Serverless Components](https://img.serverlesscloud.cn/202019/1578569597879-website.png)](http://serverless.com)

<br/>

**腾讯云 Website 静态网站组件** ⎯⎯⎯ 通过使用 [Tencent Serverless Framework](https://github.com/serverless/components/tree/cloud)，基于云上 Serverless 服务（如对象存储等），实现“0”配置，便捷开发，极速部署你的静态网站，Website 静态网站组件支持丰富的配置扩展，如自定义域名和 CDN 加速等。提供了目前最易用、低成本并且弹性伸缩的静态站点开发和托管能力。
<br/>

特性介绍：

- [x] **按需付费** - 按照请求的使用量进行收费，没有请求时无需付费
- [x] **"0"配置** - 只需要关心项目代码，之后部署即可，Serverless Framework 会搞定所有配置。
- [x] **极速部署** - 仅需几秒，部署你的静态网站。
- [x] **实时日志** - 通过实时日志的输出查看业务状态，便于直接在云端开发应用。
- [x] **便捷协作** - 通过云端的状态信息和部署日志，方便的进行多人协作开发。
- [x] **CDN加速，SSL证书配置和自定义域名** - 支持配置CDN加速，支持自定义域名及 HTTPS 访问


<br/>

快速开始：

1. [**安装**](#1-安装)
2. [**创建**](#2-创建)
3. [**部署**](#3-部署)
4. [**配置**](#4-配置)
5. [**开发调试**](#5-开发调试)
6. [**移除**](#6-移除)
7. [**账号配置(可选)**](#账号配置(可选))

&nbsp;

### 1. 安装

通过 npm 安装最新版本的 Serverless Framework 
```
$ npm install -g serverless
```

### 2. 创建

创建并进入一个全新目录：
```
$ mkdir tencent-website && cd tencent-website
```

通过如下命令和模板链接，快速创建一个静态网站托管应用：
```
$ serverless create --template-url https://github.com/serverless-components/tencent-website/tree/v2/example
$ cd example
```

下载完毕后，目录结构如下所示：
```
|- src
|   └── index.html
└──  serverless.yml
```

在 `src` 目录中既可以托管简单的 html 文件，也可以托管完整的 React/Vue 的应用。

### 3. 部署

在 `serverless.yml` 文件下的目录中运行如下命令进行静态网站的部署。部署完毕后，你可以在命令行的输出中查看到你静态网站的 URL 地址，点击地址即可访问网站托管的链接。

```
$ serverless deploy
```

如您的账号未[登陆](https://cloud.tencent.com/login)或[注册](https://cloud.tencent.com/register)腾讯云，您可以直接通过`微信`扫描命令行中的二维码进行授权登陆和注册。

如果希望查看更多部署过程的信息，可以通过`sls deploy --debug` 命令查看部署过程中的实时日志信息，`sls`是 `serverless` 命令的缩写。

<br/>

### 4. 配置

静态网站组件支持 0 配置部署，也就是可以直接通过配置文件中的默认值进行部署。但你依然可以修改更多可选配置来进一步开发该静态网站项目。

以下是静态网站 Website 组件的 `serverless.yml`部分配置说明：

```yml
# serverless.yml

component: tencent-website # (必填) 引用 component 的名称，当前用到的是 tencent-website 组件
name: websitedemo # (必填) 该 website 组件创建的实例名称
org: test # (可选) 用于记录组织信息，默认值为您的腾讯云账户 appid
app: websiteApp # (可选) 该 website 应用名称
stage: dev # (可选) 用于区分环境信息，默认值是 dev

inputs:
  src:
    root: ./
    src: ./src
    hook: npm run build
    index: index.html
    websitePath: ./
  region: ap-guangzhou
  bucketName: my-bucket
  protocol: http
  hosts:
    - host: anycoder.cn
      https:
        certId: 123
```

点此查看[全量配置及配置说明](https://github.com/serverless-components/tencent-website/blob/v2/doc/serverless.yaml)

当你根据该配置文件更新配置字段后，再次运行 `serverless deploy` 或者 `serverless` 就可以更新配置到云端。

### 5. 开发调试

部署了静态网站应用后，可以通过开发调试能力对该项目进行二次开发，从而开发一个生产应用。在本地修改和更新代码后，不需要每次都运行 `serverless deploy` 命令来反复部署。你可以直接通过 `serverless dev` 命令对本地代码的改动进行检测和自动上传。

可以通过在 `serverless.yml`文件所在的目录下运行 `serverless dev` 命令开启开发调试能力。

`serverless dev` 同时支持实时输出云端日志，每次部署完毕后，对项目进行访问，即可在命令行中实时输出调用日志，便于查看业务情况和排障。

### 6. 移除

在`serverless.yml`文件所在的目录下，通过以下命令移除部署的静态网站 Website 服务。移除后该组件会对应删除云上部署时所创建的所有相关资源。

```
$ serverless remove
```

和部署类似，支持通过 `sls remove --debug` 命令查看移除过程中的实时日志信息，`sls`是 `serverless` 命令的缩写。

## 账号配置

当前默认支持 CLI 扫描二维码登录，如您希望配置持久的环境变量/秘钥信息，也可以本地创建 `.env` 文件

```console
$ touch .env # 腾讯云的配置信息
```

在 `.env` 文件中配置腾讯云的 SecretId 和 SecretKey 信息并保存

如果没有腾讯云账号，可以在此[注册新账号](https://cloud.tencent.com/register)。

如果已有腾讯云账号，可以在[API 密钥管理](https://console.cloud.tencent.com/cam/capi)中获取 `SecretId` 和`SecretKey`.

```
# .env
TENCENT_SECRET_ID=123
TENCENT_SECRET_KEY=123
```