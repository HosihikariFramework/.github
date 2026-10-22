# 星光 · 星光框架

<table align="right">
  <tr>
    <td align="right">
      <img src="assets/mascot.png" width="240" alt="星光（Hosi Hikari），星光框架吉祥物"><br>
      <sub>立绘：墨鱼纸鸢</sub>
    </td>
  </tr>
</table>

[English](README.md) | [简体中文](README.zh_hans.md)

把 .NET 插件带进 Minecraft 基岩版专用服务器（BDS）的插件容器。

载体（LeviLamina、Endstone 或 Linux 自持态）加载原生 HostingShim，Shim 把 CLR 托管进服务器进程；托管核心 PluginManager 负责插件发现、依赖排序、隔离装载与生命周期。C# 与 F# 加载器在装载时编译源码；RpcLoader 在子进程中运行插件；核心内置加载器处理预编译程序集。

**当前版本**：Hosihikari.Plugin.Abstractions 1.1.0 · PluginManager v1.1.0 · HostingShim v1.1.0 · C#/F#/RPC 加载器 v1.0.0 · 构建与测试包 1.0.0 · 插件模板 1.0.1  
**平台**：Windows x64（LeviLamina 26.51、Endstone 0.11）· Linux x64（Endstone 0.11、自持态 BDS 1.21.3）  
**契约**：`api_version` 2 · 清单 `manifest_version` 1

## 文档

- [在线文档](https://hosihikariframework.github.io/zh/) · [English](https://hosihikariframework.github.io/)
- [快速开始](https://hosihikariframework.github.io/zh/quick-start/)
- [插件包与清单](https://hosihikariframework.github.io/zh/plugin-package/)
- [C# 插件](https://hosihikariframework.github.io/zh/authoring-csharp/)
- [进程外插件](https://hosihikariframework.github.io/zh/authoring-rpc/)
- [示例插件](https://github.com/HosihikariFramework/hosihikariframework.github.io/tree/main/examples)
- [常见问题](https://hosihikariframework.github.io/zh/troubleshooting/)

## 安装

在服务端根目录执行：

```powershell
# 自持态 Linux
lip install github.com/HosihikariFramework/HostingShim

# LeviLamina
lip install github.com/HosihikariFramework/HostingShim#levilamina

# Endstone（Windows / Linux）
lip install github.com/HosihikariFramework/HostingShim#endstone

# 进程内源码加载器
lip install github.com/HosihikariFramework/CSharpLoader
lip install github.com/HosihikariFramework/FSharpLoader

# 进程外加载器
lip install github.com/HosihikariFramework/RpcLoader

# 预编译插件模板
dotnet new install Hosihikari.Plugin.Templates::1.0.1

# 插件工程构建与测试包
dotnet add package Hosihikari.Plugin.Build --version 1.0.0
dotnet add package Hosihikari.Testing --version 1.0.0
```

插件包是 `plugins/` 下的一个目录，目录名与清单里的 `name` 一致。第一次使用见[快速开始](https://hosihikariframework.github.io/zh/quick-start/)。

## 仓

| 仓 | 作用 |
|---|---|
| [HostingShim](https://github.com/HosihikariFramework/HostingShim) | 原生 HostingShim：把 CLR 托管进 BDS，交给托管核心 |
| [PluginManager](https://github.com/HosihikariFramework/PluginManager) | 托管核心：发现、依赖图、隔离装载、生命周期与卸载验证 |
| [PluginAbstractions](https://github.com/HosihikariFramework/PluginAbstractions) | 插件契约，发布在 [NuGet](https://www.nuget.org/packages/Hosihikari.Plugin.Abstractions) |
| [CSharpLoader](https://github.com/HosihikariFramework/CSharpLoader) | C# 源码加载器：Roslyn 在装载时编译，产物进入 collectible ALC |
| [FSharpLoader](https://github.com/HosihikariFramework/FSharpLoader) | F# 源码加载器：装载时编译，产物进入 collectible ALC |
| [RpcLoader](https://github.com/HosihikariFramework/RpcLoader) | 进程外加载器：行分隔 JSON-RPC 2.0 over stdio，带 Node/QuickJS/Python/Java/Kotlin 绑定 |
| [CSharpPluginTemplate](https://github.com/HosihikariFramework/CSharpPluginTemplate) | 源码 C# 插件模板 |
| [FSharpPluginTemplate](https://github.com/HosihikariFramework/FSharpPluginTemplate) | 源码 F# 插件模板 |
| [RpcPluginTemplate](https://github.com/HosihikariFramework/RpcPluginTemplate) | 进程外模板：Node.js/TypeScript、Python、Kotlin/JVM |
| [Hosihikari.McMaster.NETCore.Plugins](https://github.com/HosihikariFramework/Hosihikari.McMaster.NETCore.Plugins) | McMaster.NETCore.Plugins 的 fork：本机库按当前 RID 优先解析 |
| [HOCON](https://github.com/HosihikariFramework/HOCON) | 框架配置使用的 HOCON 实现 |
| [hosihikariframework.github.io](https://github.com/HosihikariFramework/hosihikariframework.github.io) | 文档站点与示例插件 |

## 许可与信任边界

框架与加载器使用 LGPL-3.0-or-later；Hosihikari.Plugin.Abstractions 0.7.1 及之后为 MIT，0.7.0 包仍为 LGPL-3.0-or-later。插件模板与文档代码示例为 MIT-0；文档正文为 CC BY-SA 4.0。进程内插件与宿主同进程运行，进程外插件在子进程中运行；两类都完全受信，框架不提供权限边界；不要加载不受信的插件。
