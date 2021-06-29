![ZSH](https://user-images.githubusercontent.com/48232101/122083324-7e68ba00-ce20-11eb-9de8-4b1e56469785.gif)

## 🔗 Useful Links 
* [Oh My ZSH](https://ohmyz.sh/)
* [Oh My ZSH Plugins](https://github.com/ohmyzsh/ohmyzsh/wiki/Plugins)
* [Awesome ZSH Plugins](https://learnpracticeandshare.com/awesome-zsh-plugins-massive-collection-of-resources/)
* [ZSH Themes](https://zshthem.es/all/)
* [Powerlevel 10k](https://github.com/romkatv/powerlevel10k)

## ❓ How To
- Install ZSH 
```
*************** APT Based Distros ***************
$~ sudo apt install zsh 

*************** RPM Based Distros ***************
$~ sudo yum install zsh 
$~ sudo dnf install zsh 

*************** Arch Based Distros ***************
$~ sudo pacman -S zsh 
```

- Using ZSH Shell (Optional)
```
I'm using XFCE4-Terminal
Go to Terminal's Prefrence -> General -> Check on Run a Custom Command Instead of my Shell -> /bin/zsh
```

- Installing Oh-My-ZSH
```
$~ sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
Cloning Oh My Zsh...
Cloning into '/home/encrypt3db0t/.oh-my-zsh'...
remote: Enumerating objects: 1239, done.
remote: Counting objects: 100% (1239/1239), done.
remote: Compressing objects: 100% (1204/1204), done.
remote: Total 1239 (delta 20), reused 1103 (delta 15), pack-reused 0
Receiving objects: 100% (1239/1239), 863.71 KiB | 675.00 KiB/s, done.
Resolving deltas: 100% (20/20), done.

Looking for an existing zsh config...
Using the Oh My Zsh template file and adding it to ~/.zshrc.

Time to change your default shell to zsh:
Do you want to change your default shell to zsh? [Y/n] y
Changing the shell...
Password: 
Shell successfully changed to '/usr/bin/zsh'.

         __                                     __
  ____  / /_     ____ ___  __  __   ____  _____/ /_
 / __ \/ __ \   / __ `__ \/ / / /  /_  / / ___/ __ \
/ /_/ / / / /  / / / / / / /_/ /    / /_(__  ) / / /
\____/_/ /_/  /_/ /_/ /_/\__, /    /___/____/_/ /_/
                        /____/                       ....is now installed!


Before you scream Oh My Zsh! please look over the ~/.zshrc file to select plugins, themes, and options.

• Follow us on Twitter: https://twitter.com/ohmyzsh
• Join our Discord server: https://discord.gg/ohmyzsh
• Get stickers, shirts, coffee mugs and other swag: https://shop.planetargon.com/collections/oh-my-zsh

```

- Installing and Using Powerlevel10k Theme
```
********** Installation **********
~ git clone --depth=1 https://gitee.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k

********** Using Powerlevel10k Theme **********
$~ vim .zshrc 

# Set name of the theme to load --- if set to "random", it will
# load a random theme each time oh-my-zsh is loaded, in which case,
# to know which specific one was loaded, run: echo $RANDOM_THEME
# See https://github.com/ohmyzsh/ohmyzsh/wiki/Themes
ZSH_THEME="powerlevel10k/powerlevel10k"

********** Configuring Powerlevel10k Theme **********
- Exit out of the current terminal session 
- Open new Terminal 
$~ p10k configure 

This is Powerlevel10k configuration wizard. It will ask you a few questions and
                                 configure your prompt.

                    Does this look like a diamond (rotated square)?
                      reference: https://graphemica.com/%E2%97%86

                                     --->  <>  <---

(y)  Yes.

(n)  No.

(q)  Quit and do nothing.

Choice [ynq]: 

Continue as you want
```

- Shell after ZSH 

![DE](https://user-images.githubusercontent.com/48232101/123642695-4f504080-d843-11eb-8f81-3527ad4bfc25.png)

- Configuring and Using Plugins in ZSH 
```
1. Auto Color ls
$~ git clone https://github.com/gretzky/auto-color-ls ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/auto-color-ls
- Enable this plugin by adding auto-color-ls in your zshrc file

2. ZSH-Autocomplete 
$~ git clone https://github.com/marlonrichert/zsh-autocomplete ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autocomplete
- Enable this plugin by adding zsh-autocomplete to plugins array in your zshrc file 

3. Colorls
$~ git clone https://github.com/Kallahan23/zsh-colorls ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-colorls
- Enable this plugin by adding zsh-colorls to the plugins array in your zshrc file:

* NOTE: Make sure it is listed after any plugin which sets aliases for the ls command, such as the common-aliases plugin.
plugins=(... zsh-colorls)

4. Colorize
$~ git clone https://github.com/zpm-zsh/colorize ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/colorize
- Enable this plugin by adding colorize in your zshrc file

5. Colored Man Pages 
$~ git clone https://github.com/ael-code/zsh-colored-man-pages.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-colored-man-pages
- Enable this plugin by adding zsh-colored-man-pages in your zshrc file

6. Syntax Highlighting 
$~ cd ~/.oh-my-zsh/custom/plugins
$~ git clone https://github.com/zsh-users/zsh-syntax-highlighting.git
$~ echo "source ${(q-)PWD}/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" >> ${ZDOTDIR:-$HOME}/.zshrc
$~ source ~/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
- Enable this plugin by adding zsh-syntax-highlighting in your zshrc files 
```
