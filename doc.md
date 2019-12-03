This Christmas, I decided to see what I could do with all the Arduino
gear I have collected - after all, blinking lights and Christmas Trees
naturally go together!

I started with a bunch of RGB LEDS:

I have been using [the Adafruit Pixel](http://www.adafruit.com/products/322)-
based RGB LED strings as the
basis for my model train cTc work - each lamp is individually
addressable - the string of 50 RGB LED lamps is treated as a 50-element
shift register; the WS2801 LED controller chip latches the (R,G,B)
triple and manages the PWM and current control for each LED segment in
its lamp.

The [Seeed Grove LED Strip Driver](http://www.seeedstudio.com/depot/grove-led-strip-driver-p-1197.html?cPath=91_18)
also uses a WS2801, but adds a high current driver FET to each channel so it can drive a 5-meter RGB LED strip.

I wrapped the RGB strip around the Christmas tree trunk in a spiral,
connected it to the strip driver and plugged it into an Arduino by way
of a [Seeed Grove Shield](http://www.seeedstudio.com/depot/grove-base-shield-p-754.html?cPath=73).
Chained off the strip driver are two chains of Pixels, for a total of
101 RGB lamps.

The strip driver runs off of 12v at 1A or more (900 LEDs (300 each of
red, green and blue) at even a couple of mA each adds up!), while the
Pixels require 5VDC so the embedded driver chips don\'t blow. The
Arduino is happy with 5V, so I only needed two wall warts and a splitter
cable to power everything.

Thanks to [Pololu](http://github.com/pololu/pololu-led-strip-arduino), I
found a nice collection of RGB LED routines. The bad news is that they
were written for a TM1804/WS2812 driver chips; the good news is that it
was easy to rip out the chip specific routines and replace them with
[ones for the WS2801](http://www.seeedstudio.com/wiki/Grove_-_LED_Strip_Driver). With
100 lamps in the chain the update rate is only a few HZ, which makes
brightness changes easily visible - whether or not this is a bug or a
feature is still up in the air; I personally don\'t mind slowly changing
light patterns\...

One of the problems with a live (or, should I say, formerly live) tree
is that you need to keep water in the stand or it will dry out. My next
hack was to wire up a water sensor - esentially an analog input with a
1MegOhm pullup wired to a perf board next to a wire connected to ground:
The water \"resistance\" forms a voltage divider with the pullup
resistor which results in a fluctuating voltage on the A-to-D pin, with
\"dry\" probe (a higher resistance) resulting in a higher voltage than a
\"wet\" (lower resistance) one. When the wire sensor \"triggered\", the
code turns all the lights RED and leaves them that way as a reminder to
water the tree.

Another problem with a tree on a table is that little kids tend to get
too close and pull at the branches, lights and ornaments that they can
reach. As hosts, continually telling other parents to watch their kids
gets old pretty quickly - wouldn\'t it be nice if the tree itself could
alert them instead? I added a [Grove Ultrasonic ranger](http://www.seeedstudio.com/depot/grove-ultrasonic-ranger-p-960.html)
to the mix, with a triggered routine to flash the lights quickly between
full-on RED and full-on GREEN. Now, whenever anyone gets within a few
inches of the tree, everyone in the room notices!

Unfortunately, this blink-on-demand feature ended up attracting the kids; thankefully, they were appreciative and well behaved!

Next year, I\'m aiming for several more Pixel chains (or maybe some
higher speed TM1804/WS2812 chains), a better water sensor (this hack
suffers from wire corrosion/crud build-up that changes the range of
\"good\" readings over time) and different/more interesting
feedback-based light patterns (e.g., cheerlights or web usage analytics
or \...)

If you got this far, I hope you have a Merry Christmas, a happy New
Year, and an Arduino in a Fir tree!!!

