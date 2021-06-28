
# os : archlinux
# terminal : xfce4-terminal
# font : HackNF Monospace Regular
# source : https://gist.github.com/3feec5b12fcf07c6b64e

### export {{{
PATH=$PATH:$HOME/.rvm/bin
HISTFILE=~/.zsh_history
HISTSIZE=20000
SAVEHIST=20000
fpath=(~/.zsh/functions/ $fpath)
fpath=($HOME/.zsh/functions $fpath)
e_normal=`echo -e "¥033[0;30m"`
e_RED=`echo -e "¥033[1;31m"`
e_BLUE=`echo -e "¥033[1;36m"`

unset LSCOLORS
export EDITOR=/Applications/MacVim.app/Contents/MacOS/Vim
export BROWSER=w3m
export PATH=/usr/local/bin:$PATH
export LANG=ja_JP.UTF-8
export LESSCHARSET=utf-8
export EDITOR=vim
export PATH=$PATH:$HOME/local/bin:/usr/local/git/bin
export PATH=$PATH:$HOME/dotfiles/bin
export PATH=$PATH:/sbin:/usr/local/bin
export MANPATH=$MANPATH:/opt/local/man:/usr/local/share/man
export PATH="$PATH:$HOME/.rvm/bin"

[[ -s "$HOME/.pythonbrew/etc/bashrc" ]] && source "$HOME/.pythonbrew/etc/bashrc"

case "${OSTYPE}" in
    darwin*)
        export PATH=$PATH:/opt/local/bin:/opt/local/sbin
        export PATH=$PATH:/System/Library/PrivateFrameworks/Apple80211.framework/Versions/A/Resources
        ;;
    freebsd*)
        case ${UID} in
            0)
                updateports()
                {
                    if [ -f /usr/ports/.portsnap.INDEX ]
                    then
                        portsnap fetch update
                    else
                        portsnap fetch extract update
                    fi
                    (cd /usr/ports/; make index)

                    portversion -v -l \<
                }
                alias appsupgrade='pkgdb -F && BATCH=YES NO_CHECKSUM=YES portupgrade -a'
                ;;
        esac
        ;;
esac
### }}}

### setopt {{{
setopt auto_cd
setopt auto_list
setopt auto_menu
setopt auto_param_keys
setopt auto_param_slash
setopt auto_pushd
setopt autopushd
setopt brace_ccl
setopt chase_links
setopt complete_aliases
setopt correct_all
setopt extended_glob
setopt globdots
setopt hist_ignore_all_dups
setopt hist_no_store
setopt hist_reduce_blanks
setopt inc_append_history
setopt list_packed
setopt list_types
setopt magic_equal_subst
setopt multios
setopt no_clobber
setopt noautoremoveslash
setopt nolistbeep
setopt path_dirs
setopt pushd_ignore_dups
setopt share_history
### }}}

### cdr {{{
autoload -Uz chpwd_recent_dirs cdr add-zsh-hook
zstyle ':completion:*:*:cdr:*:*' menu selection
zstyle ':completion:*' recent-dirs-insert both
zstyle ':chpwd:*' recent-dirs-max 500
zstyle ':chpwd:*' recent-dirs-default true
zstyle ':chpwd:*' recent-dirs-pushd true
### }}}

### color {{{
zstyle ':completion:*:sudo:*' command-path /usr/local/sbin /usr/local/bin /usr/sbin /usr/bin /sbin /bin
zstyle ':completion:*' list-colors di=34 fi=0
case "${TERM}" in
    xterm)
        export TERM=xterm-color

        ;;
    kterm)
        export TERM=kterm-color
        stty erase
        ;;

    cons25)
        unset LANG
        export LSCOLORS=ExFxCxdxBxegedabagacad

        export LS_COLORS='di=01;32:ln=01;35:so=01;32:ex=01;31:bd=46;34:cd=43;34:su=41;30:sg=46;30'
        zstyle ':completion:*' list-colors \
            'di=;36;1' 'ln=;35;1' 'so=;32;1' 'ex=31;1' 'bd=46;34' 'cd=43;34'
        ;;

    kterm*|xterm*)
        export CLICOLOR=1
        export LSCOLORS=ExFxCxDxBxegedabagacad

        zstyle ':completion:*' list-colors \
            'di=36' 'ln=35' 'so=32' 'ex=31' 'bd=46;34' 'cd=43;34'
        ;;

    dumb)
        echo "Welcome Emacs Shell"
        ;;
esac

autoload colors
colors
LS_COLORS="di=34:ln=35:so=32:pi=33:ex=31:bd=46;34:cd=43;34:su=41;30:sg=46;30:tw=42;30:ow=43;30"
export LS_COLORS

if [ -f ~/.dircolors ]; then
    if type dircolors > /dev/null 2>&1; then
        eval $(dircolors ~/.dircolors)
    elif type gdircolors > /dev/null 2>&1; then
        eval $(gdircolors ~/.dircolors)
    fi
fi

### }}}

### autoload, zstyle {{{
#HELPDIR=/usr/local/share/zsh/helpfiles
#alias run-help >/dev/null 2>&1 && unalias run-help
autoload -Uz run-help
autoload -Uz run-help-git
autoload -Uz run-help-svn
autoload -Uz run-help-svk
autoload -Uz run-help-openssl
autoload -Uz run-help-p4
autoload -Uz run-help-sudo
autoload zed
autoload predict-on
autoload history-search-end
autoload -Uz select-word-style
select-word-style default
autoload -Uz zmv
autoload -U url-quote-magic
autoload -U compinit
compinit
zstyle ':zle:*' word-chars " _-./;@"
zstyle ':zle:*' word-style unspecified
zstyle ':completion:*:default' menu select=1
zstyle ':completion:history-words:*' list no
zstyle ':completion:history-words:*' menu yes
zstyle ':completion:history-words:*' remove-all-dups yes
bindkey "\e/" _history-complete-older
bindkey "\e," _history-complete-newer

zstyle ':filter-select' max-lines $(($LINES / 2))
zstyle ':completion:*' verbose yes
zstyle ':completion:*' completer _expand _complete _match _prefix _approximate _list _history
zstyle ':completion:*:messages' format '%F{YELLOW}%d'$DEFAULT
zstyle ':completion:*:warnings' format '%F{RED}No matches for:''%F{YELLOW} %d'$DEFAULT
zstyle ':completion:*:descriptions' format '%F{YELLOW}completing %B%d%b'$DEFAULT
zstyle ':completion:*:options' description 'yes'
zstyle ':completion:*' group-name ''
zstyle ':completion:*' use-cache true
zstyle ':completion:*' list-separator '-->'
zstyle ':completion:*:manuals' separate-sections true
zstyle ':completion:*' list-colors ${(s.:.)LS_COLORS}
if [ -n "$LS_COLORS" ]; then
    zstyle ':completion:*' list-colors ${(s.:.)LS_COLORS}
fi
### }}}

### magick {{{
typeset -A abbreviations
abbreviations=(
"L"    "| $PAGER"
"G"    "| grep"

"HEAD^"     "HEAD\\^"
"HEAD^^"    "HEAD\\^\\^"
"HEAD^^^"   "HEAD\\^\\^\\^"
"HEAD^^^^"  "HEAD\\^\\^\\^\\^\\^"
"HEAD^^^^^" "HEAD\\^\\^\\^\\^\\^"
)

