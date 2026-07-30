# ChapterApi

Emby Server 插件：章节查看与编辑（Chapter Editor）。

支持查看、新增、删除各类章节标记；提供季级片头摘要页；可通过 Chromaprint 主题音频指纹进行片头检测。

论坛帖：https://emby.media/community/topic/110525-plugin-chapter-editor-chapterapi  
源码：https://github.com/faush01/ChapterApi

## 功能

- 查看媒体项（电影 / 季 / 集）的章节列表
- 添加、删除章节，支持多种章节标记类型
- 按固定时间间隔自动生成章节
- 季级 Intro 摘要，便于检查各集片头/片尾标记
- 基于 Chromaprint 的片头检测（需 Intro CP 数据）
- 可从共享仓库加载 Intro 主题指纹数据：https://github.com/faush01/ThemeCpData

## 环境要求

- .NET SDK（支持 `netstandard2.0` 即可，例如 .NET 6/8/9）
- Emby Server（插件依赖 `mediabrowser.server.core` 4.7.3）

## 编译

在仓库根目录执行：

```powershell
dotnet build ChapterApi.sln -c Release
```

编译产物：

```
ChapterApi\bin\Release\netstandard2.0\ChapterApi.dll
```

项目内置 PostBuild：编译成功后会将 DLL 复制到本机：

```
%AppData%\Emby-Server\programdata\plugins\
```

若该目录不存在或 Emby 安装路径不同，请手动复制 DLL。

## 安装到 Emby

1. 将 `ChapterApi.dll` 复制到 Emby 的 `plugins` 目录  
   - Windows 桌面版：`%AppData%\Emby-Server\programdata\plugins\`  
   - 其他安装方式：使用 Emby 数据目录下的 `plugins` 文件夹
2. 重启 Emby Server
3. 在管理后台确认：服务器 → 插件 → 可见 **Chapter API**

也可直接在 Emby 插件目录中搜索安装（若已上架目录）。

## 注意事项

- 对媒体项执行元数据刷新时，章节会被清空并重建；手动编辑过的章节也会丢失，目前无法锁定章节。
- 片头检测需要对应系列的 Chromaprint Intro 数据；可在插件选项中配置外部数据 URL 并下载，例如：

```
https://github.com/faush01/ThemeCpData/archive/refs/heads/main.zip
```

## 许可

GNU General Public License v3
