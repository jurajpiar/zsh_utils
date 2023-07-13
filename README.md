# zsh_site-functions

some things I found useful to automate mainly at work, i.e. how I wasted time, so that I can save some.

![image](https://user-images.githubusercontent.com/36888576/236028664-38ffd4b6-8a37-44c9-9b84-d12717a7503e.png)
[xkcd 1205](https://imgs.xkcd.com/comics/is_it_worth_the_time.png)

## Usage

- let's call the install dir `$ZSH_UTILS`
  - e.g. `export ZSH_UTILS = '~/src/utils/zsh/functions'`
- and the zsh functions dir (could be the same one as `$ZSH_UTILS`) let's call $ZSH_FNS
  - e.g. `export ZSH_FNS = '~/.local/share/zsh/site-functions'` on macos
- let's call the function name we want to install `$ZSH_UTIL_NAME`
  - e.g. `export $ZSH_UTIL_NAME = 'zk_clean'`

```shell
#!/bin/bash

git clone https://github.com/jurajpiar/zsh_site-functions $ZSH_UTILS
ls -s $ZSH_UTILS/$ZSH_UTIL_NAME $ZSH_FNS/$ZSH_UTIL_NAME
autoload -Uz $ZSH_UTIL_NAME
```

## Update

- to update it we have to first unload the function

```shell
#!/bin/bash

cd $ZSH_UTILS
git pull
unset -f $ZSH_UTIL_NAME
autoload -Uz $ZSH_UTIL_NAME
```
