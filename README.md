# EasyDBCUpdater

**EasyDBCUpdater** is a small Windows tool that automates the most annoying part of working with the WoW Spell Editor:  
**moving exported Spell DBCs and patch files to the correct server and client locations with a single click.**

No more manual copying, no more missed files, no more forgetting to clear client cache.

---

## ✨ Features

- **One-click update**
  - Copies exported Spell DBC files into your **server DBC folder**
  - Copies either:
    - DBCs into a **predefined client patch folder**, or
    - The generated `patch-*.MPQ` directly into the client `Data` folder
- **Supports both server layouts**
  - Standard server build (`/Data/dbc`)
  - Repack-style layout
- **Automatic client cache cleanup**
- **Configurable paths via JSON**
- **Simple logging with timestamps**

---

## 🛠️ How It Works

EasyDBCUpdater watches the **Spell Editor `Export` folder** and:

1. Copies all exported **DBC files** (non-patch files):
   - To the server `Data/dbc` folder  
   - Or to a repack `Data/dbc` folder
2. Handles client updates:
   - If using a **pre-made patch folder** → copies DBCs into `DBFilesClient`
   - Otherwise → copies the generated `patch-*.MPQ` into the client `Data` folder
3. Deletes the client `Cache` folder (if present)
4. Logs every action in the UI

---

## 📁 Expected Folder Structure

### Spell Editor
```
WoW Spell Editor/
└── Export/
├── Spell.dbc
├── SpellEffect.dbc
└── patch-A.MPQ
```

### Server
```
ServerRoot/
└── Data/
└── dbc/
```

### Client (Option 1: Pre-made Patch Folder)
```
WoW Client/
└── Data/
└── patch-Z.MPQ/
└── DBFilesClient/
```

### Client (Option 2: Direct Patch)
```
WoW Client/
└── Data/
└── patch-A.MPQ
```
---

## ⚙️ Configuration

EasyDBCUpdater is configured using a simple JSON file.

### Example `config.json`
```json
{
  "ClientRootPath": "G:/WoW-Clients/Server-Client",
  "SpellEditorRootPath": "G:/@Tools/WoW Spell Editor",
  "ServerRootPath": "G:/SylCore/Build/bin/RelWithDebInfo",
  "ClientPredefindPatchRootPath": "G:/WoW-Clients/Server-Client/Data/patch-Z.MPQ",

  "PatchName": "patch-A.MPQ",
  "UsePreMadePatchFolder": true
}
```

Config Options Explained
| Setting                        | Description                                                                  |
| ------------------------------ | ---------------------------------------------------------------------------- |
| `ClientRootPath`               | Root folder of the WoW client                                                |
| `SpellEditorRootPath`          | Root folder of WoW Spell Editor                                              |
| `ServerRootPath`               | Server build root (contains `Data/dbc`)                                      |
| `ClientPredefindPatchRootPath` | Path to an existing patch folder                                             |
| `PatchName`                    | Name of the generated patch MPQ                                              |
| `UsePreMadePatchFolder`        | `true` = copy DBCs into patch folder<br>`false` = copy patch MPQ into client |

---

## 🖱️ Usage

1. Export spells from WoW Spell Editor
2. Launch EasyDBCUpdater
3. Click:
   - Update Server → copies to normal server DBC & client
   - Update Repack → copies to repack DBC & client
4. Client cache is cleared automatically
5. Launch client & server 🚀

## 🧾 Logging

The built-in log shows:
 - File copy operations
 - Patch updates
 - Cache deletion
 - Timestamps for every action
Example:
```
[14:32:01] Started moving Spell DBC files from 'Export' folder to server data DBC...
[14:32:02] Spell DBC files has been moved successfully to the server DBC!
[14:32:03] Client cache has been deleted successfully!
[14:32:03] Server & Client has been updated!
```

---

## 🚧 Notes & Limitations
 - Overwrites existing files without prompting
 - Assumes Spell Editor export format
 - Windows only
 - Does not validate DBC integrity (by design)

## 📜 License
Use freely for private server & repack development.
No warranty — use at your own risk.

---

❤️ Credits
Created to simplify WoW spell development workflows
and remove one more repetitive task from daily modding.

EasyDBCUpdater — Export. Click. Play.
