# Hosihikari Framework

[English](README.md) | [简体中文](README.zh_hans.md)

A plugin container that brings .NET plugins to Minecraft Bedrock Dedicated Server (BDS). Also known as 星光框架.

A carrier (LeviLamina or Endstone) loads the native HostingShim, which hosts the CLR inside the server process. The managed core discovers plugins, resolves dependencies, isolates them, and drives their lifecycle. Providers extend the plugin types: assemblies, C#, and F# run in-process; other languages connect out-of-process over JSON-RPC.

**Current release**: Abstractions 0.7.0 · Shim v0.2.1 · Provider v0.1.0  
**Platforms**: Windows x64; LeviLamina 26.51 and Endstone 0.11  
**Contract**: `api` 2 · manifest `format_version` 1

## Documentation

- [Online documentation](https://hosihikariframework.github.io/) · [简体中文](https://hosihikariframework.github.io/zh/)
- [Quick start](https://hosihikariframework.github.io/quick-start/)
- [Plugin packages](https://hosihikariframework.github.io/plugin-package/)
- [C# plugins](https://hosihikariframework.github.io/authoring-csharp/)
- [Out-of-process plugins](https://hosihikariframework.github.io/authoring-rpc/)
- [Examples](https://github.com/HosihikariFramework/hosihikariframework.github.io/tree/main/examples)
- [Troubleshooting](https://hosihikariframework.github.io/troubleshooting/)

## Install

Run in the server root:

```powershell
# LeviLamina
lip install github.com/HosihikariFramework/Shim

# Endstone
lip install github.com/HosihikariFramework/Shim#endstone

# Install providers as needed
lip install github.com/HosihikariFramework/CSharpProvider
lip install github.com/HosihikariFramework/FSharpProvider
lip install github.com/HosihikariFramework/RpcProvider
```

A plugin package is a directory under `plugins/` whose name matches `name` in its manifest. Start with the [quick start](https://hosihikariframework.github.io/quick-start/).

## Repositories

| Repository | Purpose |
|---|---|
| [Shim](https://github.com/HosihikariFramework/Shim) | Native HostingShim: hosts the CLR in BDS and hands control to the managed core |
| [PluginManagement](https://github.com/HosihikariFramework/PluginManagement) | Managed core: discovery, dependency graph, isolated loading, lifecycle, unload verification |
| [Abstractions](https://github.com/HosihikariFramework/Abstractions) | Plugin contract, published on [NuGet](https://www.nuget.org/packages/Hosihikari.Abstractions) |
| [CSharpProvider](https://github.com/HosihikariFramework/CSharpProvider) | C# script plugins, compiled at load with Roslyn |
| [FSharpProvider](https://github.com/HosihikariFramework/FSharpProvider) | F# script plugins, compiled at load |
| [RpcProvider](https://github.com/HosihikariFramework/RpcProvider) | Out-of-process plugins over line-delimited JSON-RPC 2.0, with Node/QuickJS/Python/Java/Kotlin bindings |
| [Hosihikari.McMaster.NETCore.Plugins](https://github.com/HosihikariFramework/Hosihikari.McMaster.NETCore.Plugins) | Fork of McMaster.NETCore.Plugins with RID-first native library resolution |
| [HOCON](https://github.com/HosihikariFramework/HOCON) | HOCON implementation used for framework configuration |
| [hosihikariframework.github.io](https://github.com/HosihikariFramework/hosihikariframework.github.io) | Documentation site and example plugins |

## License and trust boundary

LGPL-3.0-or-later. Plugins run in the same process as the host and are fully trusted; do not load untrusted plugins.
