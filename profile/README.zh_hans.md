# 星光 · 星光框架

[English](README.md) | [简体中文](README.zh_hans.md)

把 .NET 插件带进 Minecraft 基岩版专用服务器（BDS）的插件容器。

载体（LeviLamina 或 Endstone）加载原生 HostingShim，Shim 把 CLR 托管进服务器进程；托管核心负责插件发现、依赖排序、隔离装载与生命周期。官方 Provider 分两类：一等 Provider 把 C#/F# 源码 AOT 为 IL；RpcProvider 是例外一等 Provider，跨进程桥。预编译程序集由核心内置入口装载。

**当前版本**：Abstractions 0.7.0 · Shim v0.2.1 · Provider v0.1.0  
**平台**：Windows x64；LeviLamina 26.51、Endstone 0.11  
**契约**：`api` 2 · 清单 `format_version` 1

## 文档

- [在线文档](https://hosihikariframework.github.io/zh/) · [English](https://hosihikariframework.github.io/)
- [快速开始](https://hosihikariframework.github.io/zh/quick-start/)
- [插件包与清单](https://hosihikariframework.github.io/zh/plugin-package/)
- [C# 插件](https://hosihikariframework.github.io/zh/authoring-csharp/)
- [进程外桥（例外）](https://hosihikariframework.github.io/zh/authoring-rpc/)
- [示例插件](https://github.com/HosihikariFramework/hosihikariframework.github.io/tree/main/examples)
- [常见问题](https://hosihikariframework.github.io/zh/troubleshooting/)

## 安装

在服务端根目录执行：

```powershell
# LeviLamina
lip install github.com/HosihikariFramework/Shim

# Endstone
lip install github.com/HosihikariFramework/Shim#endstone

# 一等 Provider
lip install github.com/HosihikariFramework/CSharpProvider
lip install github.com/HosihikariFramework/FSharpProvider

# 例外一等 Provider
lip install github.com/HosihikariFramework/RpcProvider
```

插件包是 `plugins/` 下的一个目录，目录名与清单里的 `name` 一致。第一次使用见[快速开始](https://hosihikariframework.github.io/zh/quick-start/)。

## 仓

| 仓 | 作用 |
|---|---|
| [Shim](https://github.com/HosihikariFramework/Shim) | 原生 HostingShim：把 CLR 托管进 BDS，交给托管核心 |
| [PluginManagement](https://github.com/HosihikariFramework/PluginManagement) | 托管核心：发现、依赖图、隔离装载、生命周期与卸载验证 |
| [Abstractions](https://github.com/HosihikariFramework/Abstractions) | 插件契约，发布在 [NuGet](https://www.nuget.org/packages/Hosihikari.Abstractions) |
| [CSharpProvider](https://github.com/HosihikariFramework/CSharpProvider) | 一等 Provider：C# 源码 Roslyn 装载时 AOT 为 IL |
| [FSharpProvider](https://github.com/HosihikariFramework/FSharpProvider) | 一等 Provider：F# 源码装载时 AOT 为 IL |
| [RpcProvider](https://github.com/HosihikariFramework/RpcProvider) | 例外一等 Provider：跨进程桥，行分隔 JSON-RPC 2.0 over stdio，带 Node/QuickJS/Python/Java/Kotlin 绑定 |
| [Hosihikari.McMaster.NETCore.Plugins](https://github.com/HosihikariFramework/Hosihikari.McMaster.NETCore.Plugins) | McMaster.NETCore.Plugins 的 fork：本机库按当前 RID 优先解析 |
| [HOCON](https://github.com/HosihikariFramework/HOCON) | 框架配置使用的 HOCON 实现 |
| [hosihikariframework.github.io](https://github.com/HosihikariFramework/hosihikariframework.github.io) | 文档站点与示例插件 |

## 许可与信任边界

LGPL-3.0-or-later。插件与宿主同进程运行，框架按完全受信设计；不要加载不受信的插件。
