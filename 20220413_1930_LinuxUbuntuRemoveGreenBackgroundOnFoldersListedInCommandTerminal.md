# Linux / Ubuntu : Remove Green Background On Folders Listed In Command Terminal.md

Source: https://stackoverflow.com/questions/40574819/how-to-remove-dir-background-in-ls-color-output#:~:text=To%20remove%20green%20background%20for%20o%2Bw%20%28%27writable%20by,line%20type%20the%20following%3A%20dircolors%20-p%20%3E%20~%2F.dircolors?msclkid=09fba5f1bb4c11eca0f210c60df79e35

In short:
```
dircolors -p | sed 's/;42/;01/' > ~/.dircolors
source ~/.bashrc
```
