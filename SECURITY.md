# Security policy

## Supported versions

Security fixes land on the latest release line of each component. The line before it receives
fixes while the next line is being prepared. Older lines and pre-release builds do not.

| Component | Supported |
| --- | --- |
| PluginAbstractions, PluginManager, HostingShim | 1.1.x |
| C# / F# / RPC Loaders | 1.0.x |
| Plugin.Build, Testing, Plugin Templates | 1.0.x |

## Reporting a vulnerability

Use **Security → Report a vulnerability** in the repository that owns the component. The report
stays private until an advisory is published. This is enabled in every repository of the
organization.

Include the affected component and version, the server platform and carrier
(LeviLamina, Endstone, or self-hosted), steps to reproduce, and the impact you expect. Remove
secrets, server logs with IP addresses, and world data.

If the component is unclear, report against
[PluginManager](https://github.com/HosihikariFramework/PluginManager/security/advisories/new);
the report can be moved later.

Do not open a public issue for a vulnerability until an advisory exists.

## What to expect

- Acknowledgement within seven days.
- An assessment and a fix plan, or a reason the report is out of scope.
- Credit in the advisory unless you ask otherwise.

## Scope

Plugins run in the server process with the same privileges as the server, and the framework
provides isolation, not a permission boundary. Two consequences for reports:

- **In scope**: anything the framework itself mishandles — manifest and package validation,
  assembly and native library resolution, loader diagnostics, unload verification, the RPC bridge
  and its subprocess handling, the packaging tool, and the release workflows.
- **Out of scope as framework bugs**: a plugin reading files, opening sockets, or crashing the
  process on purpose. A malicious or careless plugin is expected to be able to do that. Report it
  only when the framework should have stopped it, for example a package escaping its directory
  during validation.
- **Out of scope entirely**: vulnerabilities in a carrier (LeviLamina, Endstone), in BDS itself,
  and in third-party dependencies. Report those upstream; tell us as well if the framework should
  pin or work around the issue.

## Building and running

Build and test commands live in each repository's `AGENTS.md`. A fix is expected to arrive as a
pull request that references the advisory.
