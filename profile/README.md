# Hosihikari Framework

<table align="right">
  <tr>
    <td align="right">
      <img src="assets/mascot.png" width="240" alt="Hosi Hikari"><br>
      <sub>Art by 墨鱼纸鸢</sub>
    </td>
  </tr>
</table>

[English](README.md) | [简体中文](README.zh_hans.md)

Loads and manages .NET plugins inside Minecraft Bedrock Dedicated Server (BDS). Also known as 星光框架.

A carrier (LeviLamina, Endstone, or the Linux self-hosted carrier) loads the native HostingShim, which hosts the CLR inside the server process. The managed PluginManager discovers plugins, resolves dependencies, isolates them, and drives their lifecycle. C# and F# loaders compile source at load; RpcLoader runs plugins out of process; the core's built-in loader handles precompiled assemblies.

**Current release**: Hosihikari.Plugin.Abstractions 1.1.0 · PluginManager v1.2.0 · HostingShim v1.2.1 · C#/F#/RPC Loaders v1.1.0 · Plugin.Build / Testing 1.0.0 · Plugin Templates 1.0.1  
**Platforms**: Windows x64 (LeviLamina 26.51, Endstone 0.11, self-hosted BDS 1.21.3.01) · Linux x64 (Endstone 0.11, self-hosted BDS 1.21.3)  
**Contract**: `api_version` 2 · manifest `manifest_version` 1

## Documentation

- [Online documentation](https://hoshi.srcz.one/) · [简体中文](https://hoshi.srcz.one/zh/)
- [Running a server](https://hoshi.srcz.one/framework/server/) — carriers, install, updating, recovery
- [Writing plugins](https://hoshi.srcz.one/framework/develop/) — contract, packages, loaders
- [Embedding the manager](https://hoshi.srcz.one/framework/embed/)
- [Examples](https://github.com/Hosihikari/hosihikari.github.io/tree/main/examples)

## Install

Run in the server root:

```powershell
sk init
sk add hosihikari-hosting-levilamina     # LeviLamina
# or: sk add hosihikari-hosting-endstone
# or: sk add hosihikari-hosting-selfhosted

# In-process source loaders
sk add hosihikari-csharp
sk add hosihikari-fsharp

# Out-of-process loader
sk add hosihikari-rpc

# Precompiled plugin templates
dotnet new install Hosihikari.Plugin.Templates::1.0.1
```

A plugin package is a directory under `plugins/` whose name matches `name` in its manifest. Start with the [first plugin](https://hoshi.srcz.one/framework/develop/first-plugin/).

## Plugin project packages

In the plugin project directory, add the build package:

```powershell
dotnet add package Hosihikari.Plugin.Build --version 1.0.0
```

In the test project directory, add the test package:

```powershell
dotnet add package Hosihikari.Testing --version 1.0.0
```

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
| [DotNetCorePlugins](https://github.com/HosihikariFramework/DotNetCorePlugins) | Fork of McMaster.NETCore.Plugins with RID-first native library resolution |
| [HOCON](https://github.com/HosihikariFramework/HOCON) | HOCON implementation used for framework configuration |
| [hosihikari.github.io](https://github.com/Hosihikari/hosihikari.github.io) | Documentation site and example plugins |

## License and trust boundary

LGPL-3.0-or-later for the framework and loaders. Hosihikari.Plugin.Abstractions 0.7.1 and later are MIT; the 0.7.0 package remains LGPL-3.0-or-later. Plugin templates and documentation code examples are MIT-0; documentation prose is CC BY-SA 4.0. In-process plugins run in the host process; cross-process plugins run in a child process. Both are fully trusted, and the framework provides no permission boundary; do not load untrusted plugins.
