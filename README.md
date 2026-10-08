# Universal Save Editor

An offline-capable, cross-engine game save editor, batch management suite, and desktop application for modern indie and retro game titles (RPG Maker MV/MZ/XP/VX/Ace, WOLF RPG, Godot, Ren'Py, and generic formats).

---

## Documentation & Technical Guides

Comprehensive guides and specifications are located in the **[`docs/`](./docs/README.md)** directory:

- 📖 **[System Architecture & Design](./docs/ARCHITECTURE.md)**: Data lifecycle, component hierarchy, and state management.
- 🎮 **[Supported Engines & Formats](./docs/SUPPORTED_FORMATS.md)**: Technical breakdown of Ruby Marshal, Shift-JIS, LZ-String, WOLF RPG binary, and Python Pickle.
- 🔌 **[Plugin System & SDK Guide](./docs/PLUGIN_SYSTEM.md)**: How to write custom `SavePlugin` format decoders and encoders.
- ⚙️ **[Core Modules Specification](./docs/CORE_MODULES.md)**: Detailed reference for `TreeSearchManager`, `UndoRedoManager`, `BatchRenameManager`, etc.
- 🔍 **[Search Syntax Guide](./docs/SEARCH_SYNTAX.md)**: Complete guide to query tokens (`prop:`, `val:`, `type:`, numeric operators `>`, `<`, `=`).
- ⌨️ **[Keyboard Shortcuts](./docs/KEYBOARD_SHORTCUTS.md)**: Quick reference for desktop and web hotkeys.
- 🚀 **[Tauri v2 Desktop Compilation](./docs/DESKTOP_BUILD_TAURI.md)**: Compiling standalone lightweight executables for Windows, macOS, and Linux.
- 🗺️ **[Roadmap & Future Extensions](./docs/ROADMAP_AND_EXTENSIONS.md)**: Technical review and prioritized future enhancement roadmap.

---

## Desktop App Compilation (Tauri v2)

This project is configured with **Tauri v2** for high performance and ultra-lightweight desktop executables.

### Prerequisites for Building Locally
- **Node.js** (v18+)
- **Rust toolchain** (installed via [rustup.rs](https://rustup.rs/))
  - *On Windows*: Microsoft C++ Build Tools (via Visual Studio Installer with the "Desktop development with C++" workload).
  - *On Linux*: `libwebkit2gtk-4.1-dev`, `build-essential`, `curl`, `wget`, `file`, `libssl-dev`, `libgtk-3-dev`.
  - *On macOS*: Xcode Command Line Tools (`xcode-select --install`).

### How to Build
1. **Install Frontend Dependencies**:
   ```bash
   npm install
   ```

2. **Run in Development Mode**:
   ```bash
   npm run tauri:dev
   ```

3. **Compile Release Executable**:
   ```bash
   npm run build:exe
   ```
   *(or `npm run tauri:build`)*

4. **Locate the Output Binary**:
   Compiled standalone installers and portable executables (`.exe` on Windows, `.dmg` / `.app` on macOS, `.deb` / `.AppImage` on Linux) will be generated inside `src-tauri/target/release/bundle/`.

### Japanese Encoding Support
The editor now includes native Japanese `Shift-JIS` decoding and encoding specifically designed for:
- **RPG Maker XP / VX / VX Ace** (`.rxdata`, `.rvdata`, `.rvdata2`) via Ruby Marshal format parsing.
- **WOLF RPG Editor** (`.sav`) via a robust length-prefixed string scanning heuristic.

### Batch Save Renaming Utility
A comprehensive batch renaming utility is integrated directly into the workspace file management system:
- **Pattern Builder**: Dynamic placeholders including `{n}` (sequential number), `{0n}` (2-digit zero padded), `{00n}` (3-digit zero padded), `{name}` (original name), `{ext}` (extension), `{game}` (game title), and `{date}` (`YYYY-MM-DD`).
- **Engine Presets**: 1-click presets for RPG Maker MV/MZ (`file{n}.rpgsave`/`.rmmzsave`), RPG Maker XP/VX/Ace (`Save{0n}.rvdata2`), WOLF RPG (`Save{0n}.sav`), and timestamped backups.
- **Find & Replace / Prefix & Suffix / Letter Case**: Regex-capable replacement, custom prefixes/suffixes, and case normalization (snake_case, camelCase, lowercase, UPPERCASE).
- **Safety & Collision Detection**: Live side-by-side preview, automatic conflict resolution, validation of illegal characters, and optional `.bak` backup creation prior to renaming.
- **Access Points**: Available in the **Workspace Sidebar** Saves tab, the **Workspace Overview** dashboard, and under the **Tools** menu.

