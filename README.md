# 🧩 LogViewer Configuration

This repository contains the **public YAML configuration files** used by the LogViewer tool.

The configuration system is designed to be **modular**, **mergeable**, and **fallback-safe**, supporting both online use and offline usage via local caching.

➡️ View/edit directly in VSCode online:  
[https://vscode.dev/github/KooleControls/LogViewerConfig](https://vscode.dev/github/KooleControls/LogViewerConfig)



## 📂 Repository Layout

```
Sources.yaml                # Top-level config listing all config files
schema.json                 # JSON schema for VSCode validation/autocomplete
Organisations.yaml          # Contains API settings (e.g., credentials or endpoints)

Gateway/
  ├─ Gateway.yaml           # Entry point for Gateway config group
  ├─ ...
```


## 📁 Root Config Location

The application reads the main config from:

```
%LOCALAPPDATA%\LogViewer\config.yaml
```

If it doesn’t exist, it is created with a default that points to this repository.



## 🔗 Example Root Config File

This file defines which sources should be loaded:

```yaml
sources:
  - https://raw.githubusercontent.com/KooleControls/LogViewerConfig/main/Sources.yaml
```

Each file can include more sources using the `sources:` property, enabling recursive inclusion of config fragments grouped by device, domain, or purpose.



### ✍️ Overriding with Local Files

You can extend the configuration by pointing to local files:

```yaml
# %LOCALAPPDATA%\LogViewer\config.yaml
sources:
  - https://raw.githubusercontent.com/KooleControls/LogViewerConfig/main/Sources.yaml
  - C:\Path\To\Your\Local\Dev\Copy\Sources.yaml
```

Or you can fully override it (ignoring the public config):

```yaml
sources:
#  - https://raw.githubusercontent.com/KooleControls/LogViewerConfig/main/Sources.yaml
  - C:\Path\To\Your\Local\Dev\Copy\Sources.yaml
```



## 🔁 How Merging Works

- Config files are **merged in order** (from top to bottom).
- Each file may load other files recursively.
- Duplicate keys (e.g., a profile named `Gateway`) are **merged by key**.
- Lists like `traces:` are grouped by name and merged using type-specific rules.



## 💾 Caching Behavior

When a remote file is loaded:

- It is cached locally at  
  `%LOCALAPPDATA%\LogViewer\cache\{hash}.yaml`
- If the app is offline or the remote is unreachable, the cached version is used.
- Cached files are not automatically deleted, ensuring offline fallback is always available.



## ✅ Schema Support

The included `schema.json` provides autocomplete and validation support in VSCode (with the YAML extension).

To enable schema hints automatically, add this to your VSCode `settings.json`:

```json
"yaml.schemas": {
  "https://raw.githubusercontent.com/KooleControls/LogViewerConfig/main/schema.json": "/*.yaml"
}
```

