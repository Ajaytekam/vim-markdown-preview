Vim Markdown Preview
====================

> Modification : Method Vim_Markdown_Preview_Local() is removed and methods Vim_Markdown_Preview_With_Image(), Vim_Markdown_Delete() added with some other changes.  

 

- [Intro](#intro)
- [Installation](#installation)
- [Usage](#usage)
- [Requirements](#requirements)
    - [Mac OS X](#mac-os-x)
    - [Unix](#unix)
- [Options](#options)
    - [Hotkey](#hotkey)
    - [Browser](#browser)
    - [Github Flavoured Markdown](#github)
    - [Markdown.pl](#perl)
    - [Pandoc](#pandoc)
    - [Use xdg-open](#xdg)
- [Behind the Scenes](#behind-the-scenes)

Intro
-----
A small Vim plugin for previewing markdown files in a browser.

The aim of this plugin is to be light weight with minimal dependencies. Thus, there is *no* polling engine or webserver involved.

![Screenshot](http://i.imgur.com/1hvnXwA.gif?raw=true "Preview on buffer write using Unix")

Installation
------------

* With [Pathogen](https://github.com/tpope/vim-pathogen): Place `vim-markdown-preview/` in `.vim/bundle/`.
* With [Vundle](https://github.com/VundleVim/Vundle.vim):
    * Add `Plugin 'JamshedVesuna/vim-markdown-preview'` to your `.vimrc`.
    * Launch `vim` and run `:PluginInstall`

See more [Options](#options).

Usage
-----

**Preview/Reload Markdown (text only) `Ctrl-p` :** 

By default, when in a `.markdown` or `.md` file, and  `Ctrl-p` is pressed, this plugin will either open a preview in your browser, or refresh your current preview (can be remapped, see [Options](#options)). Your cursor will remain in Vim.

**Preview/Reload Markdown with Image `Ctrl-i` :**  
 
Preview/Load the markdown file with image (only works with `png` format, you can change it according to your need). It basically copies all the images (with png format) into `/tmp/` directory and then call the `Vim_Markdown_Preview()` method. Your cursor will remain in Vim.  

**Other Change :**  

When you exit from vim then it automatically delete `vim-markdown-preview.html` file from `/tmp` if you use `Ctrl-p` at-least once, and also deletes all the copied `png` files from `/tmp` if you use `Ctrl-i` at-least once by calling `Vim_Markdown_Delete()` method.  


Requirements
------------

### Mac OS X:

* [Markdown](http://daringfireball.net/projects/markdown/) or [grip](https://github.com/joeyespo/grip) (for [GitHub flavoured markdown](#github))
    * If using Markdown, put `let vim_markdown_preview_github=0` in your `.vimrc` file
* [Safari](https://www.apple.com/safari/)

### Unix:

* [Markdown](http://daringfireball.net/projects/markdown/) or [grip](https://github.com/joeyespo/grip) (for [GitHub flavoured markdown](#github))
    * If using Markdown, put `let vim_markdown_preview_github=0` in your `.vimrc` file
* [xdotool](https://github.com/jordansissel/xdotool)
* [Google Chrome](https://www.google.com/chrome/browser/) or [other browser](https://github.com/JamshedVesuna/vim-markdown-preview/wiki/Use-other-browser-to-preview-markdown#ubuntu-or-debian)
* For example to install dependencies in Linux : `sudo apt install xdotool grip markdown -y`   

It is recommended to use grip when rendering Unicode characters.

Options
-------
All options have default values and work out of the box. If you prefer to change these, just add the following lines to your [.vimrc](http://vim.wikia.com/wiki/Open_vimrc_file) file.
Note that after changing an option, you have to restart Vim for the change to take effect.

<a name='hotkey'></a>
### The `vim_markdown_preview_hotkey` option

By default, this plugin maps `<C-p>` (Control p) to activate the preview. To remap Control p to a different hotkey, change the binding. Don't forget to add the single quotation marks.

Default: `'<C-p>'`

Example: Mapping Control M.
```vim
let vim_markdown_preview_hotkey='<C-m>'
```

<a name='browser'></a>
### The `vim_markdown_preview_browser` option

By default, if you are using Unix, [Google Chrome](https://www.google.com/chrome/) is the default browser. If you are on Mac OS X, [Safari](https://www.apple.com/safari/) is the default.
Note that bug [#16](https://github.com/JamshedVesuna/vim-markdown-preview/issues/16) does not allow cross operating system and browser support. See the [wiki page](https://github.com/JamshedVesuna/vim-markdown-preview/wiki/Use-other-browser-to-preview-markdown) for more help.

Default: `'Google Chrome'`

Example: Using Google Chrome.
```vim
let vim_markdown_preview_browser='Google Chrome'
```

<a name='github'></a>
### The `vim_markdown_preview_github` option

If you prefer [GitHub flavoured markdown](https://help.github.com/articles/github-flavored-markdown/) you need to install [Python grip](https://github.com/joeyespo/grip). Note that this makes a request to [GitHub's API](https://developer.github.com/v3/markdown/) (causing latencies) and may require [authentication](https://github.com/joeyespo/grip#access). This option also requires a network connection.

Default: `1`

Example: Use Markdown.
```vim
let vim_markdown_preview_github=0
```

<a name='perl'></a>
### The `vim_markdown_preview_perl` option
If you prefer to use John Gruber's [Markdown.pl](https://daringfireball.net/projects/markdown/) to render HTML, set the following flag:

Default: `0`

Example: Use Markdown.pl to render HTML.
```vim
let vim_markdown_preview_perl=1
```

<a name='pandoc'></a>
### The `vim_markdown_preview_pandoc` option
If you prefer to use John MacFarlane's [Pandoc](http://pandoc.org/) to render HTML, set the following flag:

Default: `0`

Example: Use Pandoc to render HTML.
```vim
let vim_markdown_preview_pandoc=1
```

<a name='xdg'></a>
### The `vim_markdown_preview_use_xdg_open` option

If your system does not come with `see`, and you would like to use `xdg-open` to view your rendered html in the browser, set the following flag:

Default: `0`

Example: Use `xdg-open`.
```vim
let vim_markdown_preview_use_xdg_open=1
```

Behind The Scenes
-----------------

1. First, this plugin renders your markdown as html and creates a temporary html file.
2. Next, this plugin either opens the html file or refreshes the Google Chrome or Safari tab.
    * If you are using GitHub flavoured markdown, `grip` will make a call to the GitHub API and retrieve the html.
3. If you press `Ctrl-i` then it copies all the `*.png` files from current directory into `/tmp/` directory, then render it. 
4. In exit from vim it deletes `html` and `png` files from `/tmp` directory.   

