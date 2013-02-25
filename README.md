# Sheerun's vimrc.vim

I am Ruby developer and this plugin is supposed to replace my `.vimrc` file.

This is fork of [`vim-sensible`](https://github.com/tpope/vim-sensible), but not everyone agreed on these settings. They just reflect my (rather good) taste.

## Installation

You can use [vundle](https://github.com/gmarik/vundle) or [pathogen](https://github.com/tpope/vim-pathogen) for installation of this plugin.

You are supposed to **fork this repository** and source it at the top of `.vimrc`:

    runtime! plugin/vimrc.vim

You can see [my dotfiles](https://github.com/sheerun/dotfiles) for nice & clean method of managing vim configuration.

## Features overview

The same as in [`vim-sensible`](https://github.com/tpope/vim-sensible), but:

* Automatically create backup and undo directories.
* Support only for UNIX-like operating systems.
* Keep 8 lines above or below the cursor when scrolling.
* Keep 15 columns next to the cursor when scrolling horizontally.
* Hide buffers instead of asking if to save them.
* Don't wrap lines. But if so, do it at convenient points.
* For autocompletion, complete as much as you can.
* Show line numbers on the sidebar.
* Disable any annoying beeps on errors.
* Don't parse modelines (google "vim modeline vulnerability").
* Do not fold by default. But if, do it up to 3 levels.
* Enable mouse for scrolling and window resizing.
* Disable swap to prevent annoying messages.
* Save up to 100 marks, enable capital marks.
* Enable search highlighting.
* Ignore case when searching.
* Show mode in statusbar, not separately.
* Don't ignore case when search has capital letters
  (although also don't ignore case by default).
* Add gems.tags to files searched for tags.
* Disable output, vcs, archive, rails, temp and backup files.

## Detailed features

### Compatible with [`vim-sensible`](https://github.com/tpope/vim-sensible)

* Disable strange Vi defaults.

  ```vim
  set nocompatible
  ```

* Turn on filetype plugins (:help filetype-plugin).

  ```vim
  if has('autocmd')
    filetype plugin indent on
  endif
  ```

* Enable syntax highlighting.

  ```vim
  if has('syntax')
    syntax enable
  endif
  ```

* Autoindent when starting new line, or using `o` or `O`.

  ```vim
  set autoindent
  ```

* Allow backspace in insert mode.

  ```vim
  set backspace=indent,eol,start
  ```

* Don't scan included files. The .tags file is more performant.

  ```vim
  set complete-=i
  ```

* When inserting paren, jump briefly to matching one.

  ```vim
  set showmatch
  ```

* Use 'shiftwidth' when using `<Tab>` in front of a line.

  By default it's used only for shift commands (`<`, `>`).

  ```vim
  set smarttab
  ```

* Disable octal format for number processing.

  ```vim
  set nrformats-=octal
  ```

* Round autoindentation. No one needs 3 spaces when you indent by two.

  ```vim
  set shiftround
  ```

* Allow for mappings including `Esc`, while preserving

  zero timeout after pressing it manually.

  ```vim
  set ttimeout
  set ttimeoutlen=50
  ```

* Indent using two spaces.

  ```vim
  set tabstop=2
  set shiftwidth=2
  set expandtab
  ```

* Enable highlighted case-insensitive incremential search.

  ```vim
  set incsearch
  ```

* Use `Ctrl-L` to clear the highlighting of :set hlsearch.

  ```vim
  nnoremap <silent> <C-L> :nohlsearch<CR><C-L>
  ```

* Always show window statuses, even if there's only one.

  ```vim
  set laststatus=2
  ```

* Show the line and column number of the cursor position.

  ```vim
  set ruler
  ```

* Show the size of block one selected in visual mode.

  ```vim
  set showcmd
  ```

* Autocomplete commands using nice menu in place of window status.

  Enable `Ctrl-N` and `Ctrl-P` to scroll through matches.

  ```vim
  set wildmenu
  ```

* When 'wrap' is on, display last line even if it doesn't fit.

  ```vim
  set display+=lastline
  ```

* Show all whitespaces by default.

  ```vim
  set list
  set listchars=tab:>\ ,trail:-,extends:>,precedes:<,nbsp:+
  if &termencoding ==# 'utf-8' || &encoding ==# 'utf-8'
    let &listchars = "tab:\u21e5 ,trail:\u2423,extends:\u21c9,precedes:\u21c7,nbsp:\u26ad"
  endif
  ```

* Reload unchanged files automatically.

  ```vim
  set autoread
  ```

* Automatically save file as buffer goes away.

  ```vim
  set autowrite
  ```

* Support all kind of EOLs by default.

  ```vim
  set fileformats+=mac
  ```

* Increase history size to 1000 items.

  ```vim
  set history=1000
  ```

* Allow for up to 50 opened tabs on Vim start.

  ```vim
  set tabpagemax=50
  ```

* Always save upper case variables to viminfo file.

  ```vim
  set viminfo^=!
  ```

* Create and set directories for backup and undo files.

  ```vim
  let s:dir = match(system('uname'), "Darwin") > -1 ? '~/Library/Vim' : empty($XDG_DATA_HOME) ? '~/.local/share/vim' : '$XDG_DATA_HOME/vim'
  if !isdirectory(expand(s:dir))
    call system("mkdir -p " . expand(s:dir) . "/{backup,undo}")
  end
  ```

* Enable back and undo files by default.

  ```vim
  let &backupdir = expand(s:dir) . '/backup//'
  if exists('+undodir')
    let &undodir = expand(s:dir) . '/undo//'
    if exists('+undofile')
      set undofile
    endif
  endif
  ```

* Allow color schemes to do bright colors without forcing bold.

  ```vim
  if &t_Co == 8 && $TERM !~# '^linux'
    set t_Co=16
  endif
  ```

* Hide dotfiles, backup files and tag files by default.

  ```vim
  if !exists('g:netrw_list_hide')
    let g:netrw_list_hide = '^\.,\~$,^tags$'
  endif
  ```

* Load matchit.vim, but only if the user hasn't installed a newer version.

  ```vim
  if !exists('g:loaded_matchit') && findfile('plugin/matchit.vim', &rtp) ==# ''
    runtime! macros/matchit.vim
  endif
  ```

* `Ctrl-U` in insert mode deletes a lot. Use `Ctrl-G` u to first break undo,

  so that you can undo `Ctrl-U` without undoing what you typed before it.

  ```vim
  inoremap <C-U> <C-G>u<C-U>
  ```

* Keep flags when repeating last substitute command.

  ```vim
  nnoremap & :&&<CR>
  xnoremap & :&&<CR>
  ```

* Y yanks from the cursor to the end of line as expected. See :help Y.

  ```vim
  nnoremap Y y$
  ```

### Compatible with my taste ;) (you can change them in fork)

* Keep 8 lines above or below the cursor when scrolling.

  ```vim
  set scrolloff=8
  ```

* Keep 15 columns next to the cursor when scrolling horizontally.

  ```vim
  set sidescroll=1
  set sidescrolloff=15
  ```

* Hide buffers instead of asking if to save them.

  ```vim
  set hidden
  ```

* Don't wrap lines. But if so, do it at convenient points.

  ```vim
  set nowrap
  set linebreak
  ```

* For autocompletion, complete as much as you can.

  ```vim
  set wildmode=longest,full
  ```

* Show line numbers on the sidebar.

  ```vim
  set number
  ```

* Disable any annoying beeps on errors.

  ```vim
  set noerrorbells
  set visualbell
  ```

* Don't parse modelines (google "vim modeline vulnerability").

  ```vim
  set nomodeline
  ```

* Do not fold by default. But if, do it up to 3 levels.

  ```vim
  set foldmethod=indent
  set foldnestmax=3
  set nofoldenable
  ```

* Enable mouse for scrolling and window resizing.

  ```vim
  set mouse=nicr
  ```

* Disable swap to prevent annoying messages.

  ```vim
  set noswapfile
  ```

* Save up to 100 marks, enable capital marks.

  ```vim
  set viminfo='100,f1
  ```

* Enable search highlighting.

  ```vim
  set hlsearch
  ```

* Ignore case when searching.

  ```vim
  set ignorecase
  ```

* Show mode in statusbar, not separately.

  ```vim
  set noshowmode
  ```

* Don't ignore case when search has capital letters

  (although also don't ignore case by default).

  ```vim
  set smartcase
  ```

* Add gems.tags to files searched for tags.

  ```vim
  set tags+=gems.tags
  ```

* Disable output, vcs, archive, rails, temp and backup files.

  ```vim
  set wildignore+=*.o,*.out,*.obj,.git,*.rbc,*.rbo,*.class,.svn,*.gem
  set wildignore+=*.zip,*.tar.gz,*.tar.bz2,*.rar,*.tar.xz
  set wildignore+=*/vendor/gems/*,*/vendor/cache/*,*/.bundle/*,*/.sass-cache/*
  set wildignore+=*.swp,*~,._*
  ```

See the [source](https://github.com/sheerun/vim-sensible) for the authoritative list of features.

## License

The same terms as Vim itself. See `:help license`.
