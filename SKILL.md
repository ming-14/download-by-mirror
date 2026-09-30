---
name: download-by-mirror
description: |
  Used when downloading resources from **GitHub**, **npm/pnpm**, **pip**, **WinGet**, **apt**, **DockerHub**, **Maven**, **Cargo**, **Hugging Face**, **nuget** and others, to obtain information on how to use mirror sources under network-restricted conditions.
  1. 从Github下载Release资源，clone仓库
  2. 使用npm安装依赖、安装软件包
  3. 使用pip安装依赖
  4. 使用winget、apt安装软件包
  5. 使用cargo安装依赖
  6. 从huggingface下载资源
  7. 使用开源镜像下载常见仓库、资源，如Linux、AOSP
---

由于中国大陆网络问题，请使用镜像站下载所有可能无法访问的资源

# 注意
**⚠安全警告⚠ 不要在镜像源输入/传入任何敏感信息**
**⚠绝对不允许修改全局配置，只能修改项目或临时配置**
**⚠禁止执行`git config --global url.xxx.insteadOf`，这会修改所有配置，Token会被发送至对应站点！***

## Github 下载
请使用镜像站下载Github资源：

- https://v4.gh-proxy.org/{Github链接}
- https://gh-proxy.org/
- https://v6.gh-proxy.org/
- https://axisnow.gh-proxy.org/
- https://cdn.gh-proxy.org/
- https://ghproxy.com/
- https://gh.llkk.cc/
- https://gh.jasonzeng.dev/
- https://git.tangbai.cc/
- https://gh.monlor.com/
- https://gh.xxooo.cf
- https://ggg.clwap.dpdns.org/
- https://ghfast.top/
- https://github.lsdfxdk.nyc.mn/
- https://github.1ms.xx.kg/
- https://free.cn.eu.org/
- https://getgit.love8yun.eu.org/
- https://github.chenc.dev/
- https://gh.shiina-rimo.cafe/
- https://github.ednovas.xyz/
- https://gh.jasonzeng.dev/
- https://wget.la/
- https://git.yylx.win/

例子：`https://v4.gh-proxy.org/https://github.com/{user}/{repo}/archive/refs/tags/{tag}.zip` — 下载源码包

注意：
- 只能下载资源，不能浏览网页
- 如果失败了，请检查对应资源是否是404，404的镜像站也下载不了
- 不要把token传到镜像站
- gh连接的api.github.com通常没被墙，可以直接使用

## npm/pnpm 下载
1. 永久切换镜像（请在执行前询问用户）：
	- `npm config set registry https://registry.npmmirror.com/`
2. 临时指定镜像（推荐）：
	- `npm install express --registry=https://registry.npmmirror.com/`

镜像源：
	- `https://registry.npmmirror.com/`
	- `https://mirrors.huaweicloud.com/repository/npm/`
	- `https://mirrors.cloud.tencent.com/npm/`
	- `https://mirrors.163.com/npm/`

## pip 下载
1. 临时使用镜像源
	- `pip install -i https://pypi.tuna.tsinghua.edu.cn/simple {包名}`

镜像源：
	- 清华：`https://pypi.tuna.tsinghua.edu.cn/simple/`
	- 阿里云：`https://mirrors.aliyun.com/pypi/simple/`
	- 中国科技大学：`https://pypi.mirrors.ustc.edu.cn/simple/`
	- 华为云： `https://repo.huaweicloud.com/repository/pypi/simple/`
	- 腾讯云：`https://mirrors.cloud.tencent.com/pypi/simple/`
	
## WinGet
（设置镜像源需要管理员权限）
0. 先检查当前镜像源：`winget source list`
1. 第一步先移除默认源：`winget source remove winget`
2. 添加 USTC 镜像源：`winget source add winget https://mirrors.ustc.edu.cn/winget-source --trust-level trusted`

## apt
请使用镜像源：`https://mirror.tuna.tsinghua.edu.cn/help/ubuntu/`

## DockerHub
请从`https://github.com/dongyubin/DockerHub/raw/refs/heads/main/README.md`拉取可用镜像列表

