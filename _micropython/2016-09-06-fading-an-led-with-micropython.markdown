---
layout: post
title: "Fading an LED with Micropython"
permalink: /micropython/fading-an-led
redirect_from: /fading-an-led-with-micropython
date: 2016-09-06
---
<div class="video-container">
<iframe width="560" height="315" src="https://www.youtube.com/embed/GFwwPe4uO34" frameborder="0" allowfullscreen></iframe>
</div>

```python
import math
from time import sleep_ms
import machine

pin = machine.Pin(2, machine.Pin.OUT)
led = machine.PWM(pin, freq=1000)

def set_duty(l, d, t):
    l.duty(d)
    sleep_ms(t)

def pulse(l, t):
    for i in range(10):
        d = int(1023 - math.sin(i / 10 * math.pi) * 1023)
        set_duty(led, d, t)
    set_duty(led, 1023, t)

while True:
    pulse(led, 50)
    sleep_ms(500)
```
