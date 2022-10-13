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

## List of folder sizes

Source: https://superuser.com/questions/869969/is-there-a-terminal-command-to-list-folder-size-and-corresponding-file-sizes-wit

'''du -chd 1 | sort -h'''

It outputs the total size of each sub-directory from the current directory location (the "1" above), as well as a total of all sub-directories, and sorts it by human-readable sizes

'''du -m | sort -nr | head -10'''

It lists all folders (including repetitive sub-folders) with most disk space usage sorted.

here is the tree command. Install it via sudo apt-get install tree, and type the following:

'''tree -h'''

## Get list of packages installed on Ubuntu

Source: https://www.cyberciti.biz/faq/apt-get-list-packages-are-installed-on-ubuntu-linux/

```apt list --installed```

Get if a specific package is installed:

```apt list apache2```
