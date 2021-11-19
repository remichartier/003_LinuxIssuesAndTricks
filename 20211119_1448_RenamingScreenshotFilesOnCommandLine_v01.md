# Kind of files to rename : 'Screenshot from 2021-11-19 13-27-48.png'

1. Install necessary command line tool `rename` --> `sudo apt install rename`

2. Use and adapt following command :

```
rename 's/^\Screenshot.from.(\d{4}).(\d{2}).(\d{2}).(\d{2}).(\d{2}).(\d{2})/$1$2$3_$4$5_$6_FileNameThatYouWantToGive/' *.png
```