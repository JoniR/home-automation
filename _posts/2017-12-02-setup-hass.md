---
layout: post
title: "Setup Home Assistant server"
date: 2017-12-02 15:11:00
image: 'https://inventability.net/assets/pics/posts/tips/feature/hass.png'
description: Home Assistant docker installation to Ubuntu server
category: 'blog'
tags:
- jekyll
- wordpress
- blog
twitter_text: Home Assistant docker installation to Ubuntu server.
introduction: Home Assistant docker installation to Ubuntu server.
---
## Home Assistant

Docker installation is based on this blog: http://philhawthorne.com/installing-home-assistant-io-on-a-synology-diskstation-nas/

Home Assistant is running by docker and named as hass.

There is one volume /home/joni/docker/homeassistant/config which contain all configuration files

```bash
docker run --name hass --restart=always --net=host -itd -v /home/joni/docker/homeassistant/config:/config homeassistant/home-assistant
```

Updating is fairly easy by docker.
Just run script: 
```bash
sudo sh /home/joni/hass/update_hass_docker.sh
```
Script include following code:
```bash
#!/bin/bash
now=$(date +"%m_%d_%Y")
docker pull homeassistant/home-assistant && docker stop hass && docker update --restart=no hass && docker rename hass hass-old-$now && docker run --name hass --restart=always --net=host -itd -v /home/joni/docker/homeassistant/config:/config homeassistant/home-assistant
```