magic-abbrev-expand () {
    local MATCH
    LBUFFER=${LBUFFER%%(#m)[-_a-zA-Z0-9^]#}
    LBUFFER+=${abbreviations[$MATCH]:-$MATCH}
}

magic-abbrev-expand-and-insert () {
    magic-abbrev-expand
    zle self-insert
}

magic-abbrev-expand-and-accept () {
    magic-abbrev-expand
    zle accept-line
}

no-magic-abbrev-expand () {
    LBUFFER+=' '
}

zle -N magic-abbrev-expand
zle -N magic-abbrev-expand-and-insert
zle -N magic-abbrev-expand-and-accept
zle -N no-magic-abbrev-expand
bindkey "\r"  magic-abbrev-expand-and-accept
bindkey "^J"  accept-line
bindkey " "   magic-abbrev-expand-and-insert
bindkey "."   magic-abbrev-expand-and-insert
bindkey "^x " no-magic-abbrev-expand

function rmf(){
for file in $*
do
    __rm_single_file $file
done
}

function __rm_single_file(){
if ! [ -d ~/.Trash/ ]
then
    command /bin/mkdir ~/.Trash
fi

if ! [ $# -eq 1 ]
then
    echo "__rm_single_file: 1 argument required but $# passed."
    exit
fi

if [ -e $1 ]
then
    BASENAME=`basename $1`
    NAME=$BASENAME
    COUNT=0
    while [ -e ~/.Trash/$NAME ]
    do
        COUNT=$(($COUNT+1))
        NAME="$BASENAME.$COUNT"
    done

    command /bin/mv $1 ~/.Trash/$NAME
else
    echo "No such file or directory: $file"
fi
}

zle -N self-insert url-quote-magic
zle -N history-beginning-search-backward-end history-search-end
zle -N history-beginning-search-forward-end history-search-end

# }}}

### directory {{{

function chpwd() { ls -aCFG }

function mkcd() {
if [[ -d $1 ]]; then
    echo "It already exsits! Cd to the directory."
    cd $1
else
    echo "Created the directory and cd to it."
    mkdir -p $1 && cd $1
fi
}

function cdup_dir() {
if [[ -z "$BUFFER" ]]; then
    echo
    cd ..
    ls -aF
    zle reset-prompt
else
    zle self-insert 'k'
fi
 }
 zle -N cdup_dir
 bindkey '^k' cdup_dir

 function cddown_dir(){
 com='$SHELL -c "ls -AF . | grep / "'
 while [ $? = 0 ]
 do
     cdir=`eval $com | peco`
     if [ $? = 0 ];then
         cd $cdir
         eval $com
     else
         break
     fi
 done
 zle reset-prompt
}
zle -N cddown_dir
bindkey '^j' cddown_dir

### }}}

### stack {{{

local p_buffer_stack=""
local -a buffer_stack_arr

function make_p_buffer_stack()
{
    if [[ ! $#buffer_stack_arr > 0 ]]; then
        p_buffer_stack=""
        return
    fi
    p_buffer_stack="%F{black} $buffer_stack_arr %f"
}


show_buffer_stack() {
    POSTDISPLAY="
    stack: $LBUFFER"
    zle push-line-or-edit
}
zle -N show_buffer_stack
setopt noflowcontrol
bindkey '^Q' show_buffer_stack
### }}}

### golang {{{

if [ -x "`which go`" ]; then
  export GOPATH=$HOME/go
  export PATH=$PATH:$GOROOT/bin:$GOPATH/bin
fi

### }}}

### clipboard {{{
## pbcopy
case ${OSTYPE} in
  linux*)
    if [ ! -f /usr/bin/xsel ];then
      sudo pacman -S xsel
    fi
    alias pbcopy='xsel --clipboard --input'
    ;;
  cygwin*)
    alias pbcopy='putclip'
    ;;
esac

## buffer
pbcopy-buffer(){
  case ${OSTYPE} in
    freebsd*|darwin*)
      print -rn $BUFFER | pbcopy
      ;;
    linux*)
      print -rn $BUFFER | xclip -i -selection clipboard
      ;;
    cygwin*)
      print -rn $BUFFER | putclip
      ;;
  esac
  zle -M "copy : ${BUFFER}"
}
zle -N pbcopy-buffer
bindkey '^p^p' pbcopy-buffer

## alias
if which pbcopy >/dev/null 2>&1 ; then
  # Mac
  alias -g C='| pbcopy'
elif which xclip >/dev/null 2>&1 ; then
  # Linux
  alias -g C='| xclip --input --clipboard'
elif which putclip >/dev/null 2>&1 ; then
  # Cygwin
  alias -g C='| putclip'
fi

## bindkey
# bindkey -s '^b' " | pbcopy"

## clipboard-history
function clipboard-history (){
case $OSTYPE in
  linux*)
    if [ ! -f /usr/bin/anamnesis ];then
      sudo yaourt -S anamnesis
    fi
    anamnesis -l 100 | sed -n '3,100p' | peco | cut -d u -f 2- | head -c -3 | tail -c +2  | xclip -i -selection clipboard
    ;;
  freebsd*|darwin*)
    plutil -convert xml1 ~/Library/Application\ Support/ClipMenu/clips.data -o - | parsrx.sh | grep '/plist/dict/array/string ' | sed '1,2d' | sed 's/\/plist\/dict\/array\/string//g' | peco | pbcopy
    ;;
esac
}
zle -N clipboard-history
bindkey '^[c' clipboard-history
### }}}

### stack {{{
function show_buffer_stack() {
POSTDISPLAY="
stack: $LBUFFER"
zle push-line-or-edit
}
zle -N show_buffer_stack
setopt noflowcontrol
bindkey '^Q' show_buffer_stack
### }}}

### open {{{
function openapp() {
case ${OSTYPE} in
  freebsd*|darwin*)
    BUFFER="open -a "
    ;;
  linux*)
    BUFFER="xdg-open "
    #BUFFER="gnome-open "
    ;;
  cygwin*)
    BUFFER="cygstart "
    ;;
esac
CURSOR=$#BUFFER
}
zle -N openapp
bindkey '^o' openapp
# bindkey -s '^o' "open -a "
### }}}

### history {{{
case $OSTYPE in
    linux*)
        function peco-select-history() {
        local tac
        if which tac > /dev/null; then
            tac="tac"
        else
            tac="tail -r"
        fi
        BUFFER=$(\history -rn 1 | \
            eval $tac | \
            peco --query "$LBUFFER")
        CURSOR=$#BUFFER
        zle clear-screen
    }
    ;;
darwin*)
    function peco-select-history() {
    BUFFER=`history -rn 1 | peco`
    CURSOR=$#BUFFER
    zle clear-screen
}
;;
esac
zle -N peco-select-history
bindkey '^h^j' peco-select-history
### }}}

### markdown {{{
function markdown_preview(){
if [ $# -ne 1 ]
then
    echo "error: invalid arguments"
    echo "usage: $0 markdown_file"
    return 1
fi

if [ ! -f "$1" ]
then
    echo "error: $1 dose not exists"
    return 2
fi

(echo '<html><head><meta charset="UTF-8" /></head><body>';
markdown $1; echo '</body></html>')\
    | w3m -T text/html -dump

if [ $STY ]
then
    sleep 0.2
    screen -X redisplay
fi
}
### }}}

### virtualbox {{{
function vm (){
#zsh -c "ls -A ~/VirtualBox\ VMs/" | peco
vbi=`zsh -c "ls -A ~/VirtualBox\ VMs/ | tr ' ' '\n'"`
case $1 in
    [aA]rch*|[mM]ac*)
        echo $vbi | grep $1
        VBoxManage startvm `echo $vbi | grep $1`
        ;;
    "")
        echo $vbi | grep win
        echo win
        VBoxManage startvm `echo $vbi | grep win`
        ;;
    -a)
        echo $vbi | tr '\n' ' '
        VBoxManage startvm `echo $vbi | tr '\n' ' '`
    ;;
    *)
        VBoxManage startvm `echo "$vbi" | peco`
        ;;
esac
}

function vm-window (){
osascript << EOF

--tell application "System Events"
--  tell process "VirtualBoxVM"
--    every UI element
--  end tell
--end tell

tell app "VirtualBoxVM"
activate
end tell
EOF
}

### }}}

### tmux {{{

## auto-start
case $OSTYPE in
    darwin*)
        if [ -z "$SSH_CONNECTION" -a ${UID} -ne 0 -a -z "$TMUX" -a -z "$STY" ]; then
            if type tmux >/dev/null 2>&1; then
                tmux
            elif type tmux >/dev/null 2>&1; then
                if tmux has-session && tmux list-sessions | egrep -q '.*]$'; then
                    tmux attach && echo "tmux attached session "
                else
                    tmux new-session && echo "tmux created new session"
                fi
            elif type screen >/dev/null 2>&1; then
                screen -rx || screen -D -RR
            fi
        fi
        ;;
    linux*)
        if [ -z "$TMUX" -a -z "$STY" ]; then
            if type tmux >/dev/null 2>&1; then
                if tmux has-session && tmux list-sessions | /usr/bin/grep -qE '.*]$'; then
                    tmux -2 attach && echo "tmux attached session "
                else
                    tmux -2 new-session && echo "tmux created new session"
                fi
            fi
        fi
        ;;
esac

##copy-mode
function tmux-copy-line () {
tmux copy-mode\; send-keys 2k0Vj Enter
}
zle -N tmux-copy-line
bindkey '^[n' tmux-copy-line

function tmux-copy-all () {
tmux copy-mode\; send-keys ggVG Enter
#tmux copy-mode\; send-keys Space\; send-keys '$'\; send-keys Enter
}
zle -N tmux-copy-all
bindkey '^[m' tmux-copy-all
### }}}

