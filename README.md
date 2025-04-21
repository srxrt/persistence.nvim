# 💾 Persistence

A lightweight session management plugin for Neovim, originally forked from [folke/persistence.nvim](https://github.com/folke/persistence.nvim).

## ✨ Features

- 📦 Automatically saves your session on exit under `~/.local/state/nvim/sessions` 
- 🚀 Automatically loads your last session on startup (configurable)
- 🧠 Smart logic: does **not** autoload sessions if Neovim is launched without any file arguments (e.g., just running `nvim` to show a dashboard)
- Provides simple API to restore the current or last session

## 📚 Description

**Persistence** is a Neovim plugin for managing sessions — preserving buffers, window layout, and more across restarts.

This version builds upon the original by adding **session autoloading** functionality. It ensures a seamless experience by **only loading sessions when appropriate**, such as when opening Neovim with files or projects, and **skipping session restore** when launched with no arguments (e.g., opening a dashboard via `nvim` alone).


## ⚡️ Requirements

- Neovim >= 0.7.2

## 📦 Installation

Install the plugin with your preferred package manager:

### [lazy.nvim](https://github.com/folke/lazy.nvim)

```lua
-- Lua
{
  "viminizer/persistence.nvim",
  event = "BufReadPre", -- this will only start session saving when an actual file was opened
  opts = {
    -- add any custom options here
  }
}
```

## ⚙️ Configuration

Persistence comes with the following defaults:

```lua
{
  dir = vim.fn.stdpath("state") .. "/sessions/", -- directory where session files are saved
  -- minimum number of file buffers that need to be open to save
  -- Set to 0 to always save
  need = 1,
  branch = true, -- use git branch to save session
  auto_load = true -- enable autoloading sessions when enter
}
```

> [!TIP]
> To configure what should be saved in your session, check [:h 'sessionoptions'](https://neovim.io/doc/user/options.html#'sessionoptions')

## 🚀 Usage

**Persistence** works well with plugins like `startify` or `dashboard`.

```lua
-- load the session for the current directory
vim.keymap.set("n", "<leader>qs", function() require("persistence").load() end)

-- select a session to load
vim.keymap.set("n", "<leader>qS", function() require("persistence").select() end)

-- load the last session
vim.keymap.set("n", "<leader>ql", function() require("persistence").load({ last = true }) end)

-- stop Persistence => session won't be saved on exit
vim.keymap.set("n", "<leader>qd", function() require("persistence").stop() end)
```

## 📅 Events

- **PersistenceLoadPre**: before loading a session
- **PersistenceLoadPost**: after loading a session
- **PersistenceSavePre**: before saving a session
- **PersistenceSavePost**: after saving a session
