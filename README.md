# Manage NuGet Packages

Manage NuGet packages directly in VS Code.

## How to use

1. In the Explorer, right-click a `.csproj`, `.fsproj`, or `.vbproj` file.
2. Select **Manage NuGet Packages**.

To manage packages for a solution, right-click an `.sln` or `.slnx` file and select **Manage NuGet Packages for Solution**. You can also run these commands from the Command Palette (`Ctrl+Shift+P`).

## Features

- Search for packages by name in a specific source or in **All** sources.
- Select the project that will receive the change.
- Install a specific package version.
- Update or uninstall installed packages.
- Update multiple packages at once.
- View package descriptions, authors, licenses, dependencies, tags, and links.
- View vulnerability alerts and their security advisories.

Changes are applied to the project using the `dotnet` CLI. Make sure the .NET SDK is installed and available in your `PATH`.

## Package sources configuration

Sources are loaded from the following locations, in this order:

- user configuration file: `%APPDATA%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux);
- `*.config` files in `%APPDATA%\NuGet\config` (Windows) or `~/.nuget/NuGet/config` (Mac/Linux);
- `NuGet.Config` in the project folder and its parent folders.

Standard NuGet rules, including `<clear />`, `<add />`, `<remove />`, and disabled sources, are respected. In the panel, **All** searches all loaded sources.

Example of a public or private source:

```xml
<configuration>
  <packageSources>
    <add key="NuGet.org" value="https://api.nuget.org/v3/index.json" />
    <add key="Private" value="https://nuget.example.com/v3/index.json" />
  </packageSources>
</configuration>
```

### Credentials for private feeds

For searches on a private feed, add `Username` and `ClearTextPassword` under `packageSourceCredentials`:

```xml
<packageSourceCredentials>
  <Private>
    <add key="Username" value="my-username" />
    <add key="ClearTextPassword" value="my-password" />
  </Private>
</packageSourceCredentials>
```

The extension uses this information in memory to create authentication. Passwords are not written to logs. Encrypted `Password` values are not decrypted; configure the Credential Provider required by the feed so that `dotnet` can authenticate.
