---
layout: post
title: "Pushover notification from rtorrent"
description: "Get Pushover notifications when your rtorrent torrents finish downloading"
category: 
tags: [rtorrent, Ruby, Pushover]
---
{% include JB/setup %}

A friend recommended [Pushover](https://pushover.net) today. It's a service 
which let you build applications, scripts or whatever that sends push notifications to your mobile devices.
My first experimentation with Pushover was to send a notification whenever a torrent finished downloading in rtorrent.
All in the name of automation! Here's what you need to do:

* Register for [Pushover](https://pushover.net), and download the app(s)
* Download and edit [this](https://gist.github.com/jsh0rty/4996785) script to suit your needs
* Put the following line in your rtorrent.rc file:

Code:

	system.method.set_key=event.download.finished,notificationscript,"execute={ruby,/Path/To/rtorrent-notification.rb,$d.get_name=}"


This will award you with a notification with the torrents name, pretty sweet!