### alias {{{
alias lf="ls -F"
alias ll="ls -l"
alias 'ps?'='pgrep -l -f'
alias pk='pkill -f'
alias du="du -h"
alias duh="du -h ./ --max-depth=1"
alias su="su -l"
alias 'src'='exec zsh'
alias -g V="| vim -"
alias -g EV="| xargs --verbose sh -c 'vim \"\$@\" < /dev/tty'"
alias -g RET="RAILS_ENV=test"
alias -g RED="RAILS_ENV=development"
alias -g REP="RAILS_ENV=production"
alias raket='RAILS_ENV=test rake'
alias raked='RAILS_ENV=development rake'
alias rakep='RAILS_ENV=production rake'
alias ccat='pygmentize -O style=vim -f console256 -g'
alias less='less -r'
alias df='df -h'
alias free='free -m'
alias 'gr'='grep --color=auto -ERUIn'
alias 'm'='make'
alias 'mn'='make native-code'
alias 'mc'='make clean'
alias sc='screen -S main'
alias sn='screen'
alias sl='screen -ls'
alias sr='screen -r main'
alias srr='screen -U -D -RR'
alias tma='tmux attach'
alias tma0='tmux attach -t 0'
alias tma1='tmux attach -t 1'
alias tma2='tmux attach -t 2'
alias tml='tmux list-sessions'
alias pon='predict-on'
alias poff='predict-off'
alias cp='nocorrect cp -irp'
alias refe='nocorrect refe'
alias g='git'
alias gi='git'
alias oppai='git'
alias gs='git status -s -b'
alias gst='git status -s -b'
alias gc='git commit'
alias gci='git commit -a'
alias java='nocorrect java'
alias erl='nocorrect erl'
alias sbcl='nocorrect sbcl'
alias gosh='nocorrect gosh'
alias node='nocorrect node'
alias scala='scala -deprecation -unchecked -explaintypes'
alias scc='scalac -deprecation -unchecked -explaintypes'
alias sci='scala -deprecation -unchecked -explaintypes -cp $SCALA_CLASSPATH -i ~/import.scala'
alias sce='scala'
alias ex='extract'
alias be='bundle exec'
alias grv='grepvim'
alias dircolors="gdircolors"
alias zmv='noglob zmv -W'
alias ls="ls -a"
alias msf='cd /opt/msf/ && ./msfconsole'
alias p="qlmanage -p "$@" >& /dev/null"
alias gotr="altr"
alias trash="sudo rm -rf ~/.Trash/"
alias qm='qlmanage -p "$@" >& /dev/null'
alias st='/Applications/Sublime\ Text\ 2.app/Contents/SharedSupport/bin/subl'
alias qrank="w3m http://qrank.wbsrv.net/"
alias color-terminal='for c in {000..255}; do echo -n "\e[38;5;${c}m $c" ; [ $(($c%16)) -eq 15 ] && echo;done;echo'
alias ds.store="sudo find ./ -name '.DS_Store' -delete"
alias rgen="rake generate && rake preview"
alias where="command -v"
alias remem='du -sx / &> /dev/null & sleep 5 && kill $!'
alias mf='sudo purge'
alias vs='vim ~/.vimrc'
alias zs='vim ~/.zshrc'
alias ts='vim ~/.tmux.conf'
alias zr='source ~/.zshrc && exec $SHELL'
alias zd='vim ~/dotfiles/.zshrc'
alias vim-trans='vim -c "ExciteTranslate"'
alias gistvim='vim * -c "bufdo %s/foo/bar/g | Gist"'
alias f='vim +VimFiler'
alias w3mjman='W3MMAN_MAN=jman w3mman'
alias w3h='rm ~/.w3m/history && w3m -N'
alias gd='dirs -v; echo -n "select number: "; read newdir; cd +"$newdir"'

case $OSTYPE in
    darwin*)
        #/Applications/VLC.app/Contents/MacOS/VLC -I rc
        # interface:ncurses, speed:2
        alias sy='open -a "system preferences"'
        alias vlc0='/Applications/VLC.app/Contents/MacOS/VLC --rate=2 && sleep 3;reset'
        alias vlc1='killall -KILL VLC'
        alias ctags="`brew --prefix`/usr/local/bin/ctags"
        alias up="brew update && brew upgrade"
        alias ll='gls -slhAF --color'
        alias gls='gls -lAFh --color=auto'
        eval `dircolors ~/dotfiles/dircolors-solarized/dircolors.ansi-dark`
        ;;
    linux*)
        alias up="sudo pacman -Syu && sudo yaourt -Syu"
        alias vim="/usr/bin/vim"
        ;;
esac

        if which pyenv > /dev/null; then eval "$(pyenv init -)"; fi

### }}}

### download {{{

export DOTFILE=$HOME/dotfiles
export PLUGIN=$DOTFILE/.zsh/plugin

## completion
if [ ! -d $PLUGIN/zsh-completions ];then
    git clone git://github.com/zsh-users/zsh-completions $PLUGIN/zsh-completions
fi
fpath=($PLUGIN/zsh-completions/src $fpath)

## powerline {{{
if [ ! -f $PLUGIN/powerline.zsh ];then
    curl https://gist.githubusercontent.com/syui/e3fad84e3dba8a3f667b/raw/powerline.zsh -o $PLUGIN/powerline.zsh
fi

if [ ! -d $PLUGIN/powerline-bash ];then
    git clone https://github.com/milkbikis/powerline-bash $PLUGIN/powerline-bash
fi

#ln -s $PLUGIN/powerline-bash/powerline-bash.py ~/powerline-bash.py
#
#function powerline_precmd() {
#export PS1="$(~/powerline-bash.py $? --shell zsh)"
#        }
#
#        function install_powerline_precmd() {
#        for s in "${precmd_functions[@]}"; do
#            if [ "$s" = "powerline_precmd" ]; then
#                return
#            fi
#        done
#        precmd_functions+=(powerline_precmd)
#    }
#
#    install_powerline_precmd
## }}}

## tmux-powerline
# iTerm : Treat ambiguous-width characters as double width
case $OSTYPE in
    darwin*)
        if ! type tmux > /dev/null 2>&1;then
            brew tap waltarix/homebrew-customs
            brew update
            brew install waltarix/customs/tmux
        fi
    ;;
esac

if type tmux > /dev/null 2>&1;then
    if [ ! -d $DOTFILE/.tmux/tmux-powerline ];then
        git clone https://github.com/erikw/tmux-powerline $DOTFILE/.tmux/tmux-powerline
    fi
    if [ ! -d $DOTFILE/.tmux/tmux-colors-solarized ];then
        git clone https://github.com/seebi/tmux-colors-solarized $DOTFILE/.tmux/tmux-colors-solarized
    fi
fi

if [ ! -f $DOTFILE/.tmux/tmux-powerline/segments/used-mem ];then
    curl https://raw.githubusercontent.com/yonchu/used-mem/master/used-mem -o $DOTFILE/.tmux/tmux-powerline/segments/used-mem
    chmod +x $DOTFILE/.tmux/tmux-powerline/segments/used-mem
fi

if [ ! -f $DOTFILE/.tmux/tmux-powerline/segments/mplayer_tmux.sh ];then
    curl https://raw.githubusercontent.com/syui/mplayer_script/master/mplayer_tmux.sh -o $DOTFILE/.tmux/tmux-powerline/segments/mplayer_tmux.sh
    chmod +x $DOTFILE/.tmux/tmux-powerline/segments/mplayer_tmux.sh
fi

if [ ! -f $DOTFILE/.tmux/.tmux.conf.mac ];then
    curl https://gist.githubusercontent.com/syui/5c49d1296c992d8af737/raw/.tmux.conf.mac -o $DOTFILE/.tmux/.tmux.conf.mac
fi

## vim
if [ ! -d ~/.vim/bundle/neobundle.vim ];then
    curl https://raw.githubusercontent.com/Shougo/neobundle.vim/master/bin/install.sh | sh
fi

## oh-my-zsh
if [ ! -d $PLUGIN/oh-my-zsh ];then
    git clone https://github.com/robbyrussell/oh-my-zsh $PLUGIN/oh-my-zsh
fi

## cheat-sheet
if [ -f $PLUGIN/oh-my-zsh/templates/zshrc.zsh-template ];then
    cheat-sheet () { zle -M "`cat ~/dotfiles/.zsh/cheat-sheet`" }
    zle -N cheat-sheet
    # bindkey "^[^h" cheat-sheet
fi

## golang
if [ ! -f ~/dotfiles/.zsh/plugin/golang-crosscompile/crosscompile.bash ];then
  git clone https://github.com/davecheney/golang-crosscompile ~/dotfiles/.zsh/plugin/golang-crosscompile
fi

## growl
if [ ! -f ~/dotfiles/.zsh/plugin/growl.zsh ];then
       curl https://raw.githubusercontent.com/patbenatar/dotfiles/master/zsh/growl.zsh -o $HOME/dotfiles/.zsh/plugin/growl.zsh
  chmod +x ~/dotfiles/.zsh/plugin/growl.zsh
fi

## rupa/z
case $OSTYPE in
  drawin*)
    if [ -f `brew --prefix`/etc/profile.d/z.sh ];then
      brew install z
    fi
    . `brew --prefix`/etc/profile.d/z.sh
    ;;
  linux*)
    if [ ! -d ~/dotfiles/.zsh/plugin/z ];then
      git clone https://github.com/rupa/z ~/dotfiles/.zsh/plugin/z
    fi
    . ~/dotfiles/.zsh/plugin/z/z.sh
    ;;
