# Neovim/Vim Dotfiles

## 概要
このリポジトリは、Lazy.nvim ベースの Neovim 設定と従来の Vim 設定をひとまとめにした dotfiles 集です。`setup-*.sh` スクリプトでホームディレクトリにシンボリックリンクを張り、Node.js・Neovim・Nerd Fonts など主要ツールのインストールも自動化しています。Neovim の設定は `neovim/` ディレクトリに閉じ込め、Lua モジュール単位で役割を分離しています。

- `neovim/` … Lazy.nvim を使ったモジュール構成の最新設定。
- `vim/` … `~/.vimrc` と関連ファイルをまとめたレガシー Vim 向け構成。
- `setup-neovim.sh` / `setup-vim.sh` … 各エディタ向けのセットアップスクリプト。
- `stylua.toml` … Neovim Lua コードの整形ルール。

### ルート
| パス | 内容 / 目的 |
| --- | --- |
| `neovim/` | Neovide 透過設定や Lazy.nvim ブートストラップを含む最新 Neovim 設定一式。 |
| `vim/` | `.vimrc`、`coc-settings.json` など従来 Vim 用の設定群。 |
| `setup-neovim.sh` | Neovim ディレクトリを `~/.config/nvim` にリンクし、mise / Node.js / Neovim / Nerd Fonts を導入するスクリプト。 |
| `setup-vim.sh` | `.vimrc` のリンクと vim-plug、copilot.vim、terraform-lsp などの依存をまとめてインストールするスクリプト。 |
| `stylua.toml` | `lua` 配下で利用する StyLua の整形ルール。 |

### `neovim/`
| パス | 内容 / 目的 |
| --- | --- |
| `neovim/init.lua` | Neovide 用の透過設定を適用し、`config.options` / `config.lazy` / `config.autocmds` を読み込むエントリーポイント。 |
| `neovim/lazy-lock.json` | Lazy.nvim が解決した各プラグインのコミットを固定するロックファイル (常に最新版をコミット)。 |
| `neovim/AGENTS.md` | コントリビュータ向けの作業ガイドと動作確認コマンド。 |

### `neovim/lua/config`
| パス | 内容 / 目的 |
| --- | --- |
| `options.lua` | 行番号・インデント幅・wrap など Neovim の基本オプションを一括設定。 |
| `lazy.lua` | lazy.nvim のクローン、runtimepath 登録、リーダーキー設定、`lua/plugins` 読み込みと更新チェッカー設定を担当。 |
| `autocmds.lua` | Web 系ファイルタイプに 2 スペースインデントを適用する自動コマンドなどを定義。 |

### `neovim/lua/plugins`
| パス | 内容 / 目的 |
| --- | --- |
| `autopairs.lua` | `windwp/nvim-autopairs` を InsertEnter で読み込み、自動括弧補完を有効化。 |
| `bufferline.lua` | `akinsho/bufferline.nvim` でタブラインを整備し、truecolor を強制。 |
| `cmp.lua` | `nvim-cmp` の補完 UI、Luasnip 連携、cmdline 補完、`ts_ls` の LSP capability 拡張を設定。 |
| `comment.lua` | `Comment.nvim` を既定設定で起動し、トグルコメント機能を提供。 |
| `copilot.lua` | `github/copilot.vim` を常時読み込み、AI 補完を利用可能にする。 |
| `dashboard.lua` | 起動時に `dashboard-nvim` を表示するための最小セットアップ。 |
| `flash.lua` | `folke/flash.nvim` を VeryLazy で読み込み、`s` / `S` などのジャンプ系キーマップを割り当て。 |
| `gitsigns.lua` | `lewis6991/gitsigns.nvim` の既定設定で Git ハイライトと操作を提供。 |
| `indent-blankline.lua` | `ibl` (indent-blankline) を呼び出し、インデントガイドの描画を制御。 |
| `lspconfig.lua` | `nvim-lspconfig` の診断表示、インレイヒント、`basedpyright` 設定をまとめて適用。 |
| `lualine.lua` | `lualine.nvim` をモノカイテーマで常時表示し、依存するアイコンプラグインも読み込む。 |
| `markdown-preview.lua` | `iamcco/markdown-preview.nvim` のビルド手順と `<leader>cp` キーマップを定義。 |
| `mason-lspconfig.lua` | Mason と連携し、`gopls` や `ts_ls` など主要 LSP を自動インストール対象に登録。 |
| `monokai.lua` | `monokai-pro.nvim` を起動時に読み込み、カラースキームを設定。 |
| `oil.lua` | `oil.nvim` を初期化し、`<C-n>` でバッファ内ファイルマネージャを開けるようにする。 |
| `telescope.lua` | `telescope.nvim` の主要ピッカーを `<leader>f?` 系ショートカットへ割り当て。 |
| `treesitter.lua` | `nvim-treesitter` のインストール言語一覧やハイライト/インデント機能を構成。 |
| `ts-autotag.lua` | `nvim-ts-autotag` で HTML/JSX のタグ自動閉鎖・リネームを有効にする。 |

---
この README はリポジトリ全体の速習メモとしてまとめています。設定を変更する際は該当 Lua ファイルと Lazy.nvim のドキュメントを照らし合わせながら編集してください。
