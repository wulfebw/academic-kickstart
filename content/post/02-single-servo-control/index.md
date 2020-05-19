---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Single Servo Control"
subtitle: ""
summary: "Controlling a robotic arm with reinforcement learning 2: single servo control"
authors: []
tags: []
categories: [robotics]
date: 2018-02-09
lastmod: 2018-02-09
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
- Servos will control the joints of the robotic arm. In this post, we'll look at controlling a single servo using a HAT (hardware attached on top).

## Preview
<iframe width="560" height="315" src="https://www.youtube.com/embed/kY3lgvHtju8" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

## Materials 
- servo HAT
    + $22 on [amazon](https://www.amazon.com/gp/product/B00XW2OY5A/ref=oh_aui_detailpage_o01_s01?ie=UTF8&psc=1)
- HAT power source 
    + $8 on [amazon](https://www.amazon.com/gp/product/B00P5P6ZBS/ref=oh_aui_detailpage_o01_s00?ie=UTF8&psc=1)
- soldering kit 
    + $20 on [amazon](https://www.amazon.com/gp/product/B06XZ31W3M/ref=oh_aui_detailpage_o00_s00?ie=UTF8&psc=1)
- small test servos 
    + $7 on [amazon](https://www.amazon.com/gp/product/B013UI9MVG/ref=oh_aui_detailpage_o09_s01?ie=UTF8&psc=1)
- total cost: $57 + cost of previous materials 
    + cost so far: $147 + cost of common materials

## Background 

### How do servos work?
- They have a motor. You send a signal to the motor, and the length of the signal indicates the desired position of the motor
    + [Servo primer](https://learn.sparkfun.com/tutorials/hobby-servo-tutorial)
- [Pulse width modulation (PWM)](https://en.wikipedia.org/wiki/Pulse-width_modulation) is used in sending the signal
    + PWM resources:
        * [Adafruit description](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-8-using-a-servo-motor/servo-motors)

### Why do we need the servo HAT?
- The pi has the ability to send PWM signals, but there are two problems 
    1. servos draw enough power that operating them can interfere with the pi operations
    2. the pi only has a single PWM pin, which means it can only control one servo
- The servo HAT allows for controlling many servos at once, and also uses an external power supply to avoid interfering with the pi

## Walkthrough

### Servo HAT hardware setup
- Solder the pins into the servo HAT then attach the HAT to the pi as in the following picture
![A connected HAT](assembled.jpg)
- Attach the servo to the first set of 3 pins
- Power on the pi and servo HAT

### Servo HAT software setup
- Download the software library that comes with the servo HAT as described in this [tutorial](https://learn.adafruit.com/adafruit-16-channel-pwm-servo-hat-for-raspberry-pi/using-the-python-library)
- Add the downloaded library to PYTHONPATH in your raspberry pi bash_profile
    + ```export PYTHONPATH="/home/pi/software/Adafruit-Raspberry-Pi-Python-Code/Adafruit_PWM_Servo_Driver:$PYTHONPATH"```
        * where `software` is the directory where I downloaded the software
- Since these programs are run with the super user, and running with super user erases the PYTHONPATH by default, we need to explicitly keep the PYTHONPATH when running as super user 
    + ```sudo visudo -f /etc/sudoers.d/custom```
        * this creates a custom file rather than directly editing sudoers 
        * by default this uses nano to edit the file
    + add ```Defaults env_keep += "PYTHONPATH"``` to the file and exit

### Running the tutorial demo 
- Download the additional [code](https://github.com/wulfebw/robotics_rl/blob/master/tutorials/2_single_servo.py) used to control the servo 
    + this is in the same github repo as the code from the previous tutorial
    + it contains a utility function that allows for controlling the servo based on the desired angle of the servo arm rather than with pulse widths
- Run the tutorial demo
    + ```sudo python 2_single_servo.py```

## Result
<iframe width="560" height="315" src="https://www.youtube.com/embed/kY3lgvHtju8" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
