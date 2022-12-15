# wacca documentation

Info dump related to the hardware/firmware/etc of ワッカ

## disclaimer

Some information here is sourced from around the internet, of which I'm not sure if people wish to be credited for. You know who you are, let me know.

Many parts simply have not been extensively documented or are kept in private circles. My hope is that by making all of this information more accessible, someday more people will be able to enjoy this dead game. (asc when?)



## service manual

This PDF should be pretty easy to find online, there's also a shitty version that was fed through DEEPL to machine translate into english. This has a plethora of information that I won't directly post here since that's probably asking for a DMCA violation even for a dead game.

## Hardware

The anatomy of the cabinet an ALLS desktop connecting to a set of PCBs via two USB ports, two RS232 ports, two 3.5mm audio jacks, and digital video out to a 50 inch LCD (hdmi, displayport are supported WITH audio out). 

ALLS desktop RS232 1 --> PCB -->
ALLS desktop RS232 2 --> -->
ALLS desktop USB 1 -->
ALLS desktop USB 2 --> 


The desktop is a 
ALLS HX [849-0006]
Motherboard: Gigabyte MDH11BM [837-15384-02]
CPU: Intel Core i5-6500
RAM: 2x SK Hynix HMA851U6AFR6N-UH [4GB, DDR4-2133]
GPU: NVIDIA GeForce GTX 1050Ti [Aetina N1050TI-L9FX]
SSD: TDK GBDisk GS1 120GB [MDA-E0017]
Sound Card: Realtek ALC888S
OS: Windows 10 IoT LTSB 2016
PSU: 400W Seasonic 80 Bronze https://www.newegg.com/seasonic-ss-400et-bronze-400w/p/N82E16817151076 [from ALLX UX, i have 0 motiviation to open this PSU to confirm] 
RS232: 2 port + 1 port [Goes right to COM 1 COM 2 COM 3 on the motherboard]


Sound system
Subwoofer: S02012D0 4OHM 40W ????

Speakers: 2x 
Kitanihon Onkyo Co. S00308D0 
Drive Unit	77mm Paper cone full-range
Rated Impedance	4ohm
Nominal Power	10W
Maximum Power	15W
Frequency Range	200~20kHz
Sound Pressure Level	85dB
Dimensions(WxHxD)	120x90x97.5
Total Mass	605g

I believe these may work as a suitable replacement (at least it does for SDVX) https://www.crutchfield.com/S-nMsSvT4rfnE/p_108R6532EM/Infinity-Reference-REF-6532ex.html?omnews=17719017

## PCB Details

Power supplies:
LFA150F-12-J1 150W 12V 50-60Hz 12.5A IN AC100-240V
LFA150F-5-J1Y 150W 5V 50-60Hz 30A IN AC100-240V
These two units supply all the power needed for the PCB components (sound system, LEDs, touch controller etc).
My photos will look a little different at the bottom as we had to jerry rig an extension cable to feed power into the unit since I don't have the original cabling for it. Works fine on American power, theoretically works fine in europe without a transformer as well based on some reports. R1 uses a 300VA step down transformer https://cdn.discordapp.com/attachments/267603668046446603/1045057845999173692/IMG_20221123_112537805_HDR.jpg but that's probably overkill.

Touch Unit Control Board (PSS-7135-L02-01) - The most interesting part of the PCB. Custom part made by Pentel. Two of these exist on the PCB board that process 6 channels each, to get the 2 halves of the touch controller. Each segment of the touch controller has one of these as well, with the addition of the ribbon cable to connect the segments together. 

LED Data board (14-1497-R) - This sends the pretty colors to the touch controller and card reader panel?
2.1 channel AMP (14-1466CR) - Handles analog sound routing to subwoofer and tweeters

I/O Control Board (837-15257-01) - The existence of this board is a bit overkill for what it's used for, likely it *had* to be used due to Sega producing the cabinets for Marvelous. This is a newer version of the control board that has a USB port on it, almost all sega cabs use this now. Note: Wacca does NOT check for a coin counter, so the resistor trick is not needed to apply credits in game.

## Card reader panel "ASSY CTRL PNL"
This giant metal LED lined panel has [4] plugs that connect to
1) Aime card reader (610-0955). There's lots of good solutions to DIY one of these.
2) VFD Display to show IC readout for cash cards. Mine had some burn in. Unused?
3) Headphone amp jack with VOL UP and VOL DOWN buttons
4) All the LED data

The coin entry stuff connected to the cash box is here too.