esac

## _z  {{{
if ! type _z > /dev/null 2>&1;then
_z () {
  local datafile="${_Z_DATA:-$HOME/.z}"
  [ -z "$_Z_OWNER" -a -f "$datafile" -a ! -O "$datafile" ] && return
  if [ "$1" = "--add" ]
  then
    shift
    [ "$*" = "$HOME" ] && return
    local exclude
    for exclude in "${_Z_EXCLUDE_DIRS[@]}"
    do
      [ "$*" = "$exclude" ] && return
    done
    local tempfile="$datafile.$RANDOM"
    while read line
    do
      [ -d "${line%%\|*}" ] && echo $line
    done < "$datafile" | awk -v path="$*" -v now="$(date +%s)" -F"|" '
            BEGIN {
                rank[path] = 1
                time[path] = now
            }
            $2 >= 1 {
                # drop ranks below 1
                if( $1 == path ) {
                    rank[$1] = $2 + 1
                    time[$1] = now
                } else {
                    rank[$1] = $2
                    time[$1] = $3
                }
                count += $2
            }
            END {
                if( count > 9000 ) {
                    # aging
                    for( x in rank ) print x "|" 0.99*rank[x] "|" time[x]
                } else for( x in rank ) print x "|" rank[x] "|" time[x]
            }
        ' 2> /dev/null >| "$tempfile"
    if [ $? -ne 0 -a -f "$datafile" ]
    then
      env rm -f "$tempfile"
    else
      [ "$_Z_OWNER" ] && chown $_Z_OWNER:$(id -ng $_Z_OWNER) "$tempfile"
      env mv -f "$tempfile" "$datafile" || env rm -f "$tempfile"
    fi
  elif [ "$1" = "--complete" -a -s "$datafile" ]
  then
    while read line
    do
      [ -d "${line%%\|*}" ] && echo $line
    done < "$datafile" | awk -v q="$2" -F"|" '
            BEGIN {
                if( q == tolower(q) ) imatch = 1
                q = substr(q, 3)
                gsub(" ", ".*", q)
            }
            {
                if( imatch ) {
                    if( tolower($1) ~ tolower(q) ) print $1
                } else if( $1 ~ q ) print $1
            }
        ' 2> /dev/null
  else
    while [ "$1" ]
    do
      case "$1" in
        (--) while [ "$1" ]
          do
            shift
            local fnd="$fnd${fnd:+ }$1"
          done ;;
        (-*) local opt=${1:1}
          while [ "$opt" ]
          do
            case ${opt:0:1} in
              (c) local fnd="^$PWD $fnd" ;;
              (h) echo "${_Z_CMD:-z} [-chlrtx] args" >&2
                return ;;
              (x) sed -i -e "\:^${PWD}|.*:d" "$datafile" ;;
              (l) local list=1 ;;
              (r) local typ="rank" ;;
              (t) local typ="recent" ;;
            esac
            opt=${opt:1}
          done ;;
        (*) local fnd="$fnd${fnd:+ }$1" ;;
      esac
      local last=$1
      shift
    done
    [ "$fnd" -a "$fnd" != "^$PWD " ] || local list=1
    case "$last" in
      (/*) [ -z "$list" -a -d "$last" ] && cd "$last" && return ;;
    esac
    [ -f "$datafile" ] || return
    local cd
    cd="$(while read line; do
            [ -d "${line%%\|*}" ] && echo $line
        done < "$datafile" | awk -v t="$(date +%s)" -v list="$list" -v typ="$typ" -v q="$fnd" -F"|" '
            function frecent(rank, time) {
                # relate frequency and time
                dx = t - time
                if( dx < 3600 ) return rank * 4
                if( dx < 86400 ) return rank * 2
                if( dx < 604800 ) return rank / 2
                return rank / 4
            }
            function output(files, out, common) {
                # list or return the desired directory
                if( list ) {
                    cmd = "sort -n >&2"
                    for( x in files ) {
                        if( files[x] ) printf "%-10s %s\n", files[x], x | cmd
                    }
                    if( common ) {
                        printf "%-10s %s\n", "common:", common > "/dev/stderr"
                    }
                } else {
                    if( common ) out = common
                    print out
                }
            }
            function common(matches) {
                # find the common root of a list of matches, if it exists
                for( x in matches ) {
                    if( matches[x] && (!short || length(x) < length(short)) ) {
                        short = x
                    }
                }
                if( short == "/" ) return
                # use a copy to escape special characters, as we want to return
                # the original. yeah, this escaping is awful.
                clean_short = short
                gsub(/[\(\)\[\]\|]/, "\\\\&", clean_short)
                for( x in matches ) if( matches[x] && x !~ clean_short ) return
                return short
            }
            BEGIN {
                gsub(" ", ".*", q)
                hi_rank = ihi_rank = -9999999999
            }
            {
                if( typ == "rank" ) {
                    rank = $2
                } else if( typ == "recent" ) {
                    rank = $3 - t
                } else rank = frecent($2, $3)
                if( $1 ~ q ) {
                    matches[$1] = rank
                } else if( tolower($1) ~ tolower(q) ) imatches[$1] = rank
                if( matches[$1] && matches[$1] > hi_rank ) {
                    best_match = $1
                    hi_rank = matches[$1]
                } else if( imatches[$1] && imatches[$1] > ihi_rank ) {
                    ibest_match = $1
                    ihi_rank = imatches[$1]
                }
            }
            END {
                # prefer case sensitive
                if( best_match ) {
                    output(matches, best_match, common(matches))
                } else if( ibest_match ) {
                    output(imatches, ibest_match, common(imatches))
                }
            }
        ')"
    [ $? -gt 0 ] && return
    [ "$cd" ] && cd "$cd"
  fi
}
fi
### }}}

compctl -U -K _z_zsh_tab_completion ${_Z_CMD:-z}


## zaw/zaw
if [ ! -d ~/dotfiles/.zsh/plugin/zaw ];then
  git clone https://github.com/zsh-users/zaw ~/dotfiles/.zsh/plugin/zaw
fi
if [ ! -f ~/dotfiles/.zsh/plugin/zaw/sources/zaw-z.zsh ];then
  curl https://raw.githubusercontent.com/lovingly/dotfiles/master/zsh.d/zaw/zaw-z.zsh -o $HOME/dotfiles/.zsh/plugin/zaw/sources/zaw-z.zsh
  chmod +x $HOME/dotfiles/.zsh/plugin/zaw/sources/zaw-z.zsh
fi

## syui/airchrome.zsh
if [ ! -f $PLUGIN/airchrome.zsh/airchrome.zsh ];then
    git clone https://github.com/syui/airchrome.zsh $PLUGIN/airchrome.zsh
fi

## syntax-highlight
if [ ! -f $HOME/dotfiles/.zsh/plugin/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh ];then
  git clone https://github.com/zsh-users/zsh-syntax-highlighting $HOME/dotfiles/.zsh/plugin/zsh-syntax-highlighting
fi
### }}}

### source {{{

#source $PLUGIN/oh-my-zsh

source ~/dotfiles/.zsh/plugin/golang-crosscompile/crosscompile.bash
source ~/dotfiles/.zsh/plugin/zaw/zaw.zsh
source $HOME/dotfiles/.zsh/plugin/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh

[ -f ~/.zshrc.local ] && source ~/.zshrc.local

[ -s ${HOME}/.rvm/scripts/rvm ] && source ${HOME}/.rvm/scripts/rvm

case $OSTYPE in
    darwin*)
        source $PLUGIN/airchrome.zsh/airchrome.zsh
        source $PLUGIN/growl.zsh
    ;;
esac

unsetopt sh_word_split

### }}}

### bindkey {{{

bindkey -M viins 'jj' vi-cmd-mode
bindkey "^I" menu-complete
bindkey '^h^h' run-help
bindkey -s '^o^o' 'vim `zsh -c "ls -A" | peco`'
bindkey -s '^o' "open -a "
bindkey "^[u" undo
bindkey "^[r" redo
bindkey '^]'   vi-find-next-char
bindkey '^[^]' vi-find-prev-char
bindkey "^?" backward-delete-char
bindkey -a 'q' push-line
bindkey "^p" history-beginning-search-backward-end
bindkey "^n" history-beginning-search-forward-end
bindkey "\\ep" history-beginning-search-backward-end
bindkey "\\en" history-beginning-search-forward-end

bindkey '^[[7~' beginning-of-line
bindkey '^[[8~' end-of-line
bindkey '^[[2~' overwrite-mode
bindkey '^[[3~' delete-char
bindkey '^[[A'  up-line-or-history
bindkey '^[[B'  down-line-or-history
bindkey '^[[C'  forward-char
bindkey '^[[D'  backward-char
bindkey '^[[5~' history-beginning-search-backward
bindkey '^[[6~' history-beginning-search-forward

## zaw {{{
bindkey '^x' zaw
bindkey '^h' zaw-history
bindkey '^@' zaw-gitdir
bindkey '^r' zaw-open-file
bindkey '^j^j' zaw-cdr
bindkey '^j^k' zaw-z
### }}}

### }}}

### function {{{
ex() {
  if [ -f $1 ] ; then
    case $1 in
      *.tar.bz2)   tar xjf $1   ;;
      *.tar.gz)    tar xzf $1   ;;
      *.bz2)       bunzip2 $1   ;;
      *.rar)       unrar x $1     ;;
      *.gz)        gunzip $1    ;;
      *.tar)       tar xf $1    ;;
      *.tbz2)      tar xjf $1   ;;
      *.tgz)       tar xzf $1   ;;
      *.zip)       unzip $1     ;;
      *.Z)         uncompress $1;;
      *.7z)        7z x $1      ;;
      *)           echo "'$1' cannot be extracted via ex()" ;;
    esac
  else
    echo "'$1' is not a valid file"
  fi
}

grepvim() {
    XFS=`grep -ERUInl $* | uniq | xargs`
    if [ "$XFS" ] ; then
        vim `grep -ERUInl $* | uniq | xargs`
    fi
}

function gte() {
google_translate "$*" "en-ja"
}

function gtj() {
google_translate "$*" "ja-en"
}

function google_translate() {
local str opt cond

if [ $# != 0 ]; then
    str=`echo $1 | sed -e 's/  */+/g'` # 1文字以上の半角空白を+に変換
    cond=$2
    if [ $cond = "ja-en" ]; then
        # ja -> en 翻訳
        opt='?hl=ja&sl=ja&tl=en&ie=UTF-8&oe=UTF-8'
    else
        # en -> ja 翻訳
        opt='?hl=ja&sl=en&tl=ja&ie=UTF-8&oe=UTF-8'
    fi
else
    opt='?hl=ja&sl=en&tl=ja&ie=UTF-8&oe=UTF-8'
fi

opt="${opt}&text=${str}"
w3m +13 "http://translate.google.com/${opt}"
}
function make() {
LANG=C command make "$@" 2>&1 | sed -e "s@[Ee]rror:.*@$e_RED&$e_normal@g" -e "s@cannot¥sfind.*@$e_RED&$e_normal@g" -e "s@[Ww]arning:.*@$e_BLUE&$e_normal@g"
}
function cwaf() {
LANG=C command ./waf "$@" 2>&1 | sed -e "s@[Ee]rror:.*@$e_RED&$e_normal@g" -e "s@cannot¥sfind.*@$e_RED&$e_normal@g" -e "s@[Ww]arning:.*@$e_BLUE&$e_normal@g"
}

expand-to-home-or-insert () {
    if [ "$LBUFFER" = "" -o "$LBUFFER[-1]" = " " ]; then
        LBUFFER+="~/"
    else
        zle self-insert
    fi
}

function separate(){
echo -n $fg_bold[yellow]
for i in $(seq 1 $COLUMNS); do
    echo -n '~'
done
echo -n $reset_color
}

function vol(){
osascript -e "set Volume ${1}"
}
function manowar () {
mpc volume 100
amixer set PCM 100%
}
function torrent-search(){w3m "http://torrentz.eu/search?f=$1"}
function vmu(){VBoxManage storageattach $1 --storagectl ${1}sata1 --port 2 --type dvddrive --medium emptydrive}
function exdel(){exiftool -overwrite_original -all= $1}

function zman() {
PAGER="less -g -s '+/^       "$1"'" man zshall
}

function ccleaner(){
which ccleaner.scpt | xargs osascript &
open -a iterm2-f
}

function gif_make(){
gm convert *.png hoge.gif
rm *.png
}

function markpre(){
watchmedo shell-command -c "qlmanage -p $1" $HOME/blog/
}

function wifi(){
if networksetup -getairportnetwork en0 | grep off; then
    echo on
    networksetup -setairportpower en0 on
else
    echo off
    networksetup -setairportpower en0 off
fi
}

function aunpack-all(){for i in `ls *.$1`;do aunpack $i;done}

function twitter () {
osascript -e 'tell application "Twitter" to close window 1'
}

function unrar-all (){
for i in *.part1.rar
do
    unrar e -o+ $i
done
}

### git init {{{
#touch README.md
#git init
#git add README.md
#git commit -m "first commit"
#git remote add origin https://github.com/syui/syui.github.io.git
#git push -u origin master
### }}}

function gitinit(){
echo -n username:
user=`echo $USER`
repo=`echo $PWD:t`
repo_j={\"name\":\"$repo\"}
url="https://github.com/"$user/$repo.git
curl -u $user https://api.github.com/user/repos -d $repo_j
case $? in
    0)
        rm -rf .git
        rm -rf .DS_Store
        git init
        echo $url
        git remote add origin $url
        git add .
        git commit --allow-empty -m "noun"
        git push -u origin master
        ;;
esac
}

globalias() {
    if [[ $LBUFFER =~ ' [A-Z0-9]+$' ]]; then
        zle _expand_alias
        zle expand-word
    fi
    zle self-insert
}
zle -N globalias
bindkey " " globalias
bindkey "^ " magic-space           # control-space to bypass completion
bindkey -M isearch " " magic-space # normal space during searches


#function help-peco (){
#  s=`run-help | tail -n +2 | tr ' ' '\n' | sed '/^$/d' | peco`
#  man $s
#}
#zle -N help-peco

function au(){
case $1 in
    -o|*)
        SwitchAudioSource -a | grep output | cut -d '(' -f 1 | sed -e 's/ *$//' -e 's/$/"/g' -e 's/^/"/g' | peco | xargs -J % SwitchAudioSource -s %
        ;;
    -i)
        SwitchAudioSource -a | grep input | cut -d '(' -f 1 | sed -e 's/ *$//' -e 's/$/"/g' -e 's/^/"/g' | peco | xargs -J % SwitchAudioSource -t input -s %
        ;;
