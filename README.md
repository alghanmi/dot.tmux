##tmux Configuration
[tmux](https://tmux.github.io/) is a terminal multiplexer. This repository contains my personal configuration of tmux.

###`$TERM` Setup
For consistant results. The terminal ID from your terminal application along with `$TERM` environment variable and terminal settings in `.tmux.conf` should match to properly support 256 colors.

1. The terminal application such as gnome-terminal or iTerm2 should identify itself as `screen-256color`

1. In your `.bashrc` (or `.bash_profile` if you are on Mac):
```bash
#Set terminal to screen-256color in TMUX
if [ -n "$TMUX" ]; then
	export TERM=screen-256color
fi

#Force TMUX to start in 256 support-mode
alias tmux='tmux -2'
```

1. `.tmux.conf` should properly set the terminal to
```bash
set -g default-terminal 'screen-256color'
```

1. If you are using vim within tmux, you should also set the terminal colors:
```
set t_Co=256                        " force vim to use 256 colors
let g:solarized_termcolors=256      " use solarized 256 fallback
```

##Mac Installation Notes
In order for this work properly on mac, you would need to install [reattach-to-user-namespace](https://github.com/ChrisJohnsen/tmux-MacOSX-pasteboard/)

```bash
brew install reattach-to-user-namespace
```

Also, `tmux` only runs `.bashrc` and not `.bash_profile` when starting. Therefore, I advise to have all your setup in `~/.bashrc` and have the following code as your `~/.bash_profile`:
```bash
if [ -f ~/.bashrc ]; then
	. ~/.bashrc
fi
```

####Notes
  + [Forcing TERM is bad](http://blog.sanctum.geek.nz/term-strings/)

###Plugins
This tmux configuration takes advantage of the very useful [tmux plugins]. I strongly encourage you to visit this project and pick the plugins that suite you the most and install them.

###Powerline
This setup also takes advantage of [Powerline](http://powerline.readthedocs.org/en/master/index.html) which you can install to privde you with nice details and information in your terminal.

###Installation and Setup
In your terminal, clone and setup tmux configuration

```bash
git clone git@github.com:alghanmi/dot.tmux.git ~/.tmux
ln -s ~/.tmux/tmux.conf  ~/.tmux.conf
```

Next, launch tmux
```bash
tmux
```

Finally, install all the plugins, but running the following key combinations: `<Ctrl>-A` + `I`
