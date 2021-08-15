# How To Make Your Own Pixel 2, Pixel 3 or Pixel 4 Debugging Cable

## Intro

Android allows for kernel debugging over the USB interface, but this requires a special cable called a debug cable. Unlike a standard USB cable or a Suzy Qable, a debugging cable allows for uart debugging via Serial TTL to retrieve the kernel logs. These debug cables have interfaces that regular USB-C cables do not have. Although Google does not sell these devices to the public, a debug cable may be created with a USB-C to USB-C breakout board, available on ELab Bay, and a USB to TTL Serial adapter cable available on Sparkfun. 

### Parts You Will Need

#### USB 3.1 CM CF USB 3.1 Male To Female Passthrough Breakout Board - Fully Soldered

https://elabbay.myshopify.com/products/usb3-1-cm-cf-v1a-usb3-1-type-c-male-to-female-pass-through-breakout-board?variant=45423178947

![Breakout Board](https://github.com/Peter-Easton/android-debug-cable-howto/blob/master/dbc-howto-breakoutboard.jpg)

The breakout board is available in three variants, which include an unsoldered version, a partially soldered, and a fully soldered version. In this tutorial, we will be using the Fully Soldered version, which has clamps that allow for the wires to be attached with the use of a screwdriver to tighten clamps already set on the board. This is the most straightforward and hassle-free method. 

#### USB To TTL Serial Cable 

https://www.sparkfun.com/products/12977

![USB to TTL Serial Cable](https://github.com/Peter-Easton/android-debug-cable-howto/blob/master/dbc-howto-ttlcable.jpg)

This cable contains the FT232 microcontroller chip, which is housed inside the USB-A connector. The Serial TTL cable is sometimes also used for debugging Raspberry Pis and other single board computers. 

### Optional Parts

This tutorial assumes you will want to create a permanent debugging cable which will only ever be used for debugging modern (at the time of writing) Android devices. If you wish to avoid cutting the USB to TTL Serial Cable and leave it in a way that allows you to readily and easily reconnect and disconnect it to and from the breakout board, you should consider ordering a package of finger wires. Male-to-male finger wires are available in a 30-pack at SparkFun:

https://www.sparkfun.com/products/11026

If you wish to use them, these wires would be in place of cutting the wires on the TTL Serial Cable. This will not be covered in this tutorial. 


### Tools and Consumables You Will Need

- Wire stripper, or a razor for stripping wires and cables
- Wire cutter
- A 1.4mm flat precision screwdriver
- Electrician's tape and scissors to cut it
- Superglue (optional, used only for sealing the end of the electrician's tape to prevent peel-off under tension.)
- USB C to USB A cable. 


### Software You Will Need

- Android Platform tools. Obsolete versions of Fastboot, which are often packaged with incorrect version numbering in official distro repositories are known to cause issues and may result in bricking. For your device's safety, you should obtain fastboot directly from google via the platform tools by running `wget https://dl.google.com/android/repository/platform-tools-latest-linux.zip` for Linux, or by visiting https://developer.android.com/studio/releases/platform tools for Windows or  MacOS. 
- Minicom. Minicom is officially packaged for virtually all major Linux distributions. Installing it on Debian or Ubuntu can be done with `apt install minicom` or on Fedora, by `dnf install minicom`.


## Assembling your Debugging Cable

### Preparing the USB to Serial TTL Cable
The USB to TTL Serial Cable has four wires in it: one black, one red, one yellow, and one orange. Each of them should end in a female finger connector. If you wish to reuse this cable in other applications, avoid cutting the Serial TTL cable, and instead proceed by cutting and stripping the finger wires in place of the Serial TTL cable's wires. 

Unless you plan to reuse the Serial TTL cable elsewhere, your best option is generally to simply snip the plugs off, then strip away the insulation to allow the wires to be inserted directly into the clamps. The clamps in the fully soldered version of the breakout board are very small, and you will only need about 3mm (1/8") of the exposed conductor to fit. This will leave the minimum amount of uninsulated wire on the outside. It may be easier to strip enough wire to get a decent hold on, then trim the excess. 

You may need to strip 2" or approximately 50mm of the outer cable jacket from the Serial TTL cable in order to leave yourself enough wiggle room to connect everything. This can be done with a disposable razor. Take care not to damage any of the smaller, finer wires beneath it.  

![Preparing your TTL Serial Cable](https://github.com/Peter-Easton/android-debug-cable-howto/blob/master/dbc-howto-cable-prepared.jpg)

### Attaching The Wires 
The wires need to be attached to specific locations. Fortunately, the underside of the breakout board is labelled with a specific number and letter code with a letter, and a number to represent each possible position on the breakout board. The sockets in the fully soldered breakout board have small screw clamps. Loosen them with a 1.4mm flat precision screwdriver to open the clamp, insert the wire, and tighten them back into place. Make sure not to over-tighten the screws. The wires should be snug and should not pull out when gently pulled on. 

* GND, the **Black** Wire, should be connected in position **A1**.
* RXD, the **Yellow** Wire, should be connected in position **A8**, on the same side as the black wire. 
* TXD, the **Orange** Wire, should be connected in position **B8**, on the opposite side. 
* VCC, the **Red** Wire, should be left alone. Tape it out of the way, or cut it off. 

### View from below

![From Below](https://github.com/Peter-Easton/android-debug-cable-howto/blob/master/dbc-howto-where-wires-go.jpg)

#### View from above

![From Above](https://github.com/Peter-Easton/android-debug-cable-howto/blob/master/dbc-howto-where-wires-go-above.jpg)


### Tidying up

If you plan to put it in a case, you can wind the wires between the oversized pins on the bottom of the breakout board to allow them to fit flush prior to taping. This is the easiest way. Once the wires are flush, simply start the tape on one side and wrap it around the entirety of the PCB until no more components remain exposed. You will need to wrap three layers, remaining careful not to stretch the tape too tightly on the first layer. Winding it too tightly may result in the pins on the bottom piercing the layers of the tape.

![Squishing the wires into place](https://github.com/Peter-Easton/android-debug-cable-howto/blob/master/dbc-howto-squishing-wires.jpg)

Cover the breakout board in electrician's tape.

![Wrapping it in tape](https://github.com/Peter-Easton/android-debug-cable-howto/blob/master/dbc-howto-taping-wrap.jpg)

The red wire can now should be safely tucked down and taped out of the way.

![Getting the red wire out of the way](https://github.com/Peter-Easton/android-debug-cable-howto/blob/master/dbc-howto-taping-up-red.jpg)

Electrician's tape, which is designed with the tactit assumption that it will only be wrapped around a wire and sheathed sometimes may peel and cause the corners to lift when applied to irregularly shaped objects, then pressed down under tension. If you want to make it a bit more permanent and have a cleaner appearance, you can apply a small bit of superglue onto it to keep the corners from lifting. 

![Finishing with superglue](https://github.com/Peter-Easton/android-debug-cable-howto/blob/master/dbc-howto-gluing-tape.jpg)

**WARNING:** *Do not use the debug cable if the breakout board has not been properly taped or placed in an insulating case. Doing so can result in the pins being crossed should the pins on breakout board contact something conductive, which could lead to undesired operation, or short circuiting.*

### Getting fancy

If you want to get a little fancier and don't like tape, I've been working on a 3D printed case for the PCB. This is at this moment, a work in progress and this version had some issues that I needed to fix with a dremel, so at this moment I won't be releasing these until I can work those problems back out, but this is an example of what you can do to get a little fancier. I originally planned to tie a knot in the cable in the large channel, but then realized I didn't give it enough room and so decided to glue it in place. The second version of the case I design won't have this void, and will just use a channel for glue. 

![Wiring the whole thing together](https://github.com/Peter-Easton/android-debug-cable-howto/blob/master/dbc-howto-with-case.jpg)

Final product, assembled and painted. I'm a tad bit out of practice with the paint, as you can tell! 

![Assembled and painted](https://github.com/Peter-Easton/android-debug-cable-howto/blob/master/dbc-howto-final-product.jpg)

## Using Your Debugging Cable

To obtain the kernel logs, you will need to unlock your bootloader. Visit "Unlocking the bootloader" in the installation guide at https://grapheneos.org/install#unlocking-the-bootloader for details on how to unlock your bootloader. 

**ATTENTION:** *Unlocking or re-locking the bootloader of your phone will immediately perform a factory reset, permanently erasing all the data stored on the SSD at the time. There is no undelete nor recovery from this state. Ensure you have backed up your data, such as contact lists, password manager databases, and backed up your One Time Password seeds or have other means to access your 2FA protected accounts. It cannot be recovered after the fact.*

**DANGER!** *Unlocking the bootloader will bypass all software integrity checks for as long as the bootloader remains unlocked. Never use any device with an unlocked bootloader for anything where you have any expectation of security and/or privacy. Locking your bootloader does not disable uart. If the bootloader is locked without first disabling uart, uart will remain enabled with the bootloader locked and allow uart debugging of the device. Always ensure you disable uart debugging and lock your bootloader again prior to using your phone for day-to-day applications again.*

Once the bootloader is unlocked, reboot your phone to the bootloader by first switching off the phone, then pressing and holding down the Power and Volume Down buttons on your phone until the fastboot screen appears. On Pixel 3s, the Fastboot screen has white text with the phone's status, and has "Fastboot" near the top. 

**WARNING:** *It is possible to gain root privileges through the debugging console.  Be sure to turn off uart debugging before locking the bootloader.*

Once you see the fastboot screen, Connect your cellphone to the debug cable via the breakout board. You will need to plug a USB-C cable into the breakout board, and plug both the USB and Serial to USB-C cables into the computer running adb. Once all the cables are plugged in, enable uart debugging in fastboot via the command on the computer with:  

`$ fastboot oem uart enable`

**ATTENTION:** *If fastboot hangs at* `<waiting for device>` *it may be because your udev rules are not set correctly or not set at all. Ensure your udev rules are set correctly to allow the computer to talk to the device at fastboot. An ugly, but effective workaround is to run the command as the root user.* 

If all goes well, fastboot will report "OKAY" and print the time taken to finish the command. Check to ensure that it worked by seeing if it created a new USB tty device with: 

`$ ls /dev/ttyUSB0 && echo "Looks like it's working."`

Connect to the virtual terminal with minicom. The command sequence is: 

`# sudo minicom --device /dev/ttyUSB0`

**ATTENTION:** *Prior to starting the phone, you should set your terminal emulator to have unlimited scrollback, as the phone may print more than 4000 lines of debugging information from simply booting the operating system. Otherwise, valuable debugging information may be lost from the scrollback.* 

Once you are ready, use the volume buttons on your phone to select through the Fastboot options to switch your phone on. You should see the kernel debug logs appear on minicom. To exit the minicom console, press `[CTRL + A]` to bring up the menu, followed by the `[x]` key to bring up the confirm exit menu. 

Note that your new debugging cable cannot be used for typical operations. While the Android operating system is online, it may connect to the USB interface only intermittently, constantly connecting and disconnecting the host.

To disable uart debugging, use

`$ fastboot oem uart disable`

Visit "Locking the bootloader" in the installation guide at https://grapheneos.org/install#locking-the-bootloader for details on how to re-lock your bootloader. 

**ATTENTION:** *Unlocking or re-locking the bootloader of your phone will immediately perform a factory reset, permanently erasing all the data stored on the SSD at the time. There is no undelete nor recovery from this state. Ensure you have backed up your data, such as contact lists, password manager databases, and backed up your One Time Password seeds or have other means to access your 2FA protected accounts. It cannot be recovered after the fact.*


## Troubleshooting 

#### "I see strange or unrecognizeable characters in minicom alongside the text. What gives?"

The serial interface is a low-quality analogue signal. From time to time interference may occur. You may be picking some of it up. If this is too much of an annoyance, you can try wrapping the entirety of the PCB and some of the cables in shielding copper mesh, tinfoil, and more electrician's tape. EM shielding at this moment is beyond the scope of this tutorial. 

#### "I'm not getting any display, or the display is an output of unrecognizeable gibberish."

Check to ensure your wiring is positioned correctly and that the cables are plugged into the phone with the top side of the breakout board facing in the same direction that the screen is. The debugging cable is directional and may not work correctly if plugged in upside-down. 

#### "Now that my phone is on and the operating system has booted, it constantly is reconnecting and dropping the connection to the USB even with both cables plugged in."

This has unfortunately been observed by multiple users with different cables and even happens to the commercially available Suzy Qable used for debugging ChromeOS or retrieving citadel logs. The debug cable is not used for anything except uart debugging.

#### "I lose the scrollback."

Set your terminal emulator to have an unlimited amount of scrollback. On xfce4, this may be done under Edit -> Preferences -> General -> Unlimited Scrollback.

#### "I would like a more durable case."

One is being designed, but isn't currently available at this moment. Please keep checking back, as a 3D printable design is in progress and will be made available soon.

 
