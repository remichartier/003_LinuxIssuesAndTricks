# Linux redirect stdout/stderr to file

Source: https://www.geeksforgeeks.org/input-output-redirection-in-linux/?msclkid=de741aa1bd0e11ecaa4fefdede8c502a

- Use: 
```
command > log.txt 2>&1 
```

It will merge stdout/stderr to log.txt as well,

cf `tee` command as well to redirect to a file (source: https://linuxize.com/post/linux-tee-command/)

