# MeowFilm

<p align="center">
  <img src="https://raw.githubusercontent.com/ilimidusesa/MeowFilm/refs/heads/main/favicon.svg" alt="MeowFilm" width="120" />
</p>

> MeowFilm 是一个基于 Go + Vue 的影视聚合 Web 应用，提供 UI、账号与配置管理、聚合与播放等核心能力；解析能力由自定义脚本通过 catpawrunner 提供。

---

## 功能特性

- 🔌 插件化站点解析：通过 catpawrunner `/spider/*` 对接自定义脚本/规则，支持多站点聚合与站点开关/排序
- 🔍 搜索与聚合播放：覆盖搜索、详情、选集、播放，支持站点结果聚合与多来源回退
- 🧠 智能匹配引擎：内置剧集提取规则、片名清洗规则、聚合归一规则、来源优先级与网盘优先级策略
- 🚫 匹配屏蔽机制：支持维护 Smart Match Block 关键词/条目，过滤不希望命中的结果
- ❤️ 用户侧数据：支持收藏、搜索历史、播放历史与继续观看，含按 TMDB/关键词去重与续播同步
- ☁️ 多网盘适配：支持夸克、UC、百度、天翼(189)、移动云盘(139)等网盘的列表与播放解析能力
- 🔐 网盘登录管理：后台支持百度/夸克/UC/115/B站网盘登录态维护（含二维码流程）
- 🎬 Emby 兼容 API：提供 Emby 子集接口（搜索、媒体项、继续观看、会话上报、播放链路）便于客户端接入
- 🖼 元数据增强：支持 TMDB 搜索/详情与豆瓣接口代理能力，用于补充封面与结构化信息
- 🚀 GoProxy（可选）：可按网盘类型透传播放并自动选路，优化需要 headers 的直链播放场景

## 目录

- [部署](#部署)
- [默认账号](#默认账号)
- [快速配置](#快速配置)
- [可选配置](#可选配置)
- [相关项目](#相关项目)

## 部署

下载对应的系统/架构包后执行：

```bash
chmod +x ./meowfilm
./meowfilm
```

可选环境变量：

| 变量 | 说明 | 默认值 |
| --- | --- | --- |
| `MEOWFILM_ADDR` | 服务监听地址 | `:8080` |
| `MEOWFILM_DB_FILE` | 指定数据库文件路径 | 空 |
| `MEOWFILM_DATA_DIR` | 指定数据目录（默认会在该目录写入 `data.db`） | 空 |
| `MEOWFILM_DEBUG` | 启用调试接口（如 `/listdebug`、`/searchdebug`） | `0` |

示例：

```bash
MEOWFILM_ADDR=":8080" \
MEOWFILM_DATA_DIR="./data" \
MEOWFILM_COOKIE_SECURE="1" \
./meowfilm
```

## 默认账号

首次启动会初始化数据库并创建默认管理员账号与密码,均为：`admin`。


## 快速配置

1. 接口配置:

- 配置 CatPawRunner 服务,并添加对应的配置地址。例如：`http://127.0.0.1:9988/`

 - 该地址需要确保客户端能正确访问,如果要使用emby客户端,则需要服务器也能访问

2. 视频源配置:

- 配置好 CatPawRunner 服务后进行导入即可

3. 网盘配置:

- 后台设置中设定好对应的网盘信息后,给 CatPawRunner 服务同步网盘信息,(接口设置中的`同步网盘账号至CatPawRunner`)


## 可选配置

### 智能播放

在媒体数据设置中填入TMDB的token,并确保服务器能获取数据，会自动触发。

### GoProxy

主要用于减轻 CatPawRunner 的性能消耗,用于需要header的地址。


## 相关项目

- CatPawRunner：https://github.com/ilimidusesa/CatPawRunner
- GoProxy（可选）：https://github.com/ilimidusesa/GoProxy
