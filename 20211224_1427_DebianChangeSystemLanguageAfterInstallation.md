# Debian : Change System Language After Installation

# Problem

- I installed Debian French language for some keyboard and Bios/UEFI Characters reasons.

- However, long term, I wanted to swith Debian system language to English as I am using this laptop in US.

- But looking at Settings/Country and Language settings, I can only see French for languages and list of languages does not contain any other languages.

# Solution 

- Solutions found in https://wiki.debian.org/ChangeLanguage.

- One of the straight forward and easiest solution is to use `dpkg-reconfigure locales`.

- However, with a basic Debian install, `dpkg-reconfigure` would return that the command is not found.

- In fact, it is already installed by default on Debian, however it can not find it because `/usr/bin` is not yet in the $PATH variable.

- Therefore, the steps to the solutions are the following : 

  - Add in file `.bashrc` : `export PATH=/usr/bin:$PATH`

  - In the Terminal/Command window : 
  
    - `source .bashrc`

    - `dpkg-reconfigure locales` will open a basic tool to reconfigure the system language in any other available languages.