esac
#zle reset-prompt
}
zle -N au
bindkey '\^^' au

### }}}

### google {{{

function google-search() {
local str opt
if [ $ != 0 ]; then
    for i in $*; do
        str="$str+$i"
    done
    str=`echo $str | sed 's/^\+//'`
    opt='search?num=50&hl=ja&lr=lang_ja'
    opt="${opt}&q=${str}"
fi
w3m http://www.google.co.jp/$opt
}

function goy() {
local str opt
if [ $ != 0 ]; then
    for i in $*; do
        str="$str+$i"
    done
    str=`echo $str | sed 's/^\+//'`
    opt='search?num=50&hl=ja&lr=lang_ja'
    opt="${opt}&q=${str}"
    tbs='&tbs=qdr:y'
fi
w3m http://www.google.co.jp/$opt$tbs
}

function gom() {
local str opt
if [ $ != 0 ]; then
    for i in $*; do
        str="$str+$i"
    done
    str=`echo $str | sed 's/^\+//'`
    opt='search?num=50&hl=ja&lr=lang_ja'
    opt="${opt}&q=${str}"
    tbs='&tbs=qdr:m'
fi
w3m http://www.google.co.jp/$opt$tbs
}

# w3mでALC検索
function alc() {
if [ $ != 0 ]; then
    w3m "http://eow.alc.co.jp/$*/UTF-8/?ref=sa"
else
    w3m "http://www.alc.co.jp/"
fi
}



#>>>
function youtube-post(){
mkdir -p ~/Movies/youtube
google youtube post ~/Movies/youtube/*.mp4 --category People --tags "blog"
google youtube list --delimiter ','
}

functions mod(){
mkdir ~/Music/speed
cd ~/Music/speed && touch mylist.test && rm mylist* && mylist && mplayer -playlist mylist -speed 2 -af scaletempo,volnorm
}

# w3mでyoutube検索
function youtube-search() {
if [ $ != 0 ]; then
    w3m "http://www.youtube.com/results?search_query=$*&search_type=&aq=f"
else
    w3m "http://youtube.com/"
fi
}

# google booksの検索
function book-search() {
local str opt
if [ $ != 0 ]; then
    for i in $*; do
        str="$str+$i"
    done
    str=`echo $str | sed 's/^\+//'`
    opt='search?lr=lang_ja&hl=JA&tbo=p&tbm=bks&tbs=,bkv:p&num=10'
    opt="${opt}&q=${str}"
fi
w3m http://www.google.co.jp/$opt
}

function exmap (){
str=`exiftool -c "%.6f" -GPSPosition ${1} | sed -e 's/GPS Position//' -e 's/://' -e 's/E//'  -e 's/S//' -e 's/W//' -e 's/N//' -e 's/ //g'`
open -a Google\ Chrome "https://maps.google.co.jp/maps?q=$str"
}

function chrome() {
local str opt
if [ $ != 0 ]; then
    for i in $*; do
        str="$str+$i"
    done
    str=`echo $str | sed 's/^\+//'`
    opt='search?num=50&hl=ja&lr=lang_ja'
    opt="${opt}&q=${str}"
fi
open -a Google\ Chrome http://www.google.co.jp/$opt
}

function google_translate() {
local str opt arg

str=`pbpaste` # clipboard
arg=`echo ${@:2} | sed -e 's/  */+/g'` # argument
en_jp="?hl=ja&sl=en&tl=ja&ie=UTF-8&oe=UTF-8" # url

case "$1" in
    "-j") opt="?hl=ja&sl=ja&tl=en&ie=UTF-8&oe=UTF-8&text=${arg}";; # jp -> en translate
