sys {
  $iif($1 == -e,n.echo normal -atg,say) OS: $n.osinfo  –  CPU: $n.cpuinfo  –  Memory usage: $+($dedll(usedphysicalmem),/,$dedll(totalphysicalmem)) MB ( $+ $dedll(memoryload) $+ )   –   Graphics: $dedll(videocard) ( $+ $replacecs($dedll(res),bpp,bit) $+ )
}
os {
  cuptime
  var %x = $n.osinfo
  $iif($1 == -e,n.echo normal -atg,say) os: %x $iif(xp isin %x,(installed on $gettok($dedll(installdate),2-,44) $+ ))   –   uptime: $dur($calc($ticks / 1000))
}
uptime {
  cuptime
  $iif($1 == -e,n.echo normal -atg,say) uptime: $dur($calc($ticks / 1000)) $iif($ticks < $ncfg(ruptime),  –   record: $dur($calc($ncfg(ruptime) / 1000)))
}
ip {
  if ($ip) $iif($1 == -e,n.echo normal -atg,say) ip: $ip
  else n.echo normal -atg no ip found
}
cuptime { 
  if (!$ncfg(ruptime)) { w_ncfg ruptime $ticks }
  if ($ticks > $ncfg(ruptime)) { w_ncfg ruptime $ticks } 
}
uptimefake say Win95 uptime: $r(3,51) $+ w $r(1,6) $+ d $r(1,23) $+ h $r(1,59) $+ s
wah say 8,9WAAA8,9A9,8AAAA8,9AAA9,8AAAAA8,9AAAA9,8AAAAA8,9AAAA9,8AAAAAAA8,9AAAAA9,8AAAA8,9AAAA9,8AAAAA8,9AAAA9,8AAAA8,9AAA9,8AAAA8,9AA9,8AAAA8,9AAAHH9,8HHHH8,9!!!!!!!!!!
:p say :PpPPppPPpPPppPppPPpPPpPPppPppPPpPPpPPppPppPPpPPpPPppPppPPpPPpPPppPppPPpPPpPPppPppPPpPPpPPppP
wee say 8,9WEEEE9,8EEEE8,9EEEE9,8EEEE8,9EEEE9,8EEEE8,9EEEE9,8EEEE8,9EEEE9,8EEEE8,9EEEE9,8EEEE8,9EEEE9,8EEEE8,9EEEE9,8EEEE8,9EEEE9,8EEEE8,9EEEE9,8EEEE8,9!!!!!!!!!!
bu say brain usage: 1% [4|||||||||]
mem $iif($1 == -e,n.echo normal -atg,say) memory usage: $+($dedll(usedphysicalmem),/,$dedll(totalphysicalmem)) MB ( $+ $dedll(memoryload) $+ )
cpu $iif($1 == -e,n.echo normal -atg,say) cpu: $n.cpuinfo
gfx $iif($1 == -e,n.echo normal -atg,say) graphics card: $dedll(videocard) ( $+ $replacecs($dedll(res),bpp,bit) $+ )
net $iif($1 == -e,n.echo normal -atg,say) nic: $dedll(conn)
snd $iif($1 == -e,n.echo normal -atg,say) sound card: $dedll(soundcard)
bw {
  var %d = $dedll(banddown), %u = $dedll(bandup)
  if (%u > 1023) var %u = $round($calc(%u /1024),2) MB/s
  else var %u = $round(%u,1) kB/s
  if (%d > 1023) var %d = $round($calc(%d /1024),2) MB/s
  else var %d = $round(%d,1) kB/s
  $iif($1 == -e,n.echo normal -atg,say) download: %d  –  upload: %u
}
whois2 do_whois $1
whois {
  if ($chr(42) isin $1) || ($chr(63) isin $1) do_whois $1
  else do_whois $1 $1
}
do_whois {
  if ($ncfg(whois) == @whois) { 
    set %w-dest @whois ( $+ $cid $+ )
    if (!$window(%w-dest)) {
      if ($ncfg(whois_inside) == 1)  window -k0n %w-dest 
      else window -k0dn %w-dest 200 200 600 200 nbs.ico
    }
    if ($ncfg(whois_inside) != 1) iline $color(info) %w-dest 1 $timestamp $pre waiting for reply $par($1)
    if ($appactive) && (!%whois.window.passive) window -a %w-dest
  }
  !whois $1-
}
hdd hd $1-
hd {
  ghds fixed
  $iif($1 == -e,echo -a $pre,say) free space: %thdf $+ / $+ %thds GB ( $+ $perc(%thdfree,%thdsize) $+ )
}
hdds hds $1-
hds {
  unset %?
  if (l isin $1-) var %labels = 1
  if (e isin $1-) var %hd.echo = 1
  if (m isin $1-) var %type = remote
  else var %type = fixed
  var %ii = 99
  while (%ii < 123) {
    if ($disk($chr(%ii)).type == %type) var % [ $+ [ $chr(%ii) ] ] $iif(%labels == 1 && $disk($chr(%ii)).label,( $+ $disk($chr(%ii)).label $+ )) $round($calc($calc($disk($chr(%ii)).free / 1024 / 1024) /1024),2) $+ / $+ $round($calc($calc($disk($chr(%ii)).size / 1024 / 1024) / 1024),2)
    inc %ii
  }
  var %ii = 99, %hdsay
  while (%ii < 123) { 
    var %tmp.v = $chr(37) $+ $chr(%ii)
    if ($eval(%tmp.v,2)) var %hdsay = %hdsay ( $+ $upper($right(%tmp.v,-1)) $+ :) $eval(%tmp.v,2)  - 
    inc %ii
  }
  ghds %type
  if (%thds > 1) $iif(%hd.echo == 1,n.echo normal -atg,say) free space: %hdsay (total: %thdf $+ / $+ %thds GB)
  else n.echo info -atg /hds: no %type drives found
}
ghds {
  if ($1) var %type = $1
  unset %thdfree %thdsize
  set %ii 99
  while (%ii < 123) {
    if ($disk($chr(%ii)).type == %type) inc %thdfree $disk($chr(%ii)).free
    inc %ii
  }
  set %ii 99
  while (%ii < 123) {
    if ($disk($chr(%ii)).type == %type) inc %thdsize $disk($chr(%ii)).size
    inc %ii
  }
  set %thdf $round($calc($calc(%thdfree /1024/1024) /1024),2)
  set %thds $round($calc($calc(%thdsize /1024/1024) /1024),2)
}
txt if ($exists($1)) { set %txt $1- | dlg txt }
setup dlg cp
popups dlg popups
about aboutnbs
aboutnbs dlg om
autocon dlg autocon
nq dlg np
quakenet dlg qnet
undernet dlg unet
misc gen
gen dlg misc
blist dlg blist
seekcw dlg pcw
prot dlg skydd
alarm dlg alarm
sa dlg mp3s
mp3say dlg mp3s
fkeys dlg fkeys
ch dlg cl
cns dlg ns
cmds dlg cmds
paste { set %paste.target $active | dlg paste }
gl g-join $1-
tedit {
  if ($1) set %tedit $1-
  else set %tedit $left($nopath($isalias(ttimestamp).fname),-4)
  dlg tedit
}
hevents {
  set %he.chan $1
  dlg hevent
}
caj { 
  if ($1) set %n.caj $1-
  else set %n.caj $network
  dlg aj
}
addedit {
  if ($1) set %addedit $1-
  dlg addedit
}
ren {
  say 1,1@@@@@@@@0,0@1,1@@0,0@1,1@
  say 1,1@@@@@@@@0,0@1,1@@0,0@1,1@
  say 1,1@@@@@@@@@0,0@@0,01,1@@
  say 1,1@@@@@@@@0,0@@@1,1@@
  say 1,1@@@@@@@@@0,0@@1,1@@
  say 1,1@@0,0@@@@@@@@@1,1@@
  say 1,1@0,0@@@@@@@@@@1,1@@
  say 1,1@0,0@@@@@@@@@@1,1@@
  say 1,1@0,0@1,1@0,0@1,1@@@@0,0@1,1@0,0@1,1@@
  say 1,1@0,0@1,1@0,0@1,1@@@@0,0@1,1@0,0@1,1@@
  say 1,1@0,0@1,1@0,0@1,1@@@@0,0@1,1@0,0@1,1@@
}
faq n.url http://www.nbs-irc.net/faq
