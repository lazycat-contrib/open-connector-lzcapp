# OpenConnector for LazyCat

这是 [OpenConnector](https://github.com/oomol-lab/open-connector) 的懒猫微服 LPK v2 打包仓库。OpenConnector 是面向 AI Agent 的开源连接器网关，可通过 MCP、HTTP/OpenAPI 和 Web 控制台管理 1,000+ providers 与 10,000+ Actions。

当前打包版本：`v1.3.0`

## 运行配置

- 上游镜像：`ghcr.io/oomol-lab/open-connector:v1.3.0`
- 服务端口：`3000`
- 持久化目录：`/app/data`
- 健康检查：`/health`
- 控制台：通过 LazyCat 请求注入自动完成管理员 Token 鉴权
- Runtime API：在控制台的“访问 / Access”页面创建 Runtime Token 后使用 `/mcp` 或 `/v1`

加密密钥和管理员 Token 均由 LazyCat `stable_secret` 生成，不会以明文写入仓库。请勿修改 `lzc-manifest.yml` 中现有的密钥种子，否则已持久化的凭据可能无法解密。

## 本地构建

```bash
lzc-cli project release -o dist/open-connector.lpk
lzc-cli lpk info dist/open-connector.lpk
```

## 自动发布

`.github/workflows/lazycat.yml` 使用 `ca-x/lazycat-github-action@v1`：

- 每日检查上游稳定 SemVer 镜像；
- 复制 amd64 镜像到 LazyCat Registry；
- 创建版本化 GitHub Release Asset；
- 使用同一份已校验 LPK 和 SHA256 发布到官方商店与私有商店；
- 已存在相同或更高版本时安全跳过，禁止自动降级。

组织级 GitHub Secrets 由 `lazycat-contrib` 统一配置。

## 上游资料

- [Docker 镜像说明（简体中文）](https://github.com/oomol-lab/open-connector/blob/v1.3.0/docs/docker-ghcr.zh-CN.md)
- [配置参考](https://github.com/oomol-lab/open-connector/blob/v1.3.0/docs/configuration.md)
- [Runtime API](https://github.com/oomol-lab/open-connector/blob/v1.3.0/docs/runtime-api.md)
