---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "LED Control"
subtitle: ""
summary: "Controlling a robotic arm with reinforcement learning 1: led control"
authors: []
tags: []
categories: [robotics]
date: 2018-02-04
lastmod: 2018-02-04
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: true

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

## Outline 
- We'll make a LED blink in this post. Gotta start somewhere.

## Preview
<iframe width="560" height="315" src="https://www.youtube.com/embed/9AAlkAnyxGc?ecver=1" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

## Materials 
- Raspberry Pi 
    + For example through CanaKit
    + $70 on [amazon](https://www.amazon.com/CanaKit-Raspberry-Complete-Starter-Kit/dp/B01C6Q2GSY/ref=sr_1_1?s=electronics&ie=UTF8&qid=1517689480&sr=1-1&keywords=CanaKit+Raspberry+Pi+3+Complete+Starter+Kit+-+32+GB+Edition)
- electric cables
    + $7 on [amazon](https://www.amazon.com/gp/product/B01LZF1ZSZ/ref=oh_aui_detailpage_o08_s00?ie=UTF8&psc=1)
    + There are probably cheaper options 
- electronics start kit
    + $13 on [amazon](https://www.amazon.com/gp/product/B01ERP6WL4/ref=oh_aui_detailpage_o08_s00?ie=UTF8&psc=1)
    + There are definitely cheaper options
    + For this tutorial, we're just using an LED, a 1k resistor, and a breadboard
- commonly available materials 
    + keyboard
    + mouse 
    + monitor
    + hdmi-to-hdmi cable to connect raspberry pi to monitor
- total cost: $90 + cost of common materials

## Walkthrough
- set up the raspberry pi 
    + see canakit [instructions](https://www.canakit.com/quick-start/pi)
- set up raspberry pi wifi connection and ssh
    + connect pi to monitor, mouse, keyboard
    + follow these [instructions](https://www.raspberrypi.org/documentation/remote-access/ssh/) to set up ssh
        * ```hostname -I``` to get ip address
        * `ssh pi@<ip address>`
            - from your other computer
        * default password is `raspberry`
- set up raspberry pi with LED 
    + see Raspberry Pi Cookbook instructions [tutorial](http://razzpisampler.oreilly.com/ch03.html#SEC7.1)
    + download my version of the [code](https://github.com/wulfebw/robotics_rl/blob/master/tutorials/1_led.py)
        * run ```sudo python 1_led.py``` from cmd line

## Result
<iframe width="560" height="315" src="https://www.youtube.com/embed/9AAlkAnyxGc?ecver=1" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
