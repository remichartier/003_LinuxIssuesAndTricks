# Linux: Modify Terminal Prompts on Ubuntu Or Git-bash (Windows10)

## Ubuntu

* Generally, in $HOME/.bashrc, search for PS1 variable
* Then add \d \t in the PS1 variable content, for instance `S1='\d \t : .....`

## Git-bash (Windows10)

Source: https://stackoverflow.com/questions/54887987/how-to-shorten-git-bash-prompt-windows

* First make a copy of the default git-prompt.sh file and put it in your own personal config location. In my case the command is:

```cp /c/Program\ Files/Git/etc/profile.d/git-prompt.sh ~/.config/git/```

* Do not skip this step! Now make sure to update your copy of the file by removing everything except what's inside of the larger else clause where PS1 is set. (At the time of this writing I'm keeping only lines 12-36.) Note, if you skip this step Git Bash will get stuck in an infinite loop and exit.

* Now you can edit your copy of the file however you please.

* For instance, add `\d\t` in PS1 variable, like this for example:

```PS1="$PS1"'\d\t \u@\h '             # user@host<space>```