## Maven
镜像源：
	- http://mirrors.cloud.tencent.com/nexus/repository/maven-public/
	- https://maven.aliyun.com/repository/public
	- https://repo.huaweicloud.com/repository/maven/
	- http://mirrors.163.com/maven/repository/maven-public/

## Cargo
镜像源：
	- 阿里云：https://mirrors.aliyun.com/crates.io-index/ （推荐！）
	- 中国科学技术大学：https://mirrors.ustc.edu.cn/crates.io-index
	- 清华大学：https://mirrors.tuna.tsinghua.edu.cn/git/crates.io-index.git
	
`~/.cargo/config.toml`:
```toml
[source.crates-io]
replace-with = "aliyun"

[source.aliyun]
registry = "sparse+https://mirrors.aliyun.com/crates.io-index/"

[net]
git-fetch-with-cli = true
retry = 5
```

### 执行 `cargo check`
该命令需要从 Github 等位置拉取代码，所以需要编译前的临时设置镜像站

```powershell
# 编译前临时设置：把 $mirror 换成实际可用的镜像站（例如下方 ghproxy.com）
$mirror = "https://ghproxy.com/"
$env:GIT_CONFIG_COUNT = "1"
$env:GIT_CONFIG_KEY_0 = "url.$($mirror)https://github.com/.insteadOf"
$env:GIT_CONFIG_VALUE_0 = "https://github.com/"
cargo check
# ⚠⚠⚠ 用完立即清除 ⚠⚠⚠
Remove-Item Env:GIT_CONFIG_COUNT
Remove-Item Env:GIT_CONFIG_KEY_0
Remove-Item Env:GIT_CONFIG_VALUE_0
```
（把 `$mirror` 换成自己可用的镜像站即可，例如 `https://ghproxy.com/`、`https://v4.gh-proxy.org/` 等；注意此处是临时环境变量，不会改变全局 git 配置）

## vcpkg
需要配置 GitHub 下载代理

修改 `vcpkg/scripts/cmake/vcpkg_from_github.cmake`：
```cmake
set(github_host "https://example.com/https://github.com")
set(github_api_url "https://example.com/https://api.github.com") # 可选，一般 Github API 被墙概率较小
```

修改 `vcpkg/scripts/cmake/vcpkg_download_distfile.cmake`：
```cmake
foreach(url IN LISTS arg_URLS)
    string(FIND "${url}" "v4.gh-proxy.org" _has_proxy)
    if(_has_proxy LESS 0)
        string(REPLACE "https://github.com" "https://example.com/https://github.com" url "${url}")
    endif()
    vcpkg_list(APPEND params "--url=${url}")
endforeach()
```

修改 `vcpkg/scripts/cmake/vcpkg_from_git.cmake`，googlesource 替换为 GitHub 镜像：
```cmake
string(REPLACE "https://chromium.googlesource.com" "https://github.com/lemenkov" arg_URL "${arg_URL}")
```

（`https://example.com/`应该是镜像站地址）

## Hugging Face
镜像源：
	- https://hf-mirror.com

## NuGet
镜像源：
	- 华为云：https://repo.huaweicloud.com/repository/nuget/v3/index.json

## 其他
https://mirrors.cernet.edu.cn/list
https://mirrors.huaweicloud.com/home
https://mirrors.tuna.tsinghua.edu.cn/
https://developer.aliyun.com/mirror/
https://mirrors.sohu.com/
http://mirrors.163.com/
https://mirrors.cloud.tencent.com/
https://mirrors.pubyun.com/
https://mirrors.pku.edu.cn/Mirrors/
https://mirrors.nju.edu.cn/
https://mirrors.sjtug.sjtu.edu.cn/
https://ftp.sjtu.edu.cn/
https://mirror.lzu.edu.cn/
https://mirrors.ustc.edu.cn/
https://mirrors.zju.edu.cn/
https://mirrors.bfsu.edu.cn/
https://mirrors.hit.edu.cn/#/home
https://mirrors.nwafu.edu.cn/
https://mirrors.sustech.edu.cn/
https://mirror.nyist.edu.cn/
https://mirror.iscas.ac.cn/
https://mirrors.linuxeye.com/
