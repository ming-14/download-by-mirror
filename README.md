# download-by-mirror

让 AI 学会从镜像下载资源 —— 一份面向 AI 编码助手的镜像源速查与使用规范。

## 这是什么

这是一个 **Agent Skill**：当 AI Agent 需要下载 GitHub Release、安装 npm/pip/cargo 依赖、拉取 Docker 镜像或下载 Hugging Face 模型时，如果处于网络受限环境（如中国大陆）

## 解决什么问题

- 直连 `github.com`、`registry.npmjs.org`、`pypi.org` 等源经常超时或被墙；
- 网上零散的镜像地址大多已失效，AI 需要一份可直接执行的清单；

本 Skill 同时给出了「**用什么镜像**」和「**怎么安全地用**」。

## 覆盖范围

| 分类 | 说明 |
| --- | --- |
| GitHub | Release 资源下载、仓库 clone / 源码包（20+ 个 gh-proxy 镜像站） |
| npm / pnpm | 依赖安装的临时与永久镜像切换 |
| pip | PyPI 国内镜像（清华、阿里、USTC、华为云、腾讯云） |
| WinGet | USTC 镜像源的添加步骤（需管理员权限） |
| apt | Ubuntu 清华源 |
| DockerHub | 可用镜像列表的获取方式 |
| Maven | 阿里云 / 腾讯云 / 华为云 / 163 |
| Cargo | crates.io 稀疏索引镜像 + `cargo check` 拉取 GitHub 的临时方案 |
| vcpkg | `vcpkg_from_github.cmake` 等三个脚本的改写方式 |
| Hugging Face | `hf-mirror.com` |
| NuGet | 华为云 NuGet v3 源 |
| 其他 | 20+ 个综合镜像站导航 |

完整内容见 **[SKILL.md](./SKILL.md)**。

## 安装

```bash
npx skills add https://github.com/ming-14/download-by-mirror-skill -y
```