## Touch Controller
There are 12 of these bad boys divided into two halves, set to channel 1-6 on each side that feed back into 2 touch unit control boards. Each one weighs x grams which totals to about 40 LBS. Somehow I never really understood how MASSIVE these units are until I held an individual segment in my hand. 

Here are some scans of a segment that shows the curve profile.


##Replacement LED PCBs
Wacca LEDs are notorious for being burnt out, you've likely received your machine in a state where some panels are not getting color data, are dim, or are straight up not lit up. This is partly due to the design of WS2812.

There's two good options for reproducing a better version
1) Isola has a WS2813 design which can be just popped into your touch controller without any issue (it will however, look brighter than the 2812's so consider a full swap) https://github.com/mnm-isola/wacca_ws2813
Note that at the time of writing, the most recent revision's gerbers are actually the previous revision. I would recommend downloading the project from https://github.com/mnm-isola/wacca_ws2813/tree/main/wacca_ws2813_rev20220814 and opening it in kicad and making your own gerber. Detailed instructions below.

2) Speedy labs is selling their revision of the PCB https://www.speedylabs.us/product/wacca-ws2813-led-pcb/ you'll need 60 of them to replace all your touch units. There is a europe equivalent vendor []

As a sidenote, it would be interesting to see someone make a APA102 variant of the LED PCBs on an ASC.

#Details on manufacturing your own LED PCBs
1) Clone Isola's repo or download the ZIP from the Code button https://github.com/mnm-isola/wacca_ws2813. wacca_ws2813_rev20221021 is the revision we want (the main difference is that the capacitor at C9 is SMD instead of THT. if you need THT, the previous August revision will do just fine)
2) Download KiCad https://www.kicad.org/download/
3) Open wacca_ws2813.kicab_pcb
4) File --> Fabrication Outputs --> Gerbers (.gbr). Set your output directory appropriately.
5) Click "Generate Drill Files..." and ensure that the drill units are in millimeters. Click "Generate Drill File" and "Generate Map File"
6) Click "Plot"
7) You should now have 13 files. Zip these (select all, right click, send to, compressed zip folder) and goto your favorite PCB manufacturer (i like JLCPCB). You need 60 PCBs to do a full replacement.
It should be as simple as uploading the zip, and clicking through and purchasing. I didn't change any of the default options except to make the PCB solder mask white.
It took a total 7 days for 200 PCBs to produce, ship, and arrive from China to California. YMMV. About $45 for the PCBs and $47 for shipping.

If someone has a cool wacca related silkscreen, please give. Maybe one of each navigator.

#Next steps
Now that your PCBs are fabricating, it's time to order the parts you'll need. 
https://www.lcsc.com/ is the recommended shop for these, they ship right out of shenzhen and it's quite quick, considering.

## BOM (for use with WS2813B-V5)

| Footprint | Parts                  | Size | Value  | LCSC    | Remark                                      |
| --------- | ---------------------- | ---- | ------ | ------- | --------------------------------------------|
| C1-C8     | Not Needed             | N/A  | N/A    | N/A     | WS2813B-V5 do not require decoupling caps   |
| C9        | Tantalum Capacitor     | 3216?| 22uF   | C782264 | Optional. 16V? (testing in progress)        |
| CN1,CN2   | JST XA 3 pin           |      |        | C265055 | B03B-XASK-1(LF)(SN)                         |
| CN3       | JST XA 4 pin           |      |        | C264994 | B04B-XASK-1(LF)(SN)                         |
| D1-D8     | Worldsemi WS2813B-V5   |      |        | C965558 |                                             |
| R1,R2     | 0805W8F1000T5E         | 0805 | 100R   | C17408  |                                             |
| U1,U2     | MMBD1503A              |      |        | C242273 |                                             |

