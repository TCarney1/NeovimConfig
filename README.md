
Requirements: 
    sudo apt-get install ripgrep
    
Package manager:
    wbthomason/packer.nvim (https://github.com/wbthomason/packer.nvim)
    :PackerSync

Telescope:
    nvim-telescope/telescope.nvim (https://github.com/nvim-telescope/telescope.nvim)


Remaps:
    leader key = " "

    <leader>fe => go to file explorer
    <leader>ff => find file 
    <leader>fg => find file git
    <leader>fw => find word usage

    Harpoon:
        <leader>a => add file to harpoon list
        ctrl + e => show harpoon list // can use normal vim motions to edit harpoon list
        ctrl + j => go to file 1
        ctrl + k => go to file 2
        ctrl + l => go to file 3
        ctrl + ; => go to file 4

    Undotree:
        ctrl + u => toggle undo tree
require'nvim-treesitter.configs'.setup {
  -- A list of parser names, or "all" (the five listed parsers should always be installed)
  ensure_installed = { "c", "lua", "vim", "vimdoc", "query" },

  -- Install parsers synchronously (only applied to `ensure_installed`)
  sync_install = false,

  -- Automatically install missing parsers when entering buffer
  -- Recommendation: set to false if you don't have `tree-sitter` CLI installed locally
  auto_install = true,

  -- List of parsers to ignore installing (for "all")
  ignore_install = { "javascript" },

  ---- If you need to change the installation directory of the parsers (see -> Advanced Setup)
  -- parser_install_dir = "/some/path/to/store/parsers", -- Remember to run vim.opt.runtimepath:append("/some/path/to/store/parsers")!

  highlight = {
    enable = true,

    -- NOTE: these are the names of the parsers and not the filetype. (for example if you want to
    -- disable highlighting for the `tex` filetype, you need to include `latex` in this list as this is
    -- the name of the parser)
    -- list of language that will be disabled
    disable = { "c", "rust" },
    -- Or use a function for more flexibility, e.g. to disable slow treesitter highlight for large files
    disable = function(lang, buf)
        local max_filesize = 100 * 1024 -- 100 KB
        local ok, stats = pcall(vim.loop.fs_stat, vim.api.nvim_buf_get_name(buf))
        if ok and stats and stats.size > max_filesize then
            return true
        end
    end,

    -- Setting this to true will run `:h syntax` and tree-sitter at the same time.
    -- Set this to `true` if you depend on 'syntax' being enabled (like for indentation).
    -- Using this option may slow down your editor, and you may see some duplicate highlights.
    -- Instead of true it can also be a list of languages
    additional_vim_regex_highlighting = false,
  },
}
