## My small changes

I know there are many completion plugins like Youcompleteme, coc.nvim... but I still like the way clang_complete works even though it is a bit old.
In my opinion, completion menu is a bit long. This fork removes the information in it and displays it in preview (I prefer completeopt+=popup)

+ Notice: Only available in versions of Vim compiled with the ```+textprop``` feature enabled.

To check it, run the command:

``` bash
$ vim --version | grep textprop
```
Result: 

![Screenshot from 2025-01-09 00-14-13](https://github.com/user-attachments/assets/396222c4-55bc-4888-b658-55ad4fb8377a)

---

This plugin uses clang for accurately completing C and C++ code.

## Installation

You need Vim 7.3 or higher, compiled with python support and ideally, with
the conceal feature.

#### Not using any plugin management tools

Just put the files in ~/.vim/

```
git clone https://github.com/xavierd/clang_complete.git /tmp/clang_complete
cp -r /tmp/clang_complete/* ~/.vim
```

#### Using packs of Vim8

```
mkdir -p ~/.vim/pack/completion/start/
git clone https://github.com/xavierd/clang_complete.git ~/.vim/pack/completion/start/clang_complete
```

#### Using plugin managers, runtime path managers

Follow regular procedure outlined in corresponding documentation

#### Using [vimball][vimball] (not in nvim)

To build and install in one step, type: `$ make install`

To build and install in two steps, type:

```
$ make
$ vim clang_complete.vmb -c 'so %' -c 'q'
```

## Minimum Configuration

- Set the `clang_library_path` to the directory containing file named
  libclang.{dll,so,dylib} (for Windows, Unix variants and OS X respectively) or
  the file itself, example:

```vim
 " provide path directly to the library file
 let g:clang_library_path='/usr/lib/llvm-14/lib/libclang-14.so.1'
```

- Compiler options can be configured in a `.clang_complete` file in each project
  root.  Example of `.clang_complete` file:

```
-DDEBUG
-include ../config.h
-I../common
-I/usr/include/c++/4.5.3/
-I/usr/include/c++/4.5.3/x86_64-slackware-linux/
```

## Usage

The plugin provides list of matches, after that you pick completion from a
generic completion menu where <kbd>Ctrl+N</kbd>, <kbd>Ctrl+P</kbd> and alike
work and wrap around ends of list.

## License

See doc/clang_complete.txt for help and license.

## Troubleshooting

The first step is to check values of `'omnifunc'` and `'completefunc'` options
in a C++ buffer where completion doesn't work (the value should be
`ClangComplete`).  This can be done with the following command:
`:set omnifunc? completefunc?`

Output of `:messages` command after startup could also show something useful in
case there were problems with plugin initialization.

If everything is fine, next step might be to load only clang_complete plugin
and see if anything changes.

[vimball]: https://vimhelp.appspot.com/pi_vimball.txt.html