So to do the math for you, to replace all of your lights, that's 60 PCBs you need.
60x  C782264 [these ship in multiples of 5]
120x C265055 [these ship in multiples of 10]
60x  C264994 [these ship in multiples of 10]
480x C965558 [these ship in multiples of 5]
120x C17408  [these ship in multiples of 100, you'll have 80 extra]
120x C242273 [these ship in multiples of 5]

The parts at the time of writing were $61.94 with $14.24 slower shipping from China to California

#Soldering it all together
If you're reading this, you probably know the basics on soldering and soldering SMD components.
If you're totally new to soldering, SMD might be a bit tricky. I'd suggest picking up an interesting keyboard project (like the corne) and studying lots of youtube videos on the matter.
Just remember to use solder with flux (kester 63/37 .031 inch leaded solder recommended), and to use a smoke absorber for your safety (Hakko FA400-04 recommended). When in doubt, flux flux flux.

One way to shave a lot of time off mass producing these PCBs is to order a stencil from https://www.oshstencils.com/
Upload the gerber zip, select the side that has all the LEDs as the top stencil (wacca_ws2813_f_paste.gtp), and make frameless stainless steel 5mil. Should cost about $50.
Get some solder paste and apply it to the PCB using the stencil, apply the SMD components, put it in a modified oven or on top of a modified clothes iron (or maybe you can use hot air at low flow)

## Other hardware

50 inch LED
I tried with a 55 inch and the circle size is not quite right. If you're using original hw, you'll need to be exactly 50 inch or get a TV with good overscan controls. I got a TCL 50S455 open box for $299.99 at bb. 

Network Router
For connecting to a private server you'll want 
- GL.iNet GL-AR750 (Creta)
- GL.iNet GL-AR750S (Slate)
- GL.iNet GL-MT300N-V2 (Mango)
or any router that supports OpenWrt 22.03

If you need wifi, Slate is the recommended one to go with. however, you *can* make mango's perform adequately with wifi on dedicated APs.



Total Power plugs needed: 4
ALLS, TV, PCB I/O, Network Router

## Working inside the ALLS
You can get away with using a phillips screwdriver but you really do risk stripping the screws used here. Notice how each of the screws look like phillips but have a dot? These are JIS screws! You'll want to purchase JIS screwdrivers to use.

The main interest in opening the ALLS is getting to the solid state drive that's inside. It's a bit of a pain but you don't have to disassemble too much of it to be able to get it out (I was able to strain the ATX connector a bit to unscrew the drive without tampering any cable ties).

To make this process much easier the second time around, it's recommended to either get a long SATA cable (???) or to get an enclosure that fits in the open PCI slot on the ALLS, this is the one people have used https://www.amazon.com/StarTech-com-2-5in-Removable-Drive-Expansion/dp/B002MWDRD6

## Imaging your ALLS drive
ALLS uses various tamper protections such as bitlocker, tpm, etc. that are provisioned from the factory. As such, you can't just stick in any drive and expect it to work, even with keychip. 
It's a very good idea to image your drive, so you can restore it and have it work, or to just have a 2nd drive handy.

Boot Linux through a USB drive (i recommend using Linux Mint and Rufus to create the bootable USB. plenty of guides on this)
Use DD to image the drive https://linuxhint.com/make-disk-images-dd-command-linux/

tl;dr
`sudo apt install lsscsi`
`lsscsi`
lists all the drives plugged in, look for your wacca drive (if you have some kind of complex setup, do the command prior to plugging in the drive and then after to discover which one)
`sudo fdisk /dev/sd<wacca-drive>`
we want to access the wacca drive. replace /dev/sd<wacca-drive> with whatever you saw in the previous step
`p`
This will list all the partitions on the drive and the exact sector count. Important to note them.
`q`
quits out of fdisk

`sudo dd if=/dev/sd<wacca-drive> of=/pathtostorage/wacca.img bs=100M conv=noerror`
Creates a clone image of the specified input `if` to the specified destination `of`

`ls -lh wacca.img`
Checks permission of the drive, should match the original
`fdisk -; wacca.img`
To compare the sector count, should match the original

then restore using
sudo dd if=<wacca.img> of=<newdrive> bs=100M conv=noerror

TODO: issues related to going to a larger drive?

# Other
USB capture cards can be used to stream Wacca. This will also show additional song stats on the parts of the screen that are otherwise not visible from the cab. This is the recommended one to use https://www.amazon.com/gp/product/B0BJ6XLK45 but anything 1080p60 is good, there's no EDID fuckery.

Gooseneck Phone mount thing
There's a little bracket on the top right of your machine that is designed for you to clamp a gooseneck phone mount onto to record gameplay. 
TODO: Update this with a recommended mount that has appropriate length etc.

Gloves. You will want to wear gloves to play the game because you *will* burn the skin on your fingertips from doing slides on the acrylic. Any cotton gloves are recommended, lots of people like the white gloves available at Daiso. Thick or thin gloves depending on your preference, I like thin but people want to feel less friction from the touch segments and so they go thick. If you wanna go full Wacca, the custom gloves made by marv are OEM these https://www.amazon.co.jp/-/en/gp/product/B0767CMNDQ/ https://www.amazon.co.jp/-/en/gp/product/B07DJ2KJ1S/ (these are thin, and won't last long)
TODO: Update which size gloves they are

Custom charts. A charter exists here: https://github.com/Goatgarien/BAKKA-Editor/ and custom song injection is fully working. Join their discord for more information.
