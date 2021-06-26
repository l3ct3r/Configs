![NANO](https://user-images.githubusercontent.com/48232101/122084247-62194d00-ce21-11eb-816e-24b3fc160eb2.gif)

## 🔗 Useful Links 
* [Nano Syntax Highlighting](https://github.com/scopatz/nanorc)
* [Nano Configuration](https://www.nano-editor.org/dist/latest/nanorc.5.html)
* [Nano QnA](https://askubuntu.com/questions/73444/how-to-show-line-numbering-in-nano-when-opening-a-file)
* [nanorc](https://www.nano-editor.org/dist/latest/nanorc.5.html)

## ❔ How To
- GNU nano is a text editor for Unix-like computing systems or operating environments using a command line interface.

```
********** Installation **********
$~ sudo apt install nano (APT based distributions) 
$~ sudo yum install nano (RPM based distributions) 
$~ sudo pacman -S nano (Pacman based distributions) 

********** Syntax Highlighting **********

Nano ships with syntax highlighting rules for most popular file types. On most Linux systems, the syntax files are stored in the /usr/share/nano directory and included by default in the /etc/nanorc configuration file.
/etc/nanorc
include "/usr/share/nano/*.nanorc"

OR 
"/.nano/*.nanorc"

Copy or wget the files as per your requirements

********** Set Nano as the Default Text Editor **********
By default on most Linux systems, the default text editor for commands such as visudo and crontab is set to vi. To use nano as the default text editor, you need to change the VISUAL and EDITOR environment variables .

Bash users can export the variables in the ~/.bashrc file:

~/.bashrc
export VISUAL=nano
export EDITOR="$VISUAL"
```

> Nano ships with almost every GNU/Linux distributions 
