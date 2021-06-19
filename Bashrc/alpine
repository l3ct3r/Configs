#!/bin/sh
#
# ufetch-alpine - tiny system info for alpine

## INFO

# user is already defined
host="$(hostname)"
os='Alpine Linux'
kernel="$(uname -sr)"
uptime="$(uptime | awk -F, '{sub(".*up ",x,$1);print $1}' | sed -e 's/^[ \t]*//')"
packages="$(apk info | wc -l)"
shell="$(basename "${SHELL}")"

## UI DETECTION

parse_rcs() {
	for f in "${@}"; do
		wm="$(tail -n 1 "${f}" 2> /dev/null | cut -d ' ' -f 2)"
		[ -n "${wm}" ] && echo "${wm}" && return
	done
}

rcwm="$(parse_rcs "${HOME}/.xinitrc" "${HOME}/.xsession")"

ui='unknown'
uitype='UI'
if [ -n "${DE}" ]; then
	ui="${DE}"
	uitype='DE'
elif [ -n "${WM}" ]; then
	ui="${WM}"
	uitype='WM'
elif [ -n "${XDG_CURRENT_DESKTOP}" ]; then
	ui="${XDG_CURRENT_DESKTOP}"
	uitype='DE'
elif [ -n "${DESKTOP_SESSION}" ]; then
	ui="${DESKTOP_SESSION}"
	uitype='DE'
elif [ -n "${rcwm}" ]; then
	ui="${rcwm}"
	uitype='WM'
elif [ -n "${XDG_SESSION_TYPE}" ]; then
	ui="${XDG_SESSION_TYPE}"
fi

ui="$(basename "${ui}")"

## DEFINE COLORS

bold='\033[1m'
black='\033[0;30m'
red='\033[0;31m'
green='\033[0;32m'
yellow='\033[0;33m'
blue='\033[0;34m'
magenta='\033[0;35m'
cyan='\033[0;36m'
white='\033[0;37m'
reset='\033[0m'

# you can change these
lc="${reset}${bold}${blue}"         # labels
nc="${reset}${bold}${blue}"         # user and hostname
ic="${reset}"                       # info
c0="${reset}${blue}"                # first color

## OUTPUT

printf "
${c0}        /\\            ${nc}${USER}${ic}@${nc}${host}${reset}
${c0}       /  \\           ${lc}OS:        ${ic}${os}${reset}
${c0}      / /\\ \\  /\\      ${lc}KERNEL:    ${ic}${kernel}${reset}
${c0}     / /  \\ \\/  \\     ${lc}UPTIME:    ${ic}${uptime}${reset}
${c0}    / /    \\ \\/\\ \\    ${lc}PACKAGES:  ${ic}${packages}${reset}
${c0}   / / /|   \\ \\ \\ \\   ${lc}SHELL:     ${ic}${shell}${reset}
${c0}  /_/ /_|    \\_\\ \\_\\  ${lc}${uitype}:        ${ic}${ui}${reset}

"
