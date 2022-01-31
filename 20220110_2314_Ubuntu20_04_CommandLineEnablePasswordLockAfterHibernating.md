# Ubuntu20_04 : Command Line Enable Password Lock After Hibernating

Solution found in https://askubuntu.com/questions/148690/how-do-i-lock-the-screen-after-resuming-from-hibernation

- added an alias into ~/.bashrc file

```
alias hibern='echo "Hibernating..."; gnome-screensaver-command -l; sudo hibernate;'
```
So that it locks the screen before hibernating.
