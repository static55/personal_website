---
header:
   image_fullwidth: "wallebanner.jpg"
layout: page
subheadline:  "Pi3, ROS, Arduino Mega, Android R/C controller"
title:  "Clipbot"
categories:
    - design
tags:
    - post format
gallery:
    - image_url: top_clipboard.jpg
      caption: Right-Click -> View Image to see larger.
    - image_url: lipo_battery.jpg
      caption: Lipo = tons of amps. No worries about voltage drops. But I Wouldn't want to accidentally short it with my finger.
    - image_url: lower_clipboard.jpg
      caption: 3 L298Ns
    - image_url: harness.jpg
      caption: One XT60 to multiple XT30s harness
    - image_url: motor_and_wheel.jpg
      caption: El cheapo motors from China.
    - image_url: tplink.jpg
      caption: TP-LINK TL-WR802N (accidentally bought the Chinese language firmware one -- saved like $2 though :P)
    - image_url: connector.jpg
      caption: Custom dupont wires :) 

---
<iframe src="https://player.vimeo.com/video/268830752" width="640" height="360" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe> <p><a href="https://vimeo.com/268830752">Clipbot clipboard robot with Raspberry Pi 3 and Ros</a> from <a href="https://vimeo.com/user84877905">Stewart Rap</a> on <a href="https://vimeo.com">Vimeo</a>.</p>

<h3>Hardware</h3>
The hardware is mostly common, inexpensive Chinese components. The mini-clipboards are from Walmart. L298Ns, XT-60 & XT-30 connectors. Adjustable DC step-down converter.

{% include gallery %}

I love XT-30 connectors. They're small, make a good electrical connection, and stay securely connected.<br>

I used M2 tapping screws to secure the electronic components to the clipboards.<br>

I made my own <b>quality</b> dupont wires to connect the motor controllers and the Arduino because dupont wires are generally flakey. I soldered header pins to wires and used shrink wrap and black nail polish to electically isolate them. I just soldered the other end to a pin on the motor controller.

I used a Lipo RC battery so that I could run the motors and electronics off the same battery. Safety is a concern due to the crazy amps that Lipos can put out. I power the robot with a 12 volt power supply while working on it.

<h3>3d Printed Parts</h3>
<br>
<img src="/images/clipbot_stls.png"><br>
I exported <a href="/assets/clipbot_stls/clipbotstls.zip">these .STL files</a> from Fusion 360 (Free for personal use). I imagine there's a way to convert them into another format or import them into some CAD software to made adjustments.

I used m3 machine screws to attach them.

<h3>ClipbotCtrl: Remote Control Android App</h3>
<br>
<img src="/images/clipbotctrl.jpg" align="left" style="padding-right:30px"> 
This app connects to the Pi3 on the robot with SSH and sends the joystick coordinates as XML X/Y coordinates.<br>
[ClipbotCtrl on GitHub ›](https://github.com/static55/ClipbotCtrl){: .t30 .button .radius}
<br clear="left">
<h3>clipbot_sshd: Clipbot's ssh server</h3>
<br>
This ROS project is a simple ssh daemon adapted from the sshd example bundled with libssh. It accepts connections from the above Android app and forwards the joystick input it receives to the Arduino as Twist messages via rosserial.<br>
[clipbot_sshd on GitHub ›](https://github.com/static55/clipbot_sshd){: .t30 .button .radius}
<h3>clipbot_arduino: The Arduino code</h3>
This Arduino code accepts Twist messages from clipbot_sshd and uses them to drive the motors.

The project uses the PlatformIO command line tools to compile and flash the Arduino but you should be able to copy/paste the code into the Arduino IDE.<br>
[clipbot_arduino on GitHub ›](https://github.com/static55/clipbot_arduino){: .t30 .button .radius}
