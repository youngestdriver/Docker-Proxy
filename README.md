<p align="right">
   <strong>中文</strong> | <a href="./README.en.md">English</a>
</p>

<div style="text-align: center">
  <p align="center">
  <img src="https://github.com/dqzboy/Docker-Proxy/assets/42825450/c187d66f-152e-4172-8268-e54bd77d48bb" width="230px" height="200px">
      <br>
      <i>自建Docker镜像加速服务，基于官方 registry 一键部署Docker、K8s、Quay、Ghcr、Mcr、elastic、nvcr等镜像加速\管理服务.</i>
  </p>
</div>

---

## 📝 准备工作
选择一台国外服务器，并且未被墙。对于域名，无需进行国内备案。你也可以通过一些平台申请免费域名。在一键部署过程中，如果选择安装Caddy，它将自动配置HTTPS。若选择部署Nginx服务，则需要自行申请一个免费的SSL证书，或者通过其他方式来实现SSL加密。



<details>
<summary><strong>如果你没有上面提到的环境，那么你也可以尝试以下的几种方案</strong></summary>
<div>

**方案一：** 如果你身边没有上面提到的这些东西，那么你也可以试试使用第三方免费容器部署服务 **[ClawCloud](cloud/ClawCloud/README.md)、[Render](cloud/Render/README.md)**

**方案二：** 如果你只有一台服务器，不想搞域名也不想配置TLS，那么你可以修改Docker的配置文件`daemon.json`，指定`insecure-registries` 为你的镜像加速地址

**方案三：** 如果你是在国内的服务器部署，那么你可以在执行一键部署时配置代理，同时会帮你解决国内无法安装Docker的问题

</details>

---

> **部署过程中出现的问题或者疑问，请点击这里 [问题总结](Issue/issue.md)，查看是否有你遇到的情况！尝试先自己解决。**


---

## 🔨 功能
- [x] 一键部署Docker镜像代理服务，支持多个上游镜像仓库代理，如`Docker Hub`、`ghcr`、`quay`、`k8s`、`mcr.microsoft.com`、`docker.elastic.co`等
- [x] 自动检查安装软件依赖，如Docker\Compose、Nginx\Caddy等
- [x] 支持选择自动部署等反代服务，自动渲染对应Nginx或Caddy反代配置
- [x] 支持配置账号密码登入Docker Hub，可下载私有镜像并解决Docker Hub镜像下载频率限制 [配置参考](https://github.com/dqzboy/Docker-Proxy/blob/main/Issue/issue.md#12%E5%85%B3%E4%BA%8Edocker-hub%E5%85%8D%E8%B4%B9%E6%8B%89%E5%8F%96%E6%94%BF%E7%AD%96%E5%86%8D%E6%AC%A1%E5%8F%98%E6%9B%B4%E5%90%8E%E7%9A%84%E8%A7%A3%E5%86%B3%E6%96%B9%E6%A1%88)
- [x] 支持自定义配置代理缓存时间(PROXY_TTL)、支持配置IP黑/白名单，防止恶意攻击行为
- [x] 提供服务管理、配置管理、服务卸载、认证授权等功能，方便后期日常运维管理
- [x] 支持一键配置本机Docker代理和容器服务代理(HTTP_PROXY)，仅支持http
- [x] 支持国内服务器一键部署，解决国内环境无法安装Docker\Compose服务难题
- [x] HubCMD-UI服务，面板展示、镜像搜索、文档教程、容器管理、容器监控告警等功能

## 📦 部署
### Docker Compose 部署
<details>
<summary><strong>点击查看</strong></summary>
<div>

**⚠️ 注意：** 你需要对哪个镜像仓库进行加速，就下载哪个配置。`docker-compose.yaml`文件默认是部署所有的国外镜像仓库的加速服务，同样也是你部署哪个就配置哪个，其余的删除掉即可！

**1.** 下载[config](https://github.com/dqzboy/Docker-Proxy/tree/main/config)目录下对应的`yml`文件到你本地机器上

**2.** 下载[docker-compose.yaml](https://github.com/dqzboy/Docker-Proxy/blob/main/docker-compose.yaml)文件到你本地机器上，并且与配置文件同级目录下

**3.** 执行 `docker compose` 或 `docker-compose` 命令启动容器服务
```shell
# 启动全部容器
docker compose up -d

# 启动指定的容器,例如: Docker Hub Registry Proxy
docker compose up -d dockerhub

# 查看容器日志
docker logs -f [容器ID或名称]
```

</details>

### 使用教程
<details>
<summary><strong>点击查看</strong></summary>
<div>

[使用教程](https://dqzboy.github.io/docs/pages/install.html#%E2%9C%A8-%E4%BD%BF%E7%94%A8)

</details>

---


## 💻 Hubcmd-UI

> HubCMD-UI 手动安装教程：[点击查看教程](hubcmdui/README.md)

> HubCMD-UI 演示环境 [点击查看](https://ufxsgwxleywi.ap-southeast-1.clawcloudrun.com/)

<br/>
<table>
    <tr>
      <td width="50%" align="center"><b>镜像加速</b></td>
      <td width="50%" align="center"><b>镜像搜索</b></td>
    </tr>
    <tr>
        <td width="50%" align="center"><img src="https://cdn.jsdelivr.net/gh/dqzboy/Images/dqzboy-proxy/hubcmd-ui_01.png?raw=true"></td>
        <td width="50%" align="center"><img src="https://cdn.jsdelivr.net/gh/dqzboy/Images/dqzboy-proxy/hubcmd-ui_02.png?raw=true"></td>
    </tr>
    <tr>
      <td width="50%" align="center"><b>文档管理</b></td>
      <td width="50%" align="center"><b>TAG搜索</b></td>
    </tr>
    <tr>
        <td width="50%" align="center"><img src="https://cdn.jsdelivr.net/gh/dqzboy/Images/dqzboy-proxy/hubcmd-ui_03.png?raw=true"></td>
        <td width="50%" align="center"><img src="https://cdn.jsdelivr.net/gh/dqzboy/Images/dqzboy-proxy/hubcmd-ui_11.png?raw=true"></td>
    </tr>
    <tr>
      <td width="50%" align="center"><b>控制面板</b></td>
      <td width="50%" align="center"><b>容器管理</b></td>
    </tr>
    <tr>
        <td width="50%" align="center"><img src="https://cdn.jsdelivr.net/gh/dqzboy/Images/dqzboy-proxy/hubcmd-ui_07.png?raw=true"></td>
        <td width="50%" align="center"><img src="https://cdn.jsdelivr.net/gh/dqzboy/Images/dqzboy-proxy/hubcmd-ui_09.png?raw=true"></td>
    </tr>
</table>

---


## 🤝 参与贡献

感谢所有做过贡献的人!

<a href="https://github.com/dqzboy/Docker-Proxy/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=dqzboy/Docker-Proxy" />
</a>

## ❤ 鸣谢
感谢以下项目的开源的付出：

[CNCF Distribution](https://distribution.github.io/distribution/) 

[docker-registry-browser](https://github.com/klausmeyer/docker-registry-browser)

## License
Docker-Proxy is available under the [Apache 2 license](./LICENSE)

---
