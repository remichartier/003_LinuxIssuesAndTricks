# Frequent Terminal Commands Used

## Quick Find Terminal command :

`find . -type f -iname 201910*google*.pdf`

## Rename files :

```
rename 's/\-/\_/' *.jpg

sudo rename 's/IMG\-//' *.jpg

sudo rename 's/IMG\_//' *.jpg

sudo rename 's/VID\_//' *.mp4

sudo rename 's/2014/2015/' *.jpg
```

## Install .deb files

`sudo apt install -f`

## Grep options
```
-R or -r --> recursive
-i --> ignore case
-e --> use regex patterns for search
```

## tee

For redirecting in parallel stdout to a file
`<cmd> | tee log.txt`

