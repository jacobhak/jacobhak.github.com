---
layout: post
title: "Python scripting with rtorrent"
description: "Solution to moving and sorting files downloaded with rtorrent"
category: 
tags: [Python,rtorrent,Plex,XBMC]
---
{% include JB/setup %}

I got some headache over some rtorrent scripting recently. I was trying to run a python script when rtorrent had finished downloading a torrent. There are a lot of threads on the web with help on this, but none covered what I was trying to do very well. I followed this [wiki entry](https://wiki.archlinux.org/index.php/RTorrent#Manage_completed_files)
and managed to come up with this line in my .rtorrent.rc:

	system.method.set_key=event.download.finished,my_script,"execute=python,~/code/myscript.py,$d.get_base_path="

but that just rewarded me with this helpful error message:

	Event 'event.download.finished' failed: Could not find '='.

I concluded that I had some kind of syntax error. The “$d.get_base_path=” part was supposed to give me the full path to the downloaded file (This was a guess from my part, as these commands are very poorly documented). That was supposed to be the first and only parameter to my python script. It was this line from the earlier mentioned wiki that got me thinking: 
>“... is the name of our script (or whatever command you want to execute) followed by a comma separated list of all the switches/arguments to be passed.” (referring to the equivalent of myscript.py)

 or rather, it got me confused. I fooled around for a while and ultimately I found something that acually worked! Behold:

	system.method.set_key=event.download.finished,my_script,"execute={python,~/code/my_script.py,$d.get_base_path=}"

PS. If any of you are interested in the actual script, it's available in this [gist](https://gist.github.com/jacobhak/4743181)
