1491130326291
DIY 3D printer with CD Roms build
Today is last day of Nowruz holidays in Iran.

## Having Fun?

I didn't write much code in holidays. I've decided to spend more family time in holidays and have some fun.
But as you can guess, i could't resist the [``Cheap 3D printer``](http://www.instructables.com/id/Super-Cheap-3D-Printer-From-CD-Rom-Drives/) Project. It was so damn fun :D

## What did you do?

I've successfully competed the build. (Yayyyyy!)
The X, Y and Z axis are good. the platform is fair. Extruder is a bit weak! and the Hotend Rocks!
Im Using an Arduino UNO as controller with grbl 1.1f (Which is a CNC controller software for atmega32)

## What can it do?

grbl supports G-Code but grbl doesn't know about Extruder and Hotend temperatures. It only knows spindle and its direction.

Sure you can use spindle enable as extruder controller BUT the tricky part is slicers does not know spindle G-Code. So i had to design a script that translate Reprap flavor G-Code into grbl G-Code. It still needs some work.

But Currently i can do fallow paths on my printer with help of [MakerCam.com](http://makercam.com)
I have done stars, hand, rocket, and eiffel tower.

![3D printed objects](https://preview.ibb.co/dHtska/IMG_2803.jpg)

## Build size?

It is roughly 35x35x35mm

## Extruder and hot end?

I have used a 3D printing pen as hotend and extruder. I have completely removed pen's circuit, connected the hotend to the power supply and the extruder to arduino PWM pin of grbl (D11)

## Matterial?

The pen came with it's own 1.75mm ABS filament.

## What about the housing?

Uh... Due to small build size i cannot print NanoPi housing with it. NanoPi NEO has dimensions of 40x40x40mm.

But i'm planning on building a bigger Reprap printer without the kit. If i can finish my works i may be able to do that.

## Wasn't it a waste of your time?

Absolutely not! I've learned so many things with this project and this is really the important part. learning everyday and having fun. it was a lot of fun finishing this project as i didn't think i could do that at the very begining.

If you are interested in building this you can click [__HERE__](http://www.instructables.com/id/Super-Cheap-3D-Printer-From-CD-Rom-Drives/) for instructions

Thank you for reading this

T{:okT, :lets_3d_print!}T
