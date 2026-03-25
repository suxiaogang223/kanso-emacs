# ❄️ C/C++ Development Workflow

The C/C++ configuration (`lisp/lang-cc.el`) is built to handle complex codebases by deeply integrating with modern tools like `clangd` and `CMake`.

---

## ✨ Features

- **Advanced LSP Intelligence**: Powered by `clangd` for highly accurate completions, cross-referencing, and refactoring.
- **Smart Build System Detection**: Automatically locates `compile_commands.json` in common build directories (e.g., `build/`, `out/`).
- **Zero-Config CMake Setup**: Automatically generates compilation databases for fresh CMake projects.
- **Manual Formatting**: Binds `clang-format` to a dedicated shortcut.

---

## 📦 Prerequisites

To enable all features, ensure the following CLI tools are available in your `PATH`:

```bash
# macOS
brew install llvm

# Ubuntu/Debian
sudo apt install clangd clang-format
```

The configuration uses `clangd` for the language server and `clang-format` for buffer formatting.

---

## ⌨️ Daily Workflow & Keybindings

### 1. Building & Compiling
Emacs automatically configures the `compile-command` by searching for `Makefile`, CMake build directories (`build/`, `out/`), or a root `CMakeLists.txt`.

| Shortcut | Action |
| :--- | :--- |
| `C-c C-c` | Compile the current project or file. |
| `C-c C-k` | Recompile using the last compilation command. |
| `C-c C-m` | Configure the current CMake project manually. |

*Tip*: If a `CMakeLists.txt` is found but no build directory exists, it will automatically setup the build environment and export compilation commands.

### 2. Running
For single-file programs, you can compile and run them quickly:

| Shortcut | Action |
| :--- | :--- |
| `C-c C-r` | Run the current single-file C or C++ binary. |

### 3. Formatting
Maintain a consistent code style across your project:

| Shortcut | Action |
| :--- | :--- |
| `C-c C-f` | Format the current buffer with `clang-format`. |

*Note*: Ensure you have a `.clang-format` file in your project root to define your preferred style rules.

---

## ⚙️ Under the Hood

- **`eglot` & `clangd`**: We dynamically pass `--compile-commands-dir` to `clangd` when a build directory is found, ensuring the language server fully understands your project's include paths and macros.
- **`c-ts-mode` & `c++-ts-mode`**: We automatically remap standard `c-mode` and `c++-mode` to their tree-sitter backed versions if the grammars are installed.
- **Tree-sitter**: Run `M-x install-c/c++-treesit-grammars` to install grammars for both C and C++ for pixel-perfect syntax highlighting.
