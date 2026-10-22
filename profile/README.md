# Hosihikari Framework

<table align="right">
  <tr>
    <td align="right">
      <img src="assets/mascot.png" width="240" alt="Hosi Hikari, the Hosihikari Framework mascot"><br>
      <sub>Art by 墨鱼纸鸢</sub>
    </td>
  </tr>
</table>

[English](README.md) | [简体中文](README.zh_hans.md)

A plugin container that brings .NET plugins to Minecraft Bedrock Dedicated Server (BDS). Also known as 星光框架.

A carrier (LeviLamina, Endstone, or the Linux self-hosted carrier) loads the native HostingShim, which hosts the CLR inside the server process. The managed PluginManager discovers plugins, resolves dependencies, isolates them, and drives their lifecycle. C# and F# loaders compile source at load; RpcLoader runs plugins out of process; the core's built-in loader handles precompiled assemblies.

**Current release**: Hosihikari.Plugin.Abstractions 1.1.0 · PluginManager v1.1.0 · HostingShim v1.1.0 · C#/F#/RPC Loaders v1.0.0 · Plugin.Build / Testing 1.0.0 · Plugin Templates 1.0.1  
**Platforms**: Windows x64 (LeviLamina 26.51, Endstone 0.11) · Linux x64 (Endstone 0.11, self-hosted BDS 1.21.3)  
**Contract**: `api_version` 2 · manifest `manifest_version` 1

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
# self-hosted Linux
lip install github.com/HosihikariFramework/HostingShim

# LeviLamina
lip install github.com/HosihikariFramework/HostingShim#levilamina

# Endstone (Windows / Linux)
lip install github.com/HosihikariFramework/HostingShim#endstone

# In-process source loaders
lip install github.com/HosihikariFramework/CSharpLoader
lip install github.com/HosihikariFramework/FSharpLoader

# Out-of-process loader
lip install github.com/HosihikariFramework/RpcLoader

# Precompiled plugin templates
dotnet new install Hosihikari.Plugin.Templates::1.0.1

# Plugin project build and test packages
dotnet add package Hosihikari.Plugin.Build --version 1.0.0
dotnet add package Hosihikari.Testing --version 1.0.0
```

A plugin package is a directory under `plugins/` whose name matches `name` in its manifest. Start with the [quick start](https://hosihikariframework.github.io/quick-start/).

## Repositories

| Repository | Purpose |
|---|---|
| [HostingShim](https://github.com/HosihikariFramework/HostingShim) | Native hosting shim: hosts the CLR in BDS and hands control to the managed core |
| [PluginManager](https://github.com/HosihikariFramework/PluginManager) | Managed core: discovery, dependency graph, isolated loading, lifecycle, unload verification |
| [PluginAbstractions](https://github.com/HosihikariFramework/PluginAbstractions) | Plugin contract, published on [NuGet](https://www.nuget.org/packages/Hosihikari.Plugin.Abstractions) |
| [CSharpLoader](https://github.com/HosihikariFramework/CSharpLoader) | C# source loader: Roslyn compiles at load into a collectible ALC |
| [FSharpLoader](https://github.com/HosihikariFramework/FSharpLoader) | F# source loader: compiles at load into a collectible ALC |
| [RpcLoader](https://github.com/HosihikariFramework/RpcLoader) | Out-of-process loader over line-delimited JSON-RPC 2.0, with Node/QuickJS/Python/Java/Kotlin bindings |
| [CSharpPluginTemplate](https://github.com/HosihikariFramework/CSharpPluginTemplate) | Source C# plugin template |
| [FSharpPluginTemplate](https://github.com/HosihikariFramework/FSharpPluginTemplate) | Source F# plugin template |
| [RpcPluginTemplate](https://github.com/HosihikariFramework/RpcPluginTemplate) | Out-of-process templates: Node.js/TypeScript, Python, Kotlin/JVM |
| [Hosihikari.McMaster.NETCore.Plugins](https://github.com/HosihikariFramework/Hosihikari.McMaster.NETCore.Plugins) | Fork of McMaster.NETCore.Plugins with RID-first native library resolution |
| [HOCON](https://github.com/HosihikariFramework/HOCON) | HOCON implementation used for framework configuration |
| [hosihikariframework.github.io](https://github.com/HosihikariFramework/hosihikariframework.github.io) | Documentation site and example plugins |

## License and trust boundary

LGPL-3.0-or-later for the framework and loaders. Hosihikari.Plugin.Abstractions 0.7.1 and later are MIT; the 0.7.0 package remains LGPL-3.0-or-later. Plugin templates and documentation code examples are MIT-0; documentation prose is CC BY-SA 4.0. In-process plugins run in the host process; cross-process plugins run in a child process. Both are fully trusted, and the framework provides no permission boundary; do not load untrusted plugins.
