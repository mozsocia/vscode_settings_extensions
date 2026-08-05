**Lite XL Full Setup Guide** (for future reference)

This covers installing Lite XL, the plugin manager (`lpm`), the integrated terminal plugin, and the treeview-extender plugin (for Copy To / Duplicate / Move To).

---

### 1. Install Lite XL

Go to the official releases:  
**https://github.com/lite-xl/lite-xl/releases/latest**

#### Windows
- Prefer the **Setup** installer (`.exe`).
- Or download the ZIP, extract it somewhere, and run `lite-xl.exe`.
- (Optional) Chocolatey: `choco install lite-xl`  
- (Optional) Scoop:  
  ```powershell
  scoop bucket add extras
  scoop install lite-xl
  ```

#### Linux
- **AppImage** (easiest): Download → `chmod +x LiteXL-*.AppImage` → run it.
- **Tarball** (recommended permanent install):
  ```bash
  tar -xzf lite-xl-*.tar.gz
  cd lite-xl
  rm -rf $HOME/.local/share/lite-xl $HOME/.local/bin/lite-xl
  mkdir -p $HOME/.local/bin && cp lite-xl $HOME/.local/bin/
  mkdir -p $HOME/.local/share/lite-xl && cp -r data/* $HOME/.local/share/lite-xl/
  ```
  Add to PATH if needed:
  ```bash
  echo 'export PATH="$PATH:$HOME/.local/bin"' >> ~/.bashrc
  source ~/.bashrc
  ```
- Some distros have packages (Arch: `pacman -S lite-xl`, Fedora: `dnf install lite-xl`, etc.).

#### macOS
- Download the DMG → drag Lite XL to Applications.
- First launch: right-click → Open (or run `xattr -cr /Applications/Lite\ XL.app` on older versions).

**Config location (USERDIR)**  
- Linux/macOS: `~/.config/lite-xl`  
- Windows: `C:\Users\<you>\.config\lite-xl`

---

### 2. Install the Plugin Manager (`lpm`)

`lpm` is a standalone CLI tool. Run these in a **system terminal** (not inside Lite XL).

#### Linux / macOS
```bash
wget https://github.com/lite-xl/lite-xl-plugin-manager/releases/download/latest/lpm.$(uname -m | sed 's/arm64/aarch64/')-$(uname | tr '[:upper:]' '[:lower:]') -O lpm
chmod +x lpm
# Optional: move to PATH
sudo mv lpm /usr/local/bin/
```

#### Windows (PowerShell)
```powershell
Invoke-WebRequest -Uri "https://github.com/lite-xl/lite-xl-plugin-manager/releases/download/latest/lpm.x86_64-windows.exe" -OutFile "lpm.exe"
```
(Keep `lpm.exe` somewhere in your PATH or run it with `.\lpm.exe`.)

#### Install the GUI plugin manager (recommended)
```bash
lpm install plugin_manager --assume-yes
```
(On Windows use `.\lpm.exe install plugin_manager --assume-yes`)

Restart Lite XL (`Ctrl + Alt + R`).  
You can now open **Plugin Manager: Show** from the command palette (`Ctrl + Shift + P`).

---

### 3. Install the two plugins

Still in a system terminal:

```bash
# Integrated terminal
lpm install terminal

# TreeView context menu extras (Copy To / Duplicate / Move To)
lpm install treeview-extender

# git

lpm install scm
lpm install gitdiff_highlight   # optional but recommended
lpm install gitblame            # optional
```

Restart Lite XL (`Ctrl + Alt + R`).

#### Manual install (if lpm fails)

**Terminal**
```bash
# Linux/macOS example
cd ~/.config/lite-xl/plugins
# Follow instructions on https://github.com/adamharrison/lite-xl-terminal
# (usually involves downloading the prebuilt binary + lua files)
```

**treeview-extender**
```bash
cd ~/.config/lite-xl/plugins
git clone https://github.com/juliardi/lite-xl-treeview-extender.git treeview-extender
```

---

### 4. How to use them

| Feature | How |
|---------|-----|
| Toggle terminal drawer | `Alt + T` |
| Open terminal as tab | `Ctrl + Shift + `` (backtick) |
| Right-click file/folder in sidebar | Now shows **Copy To…**, **Duplicate File…**, **Move To…** |

---

### 5. Useful future commands

```bash
lpm upgrade                  # Update all plugins
lpm list                     # See installed plugins
lpm uninstall <plugin>       # Remove a plugin
lpm --help
```

---

### Quick checklist for a new machine

1. Download & install Lite XL from GitHub Releases  
2. Install `lpm` (wget / Invoke-WebRequest)  
3. `lpm install plugin_manager --assume-yes`  
4. `lpm install terminal treeview-extender`  
5. Restart Lite XL (`Ctrl + Alt + R`)

That’s it. Keep this guide and you’ll be able to recreate the exact same setup anytime.
