#! /bin/sh

pgrep -x sxhkd > /dev/null || sxhkd &
polybar example &
picom &
setxkbmap -option grp:alt_shift_toggle us,ru,ua

bspc monitor -d 1 2 3 4

bspc config border_width         2
bspc config window_gap          12

bspc config split_ratio          0.52
bspc config borderless_monocle   true
bspc config gapless_monocle      true

#bspc rule -a Gimp desktop='^8' state=floating follow=on
#bspc rule -a Chromium desktop='^2'
bspc rule -a telegram-desktop state=floating
#bspc rule -a Kupfer.py focus=on
#bspc rule -a Screenkey manage=off