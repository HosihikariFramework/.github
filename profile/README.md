# Hosihikari Framework

[English](README.md) | [简体中文](README.zh_hans.md)

A plugin container that brings .NET plugins to Minecraft Bedrock Dedicated Server (BDS). Also known as 星光框架.

A carrier (LeviLamina, Endstone, or the Linux self-hosted carrier) loads the native HostingShim, which hosts the CLR inside the server process. The managed core discovers plugins, resolves dependencies, isolates them, and drives their lifecycle. Providers come in two official classes: first-class providers compile C#/F# source AOT to IL; RpcProvider is the exception first-class provider, a cross-process bridge. The core also loads precompiled assemblies directly.

**Current release**: Abstractions 0.7.1 · Shim v0.5.0 · C#/Rpc Provider v0.2.0 · F# Provider v0.1.1  
**Platforms**: Windows x64 (LeviLamina 26.51, Endstone 0.11) · Linux x64 (Endstone 0.11, self-hosted BDS 1.21.3)  
**Contract**: `api` 2 · manifest `format_version` 1

## Documentation

- [Online documentation](https://hosihikariframework.github.io/) · [简体中文](https://hosihikariframework.github.io/zh/)
- [Quick start](https://hosihikariframework.github.io/quick-start/)
- [Plugin packages](https://hosihikariframework.github.io/plugin-package/)
- [C# plugins](https://hosihikariframework.github.io/authoring-csharp/)
- [Out-of-process bridge (the exception)](https://hosihikariframework.github.io/authoring-rpc/)
- [Examples](https://github.com/HosihikariFramework/hosihikariframework.github.io/tree/main/examples)
- [Troubleshooting](https://hosihikariframework.github.io/troubleshooting/)

## Install

Run in the server root:

```powershell
# self-hosted Linux
lip install github.com/HosihikariFramework/Shim

# LeviLamina
lip install github.com/HosihikariFramework/Shim#levilamina

# Endstone (Windows / Linux)
lip install github.com/HosihikariFramework/Shim#endstone
lip install github.com/HosihikariFramework/Shim#endstone_linux

# First-class providers
lip install github.com/HosihikariFramework/CSharpProvider
lip install github.com/HosihikariFramework/FSharpProvider

# Exception first-class provider
lip install github.com/HosihikariFramework/RpcProvider
```

A plugin package is a directory under `plugins/` whose name matches `name` in its manifest. Start with the [quick start](https://hosihikariframework.github.io/quick-start/).

## Repositories

| Repository | Purpose |
|---|---|
| [Shim](https://github.com/HosihikariFramework/Shim) | Native HostingShim: hosts the CLR in BDS and hands control to the managed core |
| [PluginManagement](https://github.com/HosihikariFramework/PluginManagement) | Managed core: discovery, dependency graph, isolated loading, lifecycle, unload verification |
| [Abstractions](https://github.com/HosihikariFramework/Abstractions) | Plugin contract, published on [NuGet](https://www.nuget.org/packages/Hosihikari.Abstractions) |
| [CSharpProvider](https://github.com/HosihikariFramework/CSharpProvider) | First-class provider: C# source AOT to IL at load with Roslyn |
| [FSharpProvider](https://github.com/HosihikariFramework/FSharpProvider) | First-class provider: F# source AOT to IL at load |
| [RpcProvider](https://github.com/HosihikariFramework/RpcProvider) | Exception first-class provider: a cross-process bridge over line-delimited JSON-RPC 2.0, with Node/QuickJS/Python/Java/Kotlin bindings |
| [CSharpPluginTemplate](https://github.com/HosihikariFramework/CSharpPluginTemplate) | Source C# plugin template |
| [FSharpPluginTemplate](https://github.com/HosihikariFramework/FSharpPluginTemplate) | Source F# plugin template |
| [RpcPluginTemplate](https://github.com/HosihikariFramework/RpcPluginTemplate) | Out-of-process templates: Node.js/TypeScript, Python, Kotlin/JVM |
| [Hosihikari.McMaster.NETCore.Plugins](https://github.com/HosihikariFramework/Hosihikari.McMaster.NETCore.Plugins) | Fork of McMaster.NETCore.Plugins with RID-first native library resolution |
| [HOCON](https://github.com/HosihikariFramework/HOCON) | HOCON implementation used for framework configuration |
| [hosihikariframework.github.io](https://github.com/HosihikariFramework/hosihikariframework.github.io) | Documentation site and example plugins |

## License and trust boundary

LGPL-3.0-or-later for the framework and providers. Abstractions 0.7.1 and later are MIT; the 0.7.0 package remains LGPL-3.0-or-later. Plugin templates and documentation code examples are MIT-0; documentation prose is CC BY-SA 4.0. In-process plugins run in the host process; cross-process plugins run in a child process. Both are fully trusted, and the framework provides no permission boundary; do not load untrusted plugins.
