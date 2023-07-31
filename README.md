# zsh_site-functions

some things I found useful to automate mainly at work, i.e. how I wasted time, so that I can save some.

![image](https://user-images.githubusercontent.com/36888576/236028664-38ffd4b6-8a37-44c9-9b84-d12717a7503e.png)
[xkcd 1205](https://imgs.xkcd.com/comics/is_it_worth_the_time.png)

## Usage

- let's call the desired installation directory `$ZSH_UTILS`
  - e.g. `export ZSH_UTILS = '~/src/utils/zsh/functions'`
- let's call the function name we want to install `$ZSH_UTIL_NAME`
  - e.g. `export ZSH_UTIL_NAME = 'zk_clean'`

```shell
git clone https://github.com/jurajpiar/zsh_site-functions $ZSH_UTILS
```

add `$ZSH_UTILS/functions` to `fpath` and autoload all functions into your `.zshrc` file with:

```shell
sed -i -e "1s;^;# Custom zsh functions\nfpath=(${ZSH_UTILS}/functions $fpath)\nautoload $ZSH_UTILS/functions/*\n\n;" .zshrc
```

to load a single utility in your current terminal without sourcing `.zshrc`

```shell
autoload -Uz $ZSH_UTIL_NAME
```

From here you should be able to call the utility with `$ZSH_UTIL_NAME` (well, or any other in the folder, given the rc file was sourced)

## Update

- to update it we have to first unload the function

```shell
cd $ZSH_UTILS
git pull
unset -f $ZSH_UTIL_NAME
autoload -Uz $ZSH_UTIL_NAME
```

## ZK_SHELL

### Requirements

- [`Homebrew`](https://brew.sh) package manager
- [`fd`](https://github.com/sharkdp/fd) faster alternative to `find` command (will be installed automatically using brew)

The script will find your zk sync installation and create a symbolic link to it.
Then it will set:

- `ZKSYNC_HOME`
- `PATH`
- `NODE_EXTRA_CA_CERTS`

environment variables and change to `$ZKSYNC_HOME`.
