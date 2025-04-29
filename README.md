# 🧩 LogViewer Configuration

This repository contains the **public YAML configuration files** used by the LogViewer tool.

The configuration system is designed to be **modular**, **mergeable**, and **fallback-safe**, supporting both online use and offline usage with caching.


## 📂 Repository Layout

```
Sources.yaml                 # Top-level config listing all profiles/groups
schema.json                 # JSON schema for editor validation
Organisations.yaml          # Optional shared config
Gateway/
  ├─ Gateway.yaml           # Entry point for Gateway config group
  ├─ IndoorUnit0Trace.yaml  # Traces for IU 0
  ├─ ...
  └─ UnknownLogcodes.yaml   # Catch-all trace file
```

---

## 🔗 Configuration Sources

The application loads configuration from one or more **sources**.

A typical `config.yaml` looks like:

```yaml
sources:
  - https://raw.githubusercontent.com/your-org/logviewerconfig/main/Sources.yaml
```

Each source can load additional sources recursively (via the `sources:` property in YAML), enabling grouped or layered configurations.

---

## 🗂 How Merging Works

- Config files are **merged in order**, recursively.
- The base config loads first, then overlay files merge in.
- Objects with the same key (e.g., a profile with the same name) are merged.
- Lists of named items (like `traces`) are grouped by name and merged by type.
- The merging behavior is defined in code using a flexible "type merger" system.

---

## 💾 Caching Behavior

When a file is loaded from a remote source:
- It is downloaded and saved to `%LOCALAPPDATA%/LogViewer/cache/{hash}.yaml`.
- If the app is **offline**, the cached copy is used.
- Cache is not automatically purged — so you always have a last known good version.

---

## 📁 Local Configuration File

The app looks for a config file here:

```
%LOCALAPPDATA%\LogViewer\config.yaml
```

This file defines which source(s) to load.  
If it doesn’t exist, it is initialized with a default that points to this repository.

### ✍️ To override locally:

1. Create or edit the config:

```yaml
# %LOCALAPPDATA%\LogViewer\config.yaml
sources:
  - C:\Path\To\Your\Local\Dev\Copy\Sources.yaml
```

2. You can now develop/test against local YAML files instead of the online repo.

---

## 🛠 Editing Config Files

- Each group (like `Gateway/`) has a main file (`Gateway.yaml`) that includes others.
- Files are linked together via the `sources:` array.
- You can validate changes using the JSON Schema (`schema.json`) in this repo.
- Editors like VSCode can use this schema for autocomplete and validation.

---

## ✅ Best Practices

- Use consistent naming: `IndoorUnit0Trace.yaml`, not `Indoorunit 0 traces.yaml`
- Avoid spaces in filenames
- Use the `$schema` property in local YAML files for schema validation:

```yaml
$schema: https://raw.githubusercontent.com/your-org/logviewerconfig/main/schema.json
```

---

## 🤖 Schema Validation

To enable YAML validation in VSCode:
1. Install the **YAML Language Support** extension.
2. Add this to your `settings.json`:

```json
"yaml.schemas": {
  "https://raw.githubusercontent.com/your-org/logviewerconfig/main/schema.json": "/*.yaml"
}
```

Now you’ll get real-time validation and autocomplete when editing the YAML files.

---

## 📢 Contributions

You are welcome to:
- Add new profiles or trace files
- Fix or improve existing mappings
- Submit suggestions via issues or pull requests

---

## 🧠 Need Help?

Ping the developers maintaining LogViewer, or check the internal documentation for advanced type merging and trace logic.

---
```

---

Let me know if you'd like to generate a clickable directory tree or include example trace definitions as well!

https://vscode.dev/github/KooleControls/LogViewerConfig