"-e") opt="${en_jp}&text=${arg}";; # en -> jp translate
        *) opt="${en_jp}&text=${str}";; # en -> jp translate
    esac

    w3m +20 "http://translate.google.com/${opt}"  # goto 20 line
}

# blogger
function bp(){
    TITLE="$(awk 'NR==1' $1)"
    TAG="$(awk 'NR==2' $1)"
    sed -ie 1,2d $1
    google blogger post --blog "MBA-HACK" --title "${TITLE}" --tags "${TAG}" $1
    url=`google blogger list url --title "${TITLE}" | cut -d , -f 2`
    open -a Google\ Chrome $url
}



function got(){
w3m "http://www.google.co.jp/search?num=50&hl=ja&lr=lang_ja&q=$2&tbs=qdr:${1}"
}

function img-search () {
dir=~/Downloads/pic
mkdir -p $dir
word=`echo $1 | ruby -r cgi -ne 'puts CGI.escape $_.chomp'`
echo $word
url=`curl "http://ajax.googleapis.com/ajax/services/search/images?q=$word&v=1.0&safe=active&imgsz=xxlarge&rsz=large" | jq -r '.responseData.results [] .url'`
cou=`echo $url | wc -l | tr -d ' '`

for (( i=1;i<$cou;i++ ))
do
    urlo=`echo $url | awk "NR==$i"`
    file=${urlo##*/}
    curl $urlo -o $dir/$file
done

qlmanage -p $dir/*
file=`zsh -c "ls -A $dir" | peco`
url=`echo $url | grep $file`
echo $url | pbcopy && pbpaste
rm -rf $dir

}



### }}}

### prompt {{{

source $PLUGIN/powerline.zsh

## default {{{

#case $OSTYPE in
#linux*)
#  TMUX_POWERLINE_SEPARATOR_LEFT_BOLD="◀"
#  TMUX_POWERLINE_SEPARATOR_LEFT_THIN="❮"
#  TMUX_POWERLINE_SEPARATOR_RIGHT_BOLD="▶"
#  TMUX_POWERLINE_SEPARATOR_RIGHT_THIN="❯"
#  TMUX_POWERLINE_GIT="ⓦ"
#;;
#darwin*)
#  TMUX_POWERLINE_SEPARATOR_LEFT_BOLD="⮂"
#  TMUX_POWERLINE_SEPARATOR_LEFT_THIN="⮃"
#  TMUX_POWERLINE_SEPARATOR_RIGHT_BOLD="⮀"
#  TMUX_POWERLINE_SEPARATOR_RIGHT_THIN="⮁"
#  TMUX_POWERLINE_GIT="⭠"
#;;
#esac
#setopt prompt_subst
#setopt prompt_percent
#setopt transient_rprompt
#
#color256()
#{
#  local red=$1; shift
#  local green=$2; shift
#  local blue=$3; shift
#
#  echo -n $[$red * 36 + $green * 6 + $blue + 16]
#}
#
#fg256()
#{
#  echo -n $'\e[38;5;'$(color256 "$@")"m"
#}
#
#bg256()
#{
#  echo -n $'\e[48;5;'$(color256 "$@")"m"
#}
#
#zstyle ':vcs_info:*' max-exports 3
#zstyle ':vcs_info:hg:*' get-revision true
#zstyle ':vcs_info:hg:*' use-simple true
#
#autoload -Uz is-at-least
#zstyle ':vcs_info:git:*' check-for-changes true
#zstyle ':vcs_info:git:*' stagedstr "-"
#zstyle ':vcs_info:git:*' unstagedstr "${TMUX_POWERLINE_GIT}"
#zstyle ':vcs_info:*' actionformats '[%b|%a]'
#
#zstyle ':vcs_info:git:*' formats '%{%k%f%}%F{black}%K{green}${TMUX_POWERLINE_SEPARATOR_RIGHT_BOLD}%F{white}%K{green} %s %f%k%K{blue}%F{green}${TMUX_POWERLINE_SEPARATOR_RIGHT_BOLD}%k%f%%F{white}%K{blue} %b %f%k%K{black}%F{blue}${TMUX_POWERLINE_SEPARATOR_RIGHT_BOLD}%k%f%%F{white}%K{black} %c%u %f%k'
#
#autoload -Uz vcs_info
#
#prompt_bar_left_self="%{%F{white}%K{020}%} %n%{%k%f%}%{%F{white}%K{020}%}@%{%k%f%}%{%F{white}%K{020}%}%m %{%k%f%}%{%B%F{020}%K{020}%}%{%b%f%k%}%K{026}%F{blue}${TMUX_POWERLINE_SEPARATOR_RIGHT_BOLD}%k%f%{%B%F{white}%K{026}%}  [%~]  %{%k%f%b%}%{%k%f%}%K{069}%F{026}${TMUX_POWERLINE_SEPARATOR_RIGHT_BOLD}%k%f%(?.%F{white}%K{069}%}`w | grep user, | cut -d , -f 2` %k%f.%B%K{069}%F{red}%}`w | grep user, | cut -d , -f 2` %b%k%f)%{%K{045}%F{069}${TMUX_POWERLINE_SEPARATOR_RIGHT_BOLD}%k%f%F{white}%K{045}%} %h  %{%k%f%}%K{black}%F{045}${TMUX_POWERLINE_SEPARATOR_RIGHT_BOLD}%k%f"
#
#prompt_bar_left="${prompt_bar_left_self} ${prompt_bar_left_status} ${prompt_bar_left_date}"
#prompt_left='%{%F{white}%K{black}%}  $SHELL  %{%k%f%}%{%K{white}%F{black}${TMUX_POWERLINE_SEPARATOR_RIGHT_BOLD}%k%f%B%F{black}%K{white}%} %# ${p_buffer_stack} %{%b%k%f%f%}%K{black}%F{white}${TMUX_POWERLINE_SEPARATOR_RIGHT_BOLD}%k%f >  '
#
#count_prompt_characters()
#{
#  print -n -P -- "$1" | sed -e $'s/\e\[[0-9;]*m//g' | wc -m | sed -e 's/ //g'
#}
#
#update_prompt()
#{
#  local bar_left_length=$(count_prompt_characters "$prompt_bar_left")
#  local bar_rest_length=$[COLUMNS - bar_left_length]
#  local stash
#  stash="stash "$(git stash list 2>/dev/null | wc -l | tr -d ' ')
#  local ahead
#  ahead="push "$(git rev-list origin/master..master 2>/dev/null \
#    | wc -l \
#    | tr -d ' ')
#  stash="%K{013}%F{black}${TMUX_POWERLINE_SEPARATOR_RIGHT_BOLD}%k%f%{%k%f%}%{%F{white}%K{013}%} $stash %{%k%f%}%F{013}%K{blue}${TMUX_POWERLINE_SEPARATOR_RIGHT_BOLD}%k%f%{%k%f%}%{%F{white}%K{blue}%} $ahead %{%k%f%}%F{blue}%K{green}${TMUX_POWERLINE_SEPARATOR_RIGHT_BOLD}"
#  local stad
#  # stash を有効にする
#  #stad=$stash
#  local bar_left="$prompt_bar_left"$stad
#  local bar_right_without_path="${prompt_bar_right:s/%d//}"
#  local bar_right_without_path_length=$(count_prompt_characters "$bar_right_without_path")
#  bar_right=${prompt_bar_right:s/%d/%(C,%${max_path_length}<...<%d%<<,)/}
#  bar_right="%${bar_rest_length}<<${separator}${bar_right}%<<"
#  prompt_bar_left_2="%K{white}%F{black}${TMUX_POWERLINE_SEPARATOR_RIGHT_BOLD}%k%f%{%F{black}%K{white}%} %l %K{black}%F{white}${TMUX_POWERLINE_SEPARATOR_RIGHT_BOLD}%k%f%{%k%f%}%{%F{white}%K{black}%}  $LANG  %{%k%f%}%F{black}${TMUX_POWERLINE_SEPARATOR_RIGHT_BOLD}"
#
#  PROMPT="${bar_left}${bar_right}${prompt_bar_left_2}"$'\n'"${prompt_left}"
#
#  case "$TERM_PROGRAM" in
#    Apple_Terminal)
#      PROMPT="${PROMPT}"
#      ;;
#  esac
#
#  LANG=C vcs_info >&/dev/null
#  if [ -n "$vcs_info_msg_0_" ]; then
#    PROMPT="${bar_left}${bar_right}${vcs_info_msg_0_}${prompt_bar_left_2}"$'\n'"${prompt_left}"
#  fi
#}
#
#precmd_functions=($precmd_functions update_prompt)
#
## }}}

### vi-mode {{{
#EMACS_INSERT=`bindkey -lL main | cut -d ' ' -f 3`
#if bindkey -lL main | cut -d ' ' -f 3 | grep emacs > /dev/null 2>&1;then
#    EMACS_INSERT="%K{black}%F{011}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%k%f%K{011}%F{034} % $EMACS_INSERT %k%f"
#    VIM_INSERT="%K{011}%F{075}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%k%f%K{075}%F{026} % INSERT %k%f%K{075}%F{black}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%k%f"
#else
#    EMACS_INSERT="%K{black}%F{034}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%k%f%K{034}%F{011} % $EMACS_INSERT %k%f"
#    VIM_INSERT="%K{034}%F{075}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%k%f%K{075}%F{026} % INSERT %k%f%K{075}%F{black}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%k%f"
#fi
##VIM_INSERT="%K{034}%F{075}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%k%f%K{075}%F{026} % INSERT %k%f%K{075}%F{black}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%%k%f"
#RPROMPT="$EMACS_INSERT$VIM_INSERT"
#function zle-keymap-select {
#EMACS_INSERT=`bindkey -lL main | cut -d ' ' -f 3`
#if echo $EMACS_INSERT | grep emacs > /dev/null 2>&1;then
#  EMACS_INSERT="%K{black}%F{011}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%k%f%K{011}%F{034} % $EMACS_INSERT %k%f"
#  VIM_NORMAL="%K{011}%F{125}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%k%f%K{125}%F{015} % NORMAL %k%f%K{125}%F{black}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%k%f"
#  VIM_INSERT="%K{011}%F{075}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%k%f%K{075}%F{026} % INSERT %k%f%K{075}%F{black}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%k%f"
#else
#  EMACS_INSERT="%K{black}%F{034}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%k%f%K{034}%F{011} % $EMACS_INSERT %k%f"
#  VIM_NORMAL="%K{034}%F{125}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%k%f%K{125}%F{015} % NORMAL %k%f%K{125}%F{black}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%k%f"
#  VIM_INSERT="%K{034}%F{075}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%k%f%K{075}%F{026} % INSERT %k%f%K{075}%F{black}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%k%f"
#fi
#RPROMPT="$EMACS_INSERT${${KEYMAP/vicmd/$VIM_NORMAL}/(main|viins)/$VIM_INSERT}"
#zle reset-prompt
#}
#zle -N zle-keymap-select

#function airchrome-bindmode-emacs () {
#bindkey -e
#EMACS_INSERT=`bindkey -lL main | cut -d ' ' -f 3`
#if echo $EMACS_INSERT | grep emacs > /dev/null 2>&1;then
#  EMACS_INSERT="%K{black}%F{011}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%k%f%K{011}%F{034} % $EMACS_INSERT %k%f"
#  VIM_NORMAL="%K{011}%F{125}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%k%f%K{125}%F{015} % NORMAL %k%f%K{125}%F{black}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%k%f"
#  VIM_INSERT="%K{011}%F{075}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%k%f%K{075}%F{026} % INSERT %k%f%K{075}%F{black}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%k%f"
#else
#  EMACS_INSERT="%K{black}%F{011}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%k%f%K{011}%F{034} % $EMACS_INSERT %k%f"
#  VIM_NORMAL="%K{011}%F{125}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%k%f%K{125}%F{015} % NORMAL %k%f%K{125}%F{black}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%k%f"
#  VIM_INSERT="%K{011}%F{075}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%k%f%K{075}%F{026} % INSERT %k%f%K{075}%F{black}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%k%f"
#fi
#RPS1="$EMACS_INSERT${${KEYMAP/vicmd/$VIM_NORMAL}/(main|viins)/$VIM_INSERT}"
#RPS2=$RPS1
#zle reset-prompt
#}
#zle -N airchrome-bindmode-emacs
#bindkey -v '^e' airchrome-bindmode-emacs
#bindkey -a '^e' airchrome-bindmode-emacs
#
#function airchrome-bindmode-vi () {
#bindkey -v
#EMACS_INSERT=`bindkey -lL main | cut -d ' ' -f 3`
#if echo $EMACS_INSERT | grep emacs > /dev/null 2>&1;then
#  EMACS_INSERT="%K{black}%F{011}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%k%f%K{011}%F{034} % $EMACS_INSERT %k%f"
#  VIM_NORMAL="%K{011}%F{125}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%k%f%K{125}%F{015} % NORMAL %k%f%K{125}%F{black}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%k%f"
#  VIM_INSERT="%K{011}%F{075}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%k%f%K{075}%F{026} % INSERT %k%f%K{075}%F{black}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%k%f"
#else
#  EMACS_INSERT="%K{black}%F{034}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%k%f%K{034}%F{011} % $EMACS_INSERT %k%f"
#  VIM_NORMAL="%K{034}%F{125}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%k%f%K{125}%F{015} % NORMAL %k%f%K{125}%F{black}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%k%f"
#  VIM_INSERT="%K{034}%F{075}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%k%f%K{075}%F{026} % INSERT %k%f%K{075}%F{black}${TMUX_POWERLINE_SEPARATOR_LEFT_BOLD}%k%f"
#fi
#RPS1="$EMACS_INSERT${${KEYMAP/vicmd/$VIM_NORMAL}/(main|viins)/$VIM_INSERT}"
#RPS2=$RPS1
#zle reset-prompt
#}
#zle -N airchrome-bindmode-vi
#bindkey -e '^v' airchrome-bindmode-vi
#### }}}
### }}}

### media {{{

case $OSTYPE in

darwin*)

function nico_mylist(){
url=`ls -A . | grep Nico | cut -d ':' -f 2 | sed -e 's/GINZA-//g' -e "s/\.[^.]*$//" | tr '\n' ' '`
data=`date +"%Y_%m_%d"`
echo "nico_mylist.py $data $url" | pbcopy && pbpaste
}

function nico_chrome(){
word1="GINZA-"
url=`zsh -c "ls -A . | grep Niconico | cut -d ':' -f 2"`
url=`echo $url | sed -e "s/$word1/http:\/\/www.nicovideo.jp\/watch\//g" -e "s/\.[^.]*$//"`
line=`echo $url | wc -l | tr -d ' '`
for (( i = $line; i > 0; i-- )) do
    murl=`echo $url | awk "NR==$i"`
    echo $murl
    open -a Google\ Chrome "$murl"
done
}

function picasa(){
    dirp=~/Pictures/picasa
    dirc=github
    qlmanage -p ${dirp}/*
    exiftool -overwrite_original -all= $dirp
    case $1 in
       "")
            #google picasa post -n "$dirc" ~/Pictures/picasa/*.png
            list=`google picasa list "$dirc" --delimiter " " --fields url-direct`
            numb=`bash -c "ls -A $dirp" | wc -l | tr -d ' '`
            echo "$list" | tail -n $numb | pbcopy && pbpaste
    ;;
    esac
    rm -rf $dirp > /dev/null 2>&1
    mkdir -p $dirp
}

function chrome_done_reload (){
osascript << EOF && osascript -e 'tell application "Google Chrome" to close first tab of window 1'
tell application "Google Chrome"
repeat while loading of active tab of window 1
delay 0.1
end repeat
activate
end tell
EOF

cat << EOF | osascript | tr ',' "\n"
tell application "Google Chrome"
set pageURI to get URL of tab of window 1
set pageTitle to get title of tab of window 1
return pageTitle & space & pageURI
end tell
EOF
}

function ffg (){
bas=`cat << EOF | peco | tr -d ' '
mp4 -> mp3
flv -> mp3
swf -> mp3
mp3 -> wav
flv -> wav
mov -> gif
jpg -> png
bmp -> png
EOF` > /dev/null 2>&1

inp=`echo $bas | cut -d '-' -f 1`
oup=`echo $bas | cut -d '>' -f 2`

case $inp in

    swf)
        for i in *.${inp}; do swfextract -m $i -o ${i%.swf}.mp3; done
    ;;

    mov)
        for i in *.${inp}; do ffmpeg -i *.mov -r 8 %04d.png && gm convert *.png ${i%.*}.gif && rm *.png; done
    ;;

    jpg)
        mogrify -format png -quality 100 *.jpg
    ;;

    bmp)
        mogrify -format png -quality 100 *.bmp
    ;;

    *)
        for i in *.${inp}; do ffmpeg -i $i -vn ${i%.*}.${oup}; done
    ;;

esac
}

alias mun='cd ~/Music/new && touch mylist.test && rm mylist* && mylist && mplayer -playlist mylist -novideo -loop 20 -quiet -msglevel all=0 -identify | grep FILE'

function ms (){
dir1=$HOME/Music
file=${0:a:t}
loop=20
speed=2

play=`ps | grep mplayer -s | wc -l | tr -d ' '`

case $play in
    ""|1)
        sea="ID_FILENAME"
        dir="$dir1/"`zsh -c "ls -A $dir1 | peco"`
        com="mplayer -speed $speed -af scaletempo,volnorm -novideo -loop $loop -quiet -msglevel all=0 -identify $dir/*"
        com="${com} | grep $sea"
        eval $com
    ;;
    *)
        pkill mplayer > /dev/null 2>&1
    ;;
esac
}

## twitter
function tweetvim (){
    case $1 in
        "")
            vim +TweetVimUserTimeline
        ;;
        t)
            vim +TweetVimSay
        ;;
        m)
            vim +TweetVimMentions +/@
        ;;
        l)
            vim -c "TweetVimListStatuses fav" +/http
        ;;
        $USER)
            vim -c "TweetVimUserTimeline syui__"
        ;;

    esac
}

alias qiita-line="curl -I 'https://qiita.com/api/v1/items.json'"
alias lingr="vim +J6uil +J6uilStartNotify"
alias iTunes='open -a iTunes'
alias youtube.py='~/youtube-cli/youtube.py'
alias html2text='python ~/html2text/html2text.py'
alias mylist='find `pwd` -maxdepth 1 -mindepth 1 | grep -v "\/\." > mylist'
alias ch="open -a Google\ Chrome --args --gpu-startup-dialog --disable-java --disable-background-mode --renderer-process-limit=2"
alias fu="~/dotfiles/fu/fu"
alias keepass="~/pull/airkeepass/airkeepass"
alias anime="~/script/anitube-cli/anitube-cli"
alias hatena="~/script/hatena-cli/hatena-cli"
alias nicovideo='nicovideo-dl -t -n'
;;

esac
### }}}

### os {{{
case $OSTYPE in
linux*)
        bindkey -v
        export CLICOLOR=1
        export LSCOLORS=ExFxCxDxBxegedabagacad
        export PATH
        # man path
        MANPATH=/usr/local/man:$MANPATH
        export MANPATH
        INFOPATH=/usr/local/info:$INFOPATH
        export INFOPATH

        # Java
        export JAVA_HOME=/usr/java/default
        export PATH=$JAVA_HOME/bin:$PATH

        # Maven2
        export MAVEN_HOME=/usr/local/apache-maven-2.2.1
        export PATH=$MAVEN_HOME/bin:$PATH
        export MAVEN_OPTS=-Xmx1024M

        #rvm
        if [[ -s $HOME/.rvm/scripts/rvm ]] ; then source $HOME/.rvm/scripts/rvm ; fi

        export PATH=$PATH:$HOME/.gem/ruby/1.8/bin

        #alias
        alias ls='ls -alh --color'
        alias vim="/usr/bin/vim"
        alias v="/usr/bin/vim"

        ;;

darwin*)
        zle -N expand-to-home-or-insert
        bindkey -v
        bindkey "@"  expand-to-home-or-insert
        export PATH=/usr/local/bin:/usr/local/sbin:$PATH
        export PATH=/opt/local/bin:/opt/local/sbin:~/bin:$PATH

        # osx alias
        alias pbc='pbcopy'
        alias vo='osascript -e "set Volume 0.00001"'
        # Terminal Colorの設定
        export CLICOLOR=1
        export LSCOLORS=ExFxCxDxBxegedabagacad

        ## vim
        export EDITOR=/Applications/MacVim.app/Contents/MacOS/Vim
        alias vi='/opt/local/bin/vim'
        alias vim='env LANG=ja_JP.UTF-8 /Applications/MacVim.app/Contents/MacOS/Vim "$@"'
        alias v='env LANG=ja_JP.UTF-8 /Applications/MacVim.app/Contents/MacOS/Vim "$@"'

        ##Java7
        export JAVA_HOME=/Library/Java/JavaVirtualMachines/1.7.0.jdk/Contents/Home
        # export JAVA_HOME=/Library/Java/Home
        export PATH=$JAVA_HOME/bin:$PATH
        # デフォルトエンコーディングSJISをUTF-8へ
        export _JAVA_OPTIONS="-Dfile.encoding=UTF-8"

        # haskell
        export PATH=/Users/ozaki/Library/Haskell/bin:$PATH

        # scala
        export SCALA_HOME=/Users/ozaki/.svm/current/rt
        PATH=$SCALA_HOME/bin:$PATH
        export SCALA_DOC_HOME=$SCALA_HOME/../devel-docs/api/
        export SCALA_CLASSPATH=~/sandbox/scala/yuroyoro/yuroyoro-util/target/yuroyoro-util-1.0.jar

        # Ant
        export ANT_VERSION=1.8.0
        export ANT_HOME=~/dev/Tools/apache-ant-${ANT_VERSION}
        export ANT_OPTS=-Xmx1g
        export PATH=$ANT_HOME/bin:$PATH

        # Maven2
        export MAVEN_VERSION=2.2.1
        export MAVEN_HOME=~/dev/Tools/apache-maven-${MAVEN_VERSION}
        export PATH=$MAVEN_HOME/bin:$PATH
        export MAVEN_OPTS=-Xmx1024M

        # man path
        MANPATH=/usr/local/man:$MANPATH
        export MANPATH
        INFOPATH=/usr/local/info:$INFOPATH
        export INFOPATH

        # Mysql
        export MYSQL_HOME=/usr/local/mysql
        export PATH=$MYSQL_HOME/bin:$PATH
        alias h2db='java -cp ~/.m2/repository/com/h2database/h2/1.1.112/h2-1.1.112.jar org.h2.tools.Server'

        # STAX SDK
        export STAX_HOME=~/dev/Project/sandbox/stax-sdk-0.2.11
        export PATH=$PATH:$STAX_HOME

        # Adobe AIR
        export AIR_HOME=~/dev/air
        export FLEX_HOME=~/dev/flex
        export PATH=$PATH:$AIR_HOME/bin:$FLEX_HOME/bin
        export GAE_SDK_VERSION=1.3.4
        GAE_SDK_INSTALLED_DIR=~/sandbox/GoogleAppEngine/sdk
        export GAE_HOME=$GAE_SDK_INSTALLED_DIR/$GAE_SDK_VERSION/google_appengine
        export PATH=$PATH:$GAE_HOME
        export GAEJ_SDK_VERSION=1.3.7
        GAEJ_SDK_INSTALLED_DIR=~/sandbox/GAEJava/sdk
        export GAEJ_HOME=$GAEJ_SDK_INSTALLED_DIR/appengine-java-sdk-$GAEJ_SDK_VERSION
        export PATH=$PATH:$GAEJ_HOME/bin
        export REFE_DATA_DIR=/System/Library/Frameworks/Ruby.framework/Versions/1.8/usr/share/refe
        export GOROOT=$HOME/dev/go
        export GOOS=darwin
        export GOARCH=386
        export PATH=$PATH:$GOROOT/bin
        export NODE_PATH=/usr/local/lib/node:$PATH
        export PATH=/usr/local/share/npm/bin:$PATH
        export JRUBY_HOME=$HOME/sandbox/jruby/jruby-1.5.2
        export PATH=$PATH:$JRUBY_HOME/bin
        export MIRAH_HOME=$HOME/sandbox/mirah/mirah
        export PATH=$PATH:$MIRAH_HOME/bin
        alias tma='tmux attach'
        alias tml='tmux list-window'
        ;;
esac

### font {{{
case $OSTYPE in
    linux*)
        if ! fc-list | grep DejaVuSans > /dev/null 2>&1;then
            sudo pacman -S ttf-dejavu
        fi
    ;;
    darwin*)
        if ! ls ~/Library/Fonts/Ricty* > /dev/null 2>&1;then
            brew tap sanemat/font
            brew install ricty
            brew install fontforge
            cp -f /usr/local/opt/ricty/share/fonts/Ricty*.ttf ~/Library/Fonts/
            #fc-cache -vf
        fi
    ;;
esac
### }}}
### }}}

#{
#  "to-do" : {
#    "os" : [ "coreos", "docker", "vagrant", "awesome", "conky" ],
#    "terminal" : [ "cygwin", "powershell", "vim", "tmux", "git" ],
#    "tool" : [ "dwb", "spacefm", "growl", "ffmpeg", "imagemagick", "googlecl", "keepass", "jq", "canto", "nc", "ssh", "mosh", "nmap", "weechat", "metasploit", "wireshark" ],
#    "lang" : [ "c++", "python", "ruby", "lua", "go", "scala", "typescript", "perl", "sass", "slim", "node.js", "swift", "gauche" ]
#  }
#}
