# Acer Aspire 17F (F5-771G) UEFI Supervisor Password Not Recognized

## Problem

- While trying to install Debian on a Windows PC via a USB stick, I could not boot via the USB stick due to Secure Boot issue.

- The solution to disable Secure Boot was to enter into the UEFI (F2 at boot), set the Supervisor Password, and then disable Secure Boot.

- However, I entered a password with numbers and non alphabetical symbols, which later where not recognized while re-entering passwords, while changing system languages back and forth between English and French but always keeping config set in French keyboard.

- Therefore, impossible to enter the UEFI Supervisor password to open UEFI later on.

## Solution

- Solution found in https://www.biosbug.com/acer/.

- Solution is : 

  - Enter password 3 times until menu shows 2 options : Unlock Password or Turn Off laptop.

  - Select `Unlock Password`

  - A code of several digits is provided.

  - Enter this code into one of the entry field of page https://www.biosbug.com/acer/.

  - The page will generate back a password, to enter in order to unlock and enter the PC UEFI, which constitute the new Supervisor password.

## Final step to reset UEFI Supervisor password : 

- Go to Security page, and enter the code generated at the last step (cf last step of `Solution` paragraph).

- Then you are free to enter a new Supervisor password, or to set it blank (ie disable Supervisor password).
