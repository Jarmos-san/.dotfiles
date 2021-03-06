# Neovim Configurations

[Neovim][Neovim] is a fork of the original [Vim][Vim]. If you are on an Unix-like system, chances are, it already comes pre-packaged with it.

But it's a different case with Windows users. While a GUI variant of Vim called GVim is available for Windows users, it's not as user-friendly as it is on Unix-like systems. And besides, Vim on Windows is way too buggy to be useful. Coupled with a buggy interface & unecessary configuration, it can be a bit of a struggle as well.

On a brighter note though, Neovim comes in as a viable alternative for Windows users. It's not as buggy as it's vanilla counterpart & comes pre-packaged with certain sensible default configuration settings as well. So, if you prefer  reading up more about it, the official documentations at [neovim.io](https://neovim.io) is a great place to start with.

But if you're already aware of Neovim & it's capabilities, and perhaps you're looking for some inspiration to configure your Neovim environment, this repo might benefit you in some ways.

But before you start with that, do note, Neovim can be configured with Lua right now. And since Neovim 0.5 which comes with an in-built Language Server Provider (LSP). The only caveat though, configuring LSP requires a bit of Lua scripting. With that in mind, you might notice I'm in the middle of migrating most of my Vim configurations from VimScript to LuaScript. Instead if you want to figure out how I had Neovim configured with VimScript, head over to [Jarmos-san/myvimconfig](https://github.com/Jarmos-san/myvimconfig). It's a backup of my older `init.vim` kept only for future reference.

## How to Configure Neovim with Lua

The best eye-catching feature of Neovim is it's embedded Lua scripting environment. You can call Lua code within VimScript with the `lua` keyword or write Lua code directly to configure Neovim. If you need more info on how to migrate from using VimScript to Lua, do check out `:h lua.txt` as a great starting point.

But briefly put, the `runtimepath` previously used within Neo(vim) hasn't changed. So, if you had scripts in there previously, they'll still work. Also, similar to `init.vim` you should leave an `init.lua` at it's usual place as well. So, for Windows users, you should leave the `init.lua` file at `%LOCALAPPDATA%\nvim`.

Additionally, while it's not a necessity, all Lua scripts should be placed inside a folder aptly named `lua`. These scripts are considered Lua modules & all scripts here is automatically "sourced". So, assuming there's a `settings.lua` script under the `lua` directory, you can call this script inside `init.lua` with the `require('settings')` syntax. For more information, refer to the `:h lua.txt` documentation.

That said, I've setup my Lua directory as follows:

```powershell
%LOCALAPPDATA%/
├─ nvim/
│  ├─ after/
│  ├─ lua/                      # Contains all Lua modules for configuring Neovim with
│  │  ├─ keymaps.lua            # Module for configuring Vim keymaps
│  │  ├─ lsp_config.lua         # Module for configuring the native in-built LSP
│  │  ├─ plugins.lua            # Module for "installing" & configuring plugins for Neovim
│  │  ├─ settings.lua           # Module for configuring all Neovim options
│  │  ├─ statusline.lua         # Module for install & configuring the Statusline
│  ├─ init.lua                  # Notice the .lua extension instead of the usual .vim extensions
```

As you can see, configuring Neovim with Lua is pretty straightforward. It's almost like developing a product with an arbitrary programming language. Now you longer have to maintain a huge `.vimrc` file with 100s of lines of code.

As usual, refer to `h: lua.txt` for more info on configuring Neovim with Lua instead of VimScript.

## My Neovim Configurations Explained

As mentioned earlier, I configure Neovim with Lua instead of VimScript. It's much more flexible, is easily extensible & is easier to maintain. That said, I keep all user-defined customizations is Lua modules inside the `lua` directory. And import these modules using `require` statements in the `init.lua` file.

Also, do note, the `init.lua` should be placed under `%LOCALAPPDATA%\nvim` & not under `lua\` like the other modules. Besides that, the order of importing the modules should also be taken care of. So, in my case, the `init.lua` file contains the following lines of code:

```lua
require('settings')
require('plugins')
require('lsp_config')
require('statusline')
```

**NOTE**: Notice the lack of `.lua` extensions. Neovim knows to look inside the `lua` directory when importing the modules mentioned in the `init.lua`. So, when loading my `init.lua`, Neovim will first import the `settings.lua` followed by the `plugins.lua` & so on.

## Plugins Used

I try to keep my `init.lua` file as minimal as possible, hence my list of plugins are quite limited as well. Some of the plugins are an absolute necessity for me & are one which I can't live without.

That said, following are the list of plugins I currently use with my Neovim setup:

- [npxbr/gruvbox.nvim](https://github.com/npxbr/gruvbox.nvim) for a retro colorscheme which is quite warm & nicer on the eyes.
- [neovim/nvim-lspconfig](https://github.com/neovim/nvim-lspconfig) for configuring the built-in LSP in Neovim.
- [ojroques/hardline](https://github.com/ojroques/hardline) for a nice & sleek statusline which also supports the Gruvbox colorscheme out-of-the-box. This plugin is subject to removal when I can write my own statusline later on.

More plugins like `telescope.nvim`, `nvim-treesitter` & such are yet to be configured later on.

## Keymapping Used

TODO: Configure & share the reasons for doing so

