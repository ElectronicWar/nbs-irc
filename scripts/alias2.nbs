f2 setup
f3 n.fkey F3
f4 n.fkey F4
f5 n.fkey F5
f6 if ($me ison %banchan) && (%banchan == $active) && (%banmode) && (%banmask) mode %banchan %banmode %banmask
f7 n.fkey F7
f8 n.fkey F8
f9 n.fkey F9
f10 n.fkey F10
f11 n.fkey F11
f12 n.fkey F12

cf1 cmds
cf2 if (%tmp.dnsresult) clipboard $ifmatch
cf5 {
  if (%rejointimer) { 
    .timer [ $+ [ %rejointimer ] ] off
    echo $color(info) -atg $pre rejoin aborted $par(%rejointimer)
  }
}
cf12 scon -a clearall | scon -at1 topicall
sf1 dll scripts\dll\winamp.dll prevsong
sf2 dll scripts\dll\winamp.dll playsong
sf3 dll scripts\dll\winamp.dll playpause
sf4 dll scripts\dll\winamp.dll stopsong
sf5 dll scripts\dll\winamp.dll nextsong

n.fkey {
  if (!$1) return
  if ($ncfg(fkey_ [ $+ [ $1 ] ])) && ($ifmatch != ânoneâ) $eval($ifmatch,2)
  else echo $color(other) -atg $pre Key $1 is unbound (use /fkeys to bind)
}
fkey n.fkey $1-
o {
  if ($n.qnet) {
    if (Q ison $active) { msg Q op $active }
    elseif (L ison $active) { msg L op $active } 
  }
}
g {
  if ($1) n.url http://www.google.com/search?q= $+ $replace($1-,$chr(32),$chr(37) $+ 20)
  else n.url http://www.google.com/
}
imdb {
  if ($1) n.url http://www.imdb.com/Find?for= $+ $replace($1-,$chr(32),$chr(37) $+ 20) $+ &select=All 
  else n.url http://www.imdb.com/
}
wiki {
  if ($1) n.url http://en.wikipedia.org/wiki/ $+ $replace($1-,$chr(32),$chr(37) $+ 20)
  else n.url http://en.wikipedia.org/
}
thott {
  if ($1) n.url http://www.thottbot.com/?s= $+ $replace($1-,$chr(32),$chr(37) $+ 20)
  else n.url http://www.thottbot.com/
}
allak {
  if ($1) n.url http://wow.allakhazam.com/search.html?q= $+ $replace($1-,$chr(32),$chr(37) $+ 20)
  else n.url http://wow.allakhazam.com/
}
wh {
  if ($1) n.url http://www.wowhead.com/?search= $+ $replace($1-,$chr(32),$chr(37) $+ 20)
  else n.url http://www.wowhead.com/
}
join {
  if ($numtok($1,44) < 2) && (-* !iswm $1) {
    if ($left($1,1) == $chr(35)) || ($left($1,1) == &) var %c = $1
    else var %c = $chr(35) $+ $1
    if (!$2) && ($chankey(%c)) join %c $v1
    else { 
      if ($2) set %pw. [ $+ [ %c ] ] $2
      !join %c $2
    }
  }
  else !join $1-
}
slap {
  if ($read(config\slaps.txt)) me $replace($read(config\slaps.txt),[nick],$$1)
  else me slaps $$1 around a bit with a large trout
}
op mode # + $+ $str(o,$modespl) $$1 $2-
dop mode # - $+ $str(o,$modespl) $$1 $2-
voice mode # + $+ $str(v,$modespl) $$1 $2-
dvoice mode # - $+ $str(v,$modespl) $$1 $2-
j join $$1-
q query $$1-
p part # $1-
n names #$$1
w whois $$1
ws whois2 $$1
qw if ($n.qnet) msg Q whois $$1
t topic $iif($chr(35) !isin $1,$active) $1-
wii !whois $$1 $1
k kick $$1 $2-
kick {
  var %r = $read(config\kicks.txt)
  if ($1 ischan) kick $1 $2 $iif(!$3,%r,$3-)
  else kick $active $1 $iif(!$2,%r,$2-)
}
q query $$1 $2-
send dcc send $$1 $2
chat dcc chat $$1
ping ctcp $$1 ping
