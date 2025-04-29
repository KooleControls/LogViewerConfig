# 🧩 LogViewer Configuration

This repository contains the **public YAML configuration files** used by the LogViewer tool.

The configuration system is designed to make it easy to extend, override, and work offline.

➡️ View/edit directly in VSCode online:  
[https://vscode.dev/github/KooleControls/LogViewerConfig](https://vscode.dev/github/KooleControls/LogViewerConfig)


## ✍️ Add your own organisations

You can add custom organisation settings by creating a local YAML file:

```yaml
#%LOCALAPPDATA%\LogViewer\user\organisations.yaml
organisations:
  - name: My Company
    uri: https://api.mycompany.com/api
    organisationId: 42
    authenticationMethod: GetOAuth2_OpenIdConnectClient
    authPath: https://accounts.mycompany.com/realms/myrealm
```

Next add a new source to the config file on your pc.
If it doesn’t exist, you can start the tool, it will be created automatically.

```yaml
#%LOCALAPPDATA%\LogViewer\config.yaml
sources:
  - https://raw.githubusercontent.com/KooleControls/LogViewerConfig/main/Sources.yaml
  - %LOCALAPPDATA%\LogViewer\user\organisations.yaml
```

**Or override** the configuration entirely:

```yaml
sources:
#  - https://raw.githubusercontent.com/KooleControls/LogViewerConfig/main/Sources.yaml
  - %LOCALAPPDATA%\LogViewer\user\organisations.yaml
```


## ✅ Features Overview

| Feature | Description |
|:--------|:------------|
| 🔄 **Merging** | Profiles, traces, and settings are merged based on their name/type |
| 🔗 **Recursive loading** | Config files can include other sources recursively |
| 💾 **Caching** | Remote configs are cached locally for offline use |
| ✍️ **Schema-based editing** | VSCode supports YAML validation and autocomplete via `schema.json` |
| 🔒 **Offline fallback** | Always uses the last cached version if offline or unreachable |


