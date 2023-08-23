# Wacca documentation

Info dump related to the hardware/firmware/etc of ワッカ

## Table of contents
- [Wacca documentation](#wacca-documentation)
  - [Table of contents](#table-of-contents)
  - [Disclaimer](#disclaimer)
  - [Service manual](#service-manual)
- [Hardware](#hardware)
  - [USB/Serial Connections Breakdown](#usbserial-connections-breakdown)
  - [WACCA Serial Port Map](#wacca-serial-port-map)
  - [Desktop specifications](#desktop-specifications)
  - [Sound system](#sound-system)
  - [Television](#television)
  - [Power supplies](#power-supplies)
- [PCB Details](#pcb-details)
  - [Touch Unit Control Boards (PSS-7135-L02-01)](#touch-unit-control-boards-pss-7135-l02-01)
  - [LED Data board (14-1497-R)](#led-data-board-14-1497-r)
    - [Custom LED Driver](#custom-led-driver)
  - [2.1 channel AMP (14-1466CR)](#21-channel-amp-14-1466cr)
  - [Headphone AMP (00-1358AR)](#headphone-amp-00-1358ar)
  - [I/O Control Board (837-15257-01)](#io-control-board-837-15257-01)
  - [Card reader panel "ASSY CTRL PNL"](#card-reader-panel-assy-ctrl-pnl)
  - [Touch Controller \& Sensor array](#touch-controller--sensor-array)
- [Replacement LED PCBs](#replacement-led-pcbs)
  - [Details on manufacturing your own LED PCBs](#details-on-manufacturing-your-own-led-pcbs)
  - [BOM (for use with WS2813B-V5)](#bom-for-use-with-ws2813b-v5)
  - [Soldering it all together](#soldering-it-all-together)
  - [Replacing the board on the touch panel](#replacing-the-board-on-the-touch-panel)
- [Other](#other)
  - [Network Router](#network-router)
  - [Working inside the ALLS](#working-inside-the-alls)
  - [Imaging your ALLS drive](#imaging-your-alls-drive)
  - [USB capture cards](#usb-capture-cards)
  - [Gooseneck Phone mount thing](#gooseneck-phone-mount-thing)
  - [Gloves](#gloves)
  - [Custom charts](#custom-charts)
  - [Enabling front panel headphone jack on Fresh Windows Install](#enabling-front-panel-headphone-jack-on-fresh-windows-install)

</details>

## Disclaimer

Some information here is sourced from around the internet, of which I'm not sure if people wish to be credited for. You know who you are, let me know.

Many parts simply have not been extensively documented or are kept in private circles. My hope is that by making all of this information more accessible, someday more people will be able to enjoy this dead game. (asc when?)

## Service manual

This PDF should be pretty easy to find online, there's also a shitty version that was fed through DEEPL to machine translate into english. This has a plethora of information that I won't directly post here since that's probably asking for a DMCA violation even for a dead game.

---

<br>

# Hardware

![Wacca I/O board](https://github.com/jbamuro/waccamole/raw/main/img/DSC00811.JPG)

The anatomy of the cabinet an ALLS desktop connecting to a set of PCBs via two USB ports, three RS232 ports, two 3.5mm audio jacks, and digital video out to a 50 inch LCD (hdmi, displayport are supported WITH audio out).

You can find a list of various informations related to the wacca hardware below.

## USB/Serial Connections Breakdown

```text
ALLS desktop RS232 1 --> Left Pentel PCB --> Left half of the touch controller
ALLS desktop RS232 2 --> Right Pentel PCB --> Right half of the touch controller
ALLS desktop RS232 3 --> AIME reader

ALLS desktop USB 1 --> Sega IO
ALLS desktop USB 2 --> LED Data board
```

## WACCA Serial Port Map

```text
COM1: Aime Reader
COM2: AimePay VFD (the little unused display)
COM3: Console Touch (Right)
COM4: Console Touch (Left)
COM5: Keychip
COM6: Console Lights
```

## Desktop specifications

```text
ALLS HX [849-0006]
Motherboard: Gigabyte MDH11BM [837-15384-02]
CPU: Intel Core i5-6500
RAM: 2x SK Hynix HMA851U6AFR6N-UH [4GB, DDR4-2133]
GPU: NVIDIA GeForce GTX 1050Ti [Aetina N1050TI-L9FX]
SSD: TDK GBDisk GS1 120GB [MDA-E0017]
Sound Card: Realtek ALC888S
OS: Windows 10 IoT LTSB 2016
PSU: 400W Seasonic 80 Bronze https://www.newegg.com/seasonic-ss-400et-bronze-400w/p/N82E16817151076 [from ALLS UX, i have 0 motiviation to open this PSU to confirm] 
https://seasonic.com/et SS-400ET
RS232: 2 port + 1 port [Goes right to COM 1 COM 2 COM 3 on the motherboard]
```

## Sound system

```text
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
```

## Television

```text
Advanced Display Lab Inc.
6F, NO.257, SINHU 2nd Rd.,
NEI-HU DISTRICT, TAIPEI, TAIWAN

Rating: 100V~240V, 50/60Hz, 0.8~3A
Model: ADOF50NN03.0
P/N: 1001500-102002-32

InnoLux S500HJ1-LE8 Rev. C1
09C1L1293620075
https://www.panelook.com/S500HJ1-LE8_Innolux_50_LCM_overview_32625.html
```

## Power supplies

```text
LFA150F-12-J1 150W 12V 50-60Hz 12.5A IN AC100-240V
LFA150F-5-J1Y 150W 5V 50-60Hz 30A IN AC100-240V
```

![Power supplies](https://github.com/jbamuro/waccamole/raw/main/img/DSC00812.JPG)

These two units supply all the power needed for the PCB components (sound system, LEDs, touch controller etc).
My photos will look a little different at the bottom as we had to jerry rig an extension cable to feed power into the unit since I don't have the original cabling for it. Works fine on American power, there are also reports of it working fine in europe.

R1 uses a 300VA but that's probably overkill.

![step down transformer](https://cdn.discordapp.com/attachments/267603668046446603/1045057845999173692/IMG_20221123_112537805_HDR.jpg)

Hits about 200W during attract mode.
TODO: power info during songlist pull etc.

---

<br>

# PCB Details

## Touch Unit Control Boards (PSS-7135-L02-01)

There are two of these and they each process 6 segments. Together they control the two halves of the touch controller assembly (for a total of 12 segments).

![Master Touch Unit Control Board](https://github.com/jbamuro/waccamole/raw/main/img/DSC00814.JPG "Master Touch Unit Control Board for the 6 segments on the right of the touch assembly (Can be determined thanks to it's ID, currently set to 8. The controller ID for the left segments is 7)")

Each segment of the touch controller is connected to the others with the help of RS485 through a ribbon cable.
The PCBs present on each segment are the exact same with the addition of a custom Pentel IC and some extra components needed to drive the tactile sensor array.

![Pentel IC](https://github.com/jbamuro/waccamole/raw/main/img/DSC00835.JPG "The custom Pentel IC handling tactile input")

*Here's a detailed component list of those boards :*

| Component | Reference         | Comment  |
| --------- | ----------------- | -------- |
| IC1       | [FM3 MB9BF124K](https://www.infineon.com/dgdl/Infineon-CY9B120M_Series_32_Bit_Arm_Cortex_M3_FM3_Microcontroller-DataSheet-v10_00-EN.pdf?fileId=8ac78c8c7d0d8da4017d0edfa79064e9) | For pinouts see page 12 (LQFP-48) |
| IC2       | Pentel PAC-0815A | Custom capacitive touch controller made for Wacca by Pentel of Japan. |
| IC3       | [ADM 3101E](<https://www.analog.com/en/products/adm3101e.html#product-overview>)  | ±15 kV ESD Protected, 3.3 V Single-Channel RS-232 Line Driver/Receiver
| U5        | [7Lb176 (8BM AHP1)](https://pdf1.alldatasheet.com/datasheet-pdf/view/28214/TI/7LB176.html) | Differential Bus Tranceiver |
| U7 / U8   | [AD8616](https://www.mouser.com/ProductDetail/Analog-Devices/AD8616?qs=5aG0NVq1C4yTdSCFgWCNCg%3D%3D) | Analog Op Amps |
| CN4       | [Hirose HIF3BA](https://ie.rs-online.com/web/p/pcb-headers/8960809) | Used to connect all boards to each other using a ribbon |
| CN6       | 22 pin 1mm pitch FFC/FPC Connector | Generic part |
| SW1       | 9 Way binary coded rotary switch | Generic part |
| RG1       | XC6206 662K 3.3V 0.5A Voltage regulator | 3.3V 0.5A Voltage regulator |
| RG2       | [178M05 91 03](https://datasheetspdf.com/pdf-file/614024/HitachiSemiconductor/178M05/1) | 5V 0.5A Fixed Voltage regulator |

<details><summary>Click to show a Top View picture of the PCB</summary>

![Touch Unit Control Board](https://cdn.discordapp.com/attachments/568491469799817246/1143576271461302333/Top_View.jpg "Top view of the PCB")

</details>

<br>


## LED Data board (14-1497-R)

It sends the pretty colors to the touch controller.

![LED Data board](https://github.com/jbamuro/waccamole/raw/main/img/DSC00813.JPG "An LED Data board, connected to the ALLS using usb")

Here's a rundown of what this board is made out of :

| Component | Reference         | Comment  |
| --------- | ----------------- | -------- |
| IC1 | [FT232HL FTDI](https://ftdichip.com/wp-content/uploads/2020/07/DS_FT232H.pdf) | Single Channel HiSpeed USB to Multipurpose UART/FIFO IC |
| IC2 | [93LC56B](https://www.microchip.com/en-us/product/93lc56b) | EEPROM for USB descriptor and VID/PID, 6 pin variant  |
| IC3 | [SN74AHCT1G86](https://www.ti.com/lit/ds/symlink/sn74ahct1g86.pdf) | Single 2-Input XOR Gate |

```text
 Additional info:
IC3 Pin# 1 - MOSI from FT232HL (Pin 14)
IC3 Pin# 2 - trace runs to one pad of R10, through R11 (10k ohm resistor), to ground
IC3 Pin# 3 - Ground
IC3 Pin# 4 - LED data out into R12 (100 ohm resistor) to CN2 (LED Data/Ground out)
IC3 Pin# 5 - 5V, VCC in
```

### Custom LED Driver

If you want to make a custom LED Driver replacement, instructions, software and adapter link are below.

![Wacca LEDs](https://cdn.discordapp.com/attachments/568491469799817246/1144020876740808824/PXL_20230822_121850510.jpg "Look at how pretty this is ! (don't mind the weird LED strip on the right)")

The ftdi adapter we use is an [Adafruit FT232H](https://www.adafruit.com/product/2264) To flash it with the proper firmware you'll need the [FT_PROG EEPROM programmer](https://ftdichip.com/wp-content/uploads/2023/08/FT_Prog_v3.12.37.642-Installer.exe_.zip) software

The flashing instructions are as follows :

```text
Ensure the FTDI d2xx drivers are installed and the FT232H board is the only FTDI device connected to your computer (verify this by opening Device Manager and inspecting each device under the COM & LPT ports drop down if you're unsure).

Open FT_PROG and navigate to "DEVICES" > "Scan and Parse" you will see a new device populate in the device tree.

Click on the device in the tree and verify "Chip Type:" is 'FT232H' as this will be the Adafruit board.

Navigate to "USB String Descriptors" under the "FT EEPROM" section of the Device tree and change the "Product Description" field to "Single RS232-HS" and ensure the Serial Number field is blank, and the Serial Number Enabled box is unchecked.

Navigate to the "Driver" tab in the device tree under "Hardware Specific" > "Port A" and ensure "Virtual COM Port" is the checked option and D2XX Direct is not selected.

Right click the root Device in the device tree and click "Program Device"

Once the programming has been completed disconnect the USB cable and reconnect it.

Open your Windows Device Manager if it is not already and navigate to "USB Serial Converter" Under the "Universal Serial Bus Controllers" click Properties and navigate to the "Advanced" tab, ensure "Load VCP" is checked. Close the window and disconnect the USB cable and reconnect it.

Within the Device manager navigate to "USB Serial Port (COM*)" under "Ports (COM & LPT)" right click, select "Properties" > "Port Settings" > "Advanced" > "COM Port Number" and select "COM6" disconnect the USB cable and reconnect it.

Connect a wire to GND for LED Ground, and a wire to pin D1 for LED Data

Load the game and you should have LED activity disaplaying if everything is configured correctly.
```

## 2.1 channel AMP (14-1466CR)

![2.1 channel AMP](https://github.com/jbamuro/waccamole/raw/main/img/DSC00816.JPG "2.1 channel AMP (14-1466CR), Handles analog sound routing to subwoofer and tweeters")
Handles analog sound routing to subwoofer and tweeters

## Headphone AMP (00-1358AR)

![Headphone Amplifier](https://github.com/jbamuro/waccamole/raw/main/img/DSC00815.JPG "Headphone Amplifier (00-1358AR), Handles audio output to the control panel")
Handles audio output to the control panel

## I/O Control Board (837-15257-01)

![I/O Control Board](https://github.com/jbamuro/waccamole/raw/main/img/DSC00817.JPG)
 The existence of this board is a bit overkill for what it's used for, likely it *had* to be used due to Sega producing the cabinets for Marvelous. This is a newer version of the control board that has a USB port on it, almost all sega cabs use this now.

 *Note: Wacca does NOT check for a coin counter, so the resistor trick is not needed to apply credits in game.*

## Card reader panel "ASSY CTRL PNL"

This giant metal LED lined panel has [4] plugs that connect to

1) Aime card reader (610-0955). There's lots of good solutions to DIY one of these.
2) VFD Display to show IC readout for cash cards. Mine had some burn in. Unused?
3) Headphone amp jack with VOL UP and VOL DOWN buttons
4) All the LEDs

The coin entry stuff connected to the cash box is here too.

## Touch Controller & Sensor array

The touch controller assembly is composed of 12 segments divided into two halves (6 per side, each having their own main controller board). They each have an individual channel ranging from 1 to 6.

![Wacca touch segment](https://media.discordapp.net/attachments/568491469799817246/1143565017216733204/PXL_20230822_151822250.jpg "Three segments on my small table")

Each one of these weighs 1kg (2.2LBS) *(870g if the metal bracket is removed)* which totals to about 12kg (26LBS).


Each unit has 5 LED strips (each strip has 8 LEDs making for a total of 40 LEDs per segment). In total, there are 480 LEDs in the touch controller assembly

The sensor array is made out of 5 columns and 4 rows amounting to 20 touch zones par segment. All 12 segments amount to a total of 240 touch zones.
![Wacca sensor array](https://cdn.discordapp.com/attachments/568491469799817246/1143575566423969812/Wacca_Sensor_Flexible_PCB_Lowres.png "A segment's touch sensor array. There are 12 of these.")
Click [here](https://cdn.discordapp.com/attachments/297114097546297354/1068442545727746078/Wacca_Sensor_Flexible_PCB-1.png) to download a higher resolution image.

Somehow I never really understood how MASSIVE these units are until I held an individual segment in my hand.
![This shit is massive](https://media.discordapp.net/attachments/568491469799817246/1143563743557591070/PXL_20230822_151247219.jpg "")


Here are some scans of a segment that shows the curve profile.
<br><img src="https://github.com/jbamuro/waccamole/raw/main/img/concurve1.png" data-canonical-src="https://github.com/jbamuro/waccamole/raw/main/img/concurve1.png" width="150" height="150"/>
<img src="https://github.com/jbamuro/waccamole/raw/main/img/concurve2.png" data-canonical-src="https://github.com/jbamuro/waccamole/raw/main/img/concurve2.png" width="150" height="150"/>
<img src="https://github.com/jbamuro/waccamole/raw/main/img/concurve3.png" data-canonical-src="https://github.com/jbamuro/waccamole/raw/main/img/concurve3.png" width="150" height="150"/>

---

<br>

# Replacement LED PCBs

Wacca LEDs are notorious for being burnt out, you've likely received your machine in a state where some panels are not getting color data, are dim, or are straight up not lit up. This is partly due to the design of WS2812.

There's two good options for reproducing a better version

1) Isola has a WS2813 design which can be just popped into your touch controller without any issue (it will however, look brighter than the 2812's so consider a full swap) <https://github.com/mnm-isola/wacca_ws2813>
Note that at the time of writing, the most recent revision's gerbers are actually the previous revision. I would recommend downloading the project from <https://github.com/mnm-isola/wacca_ws2813/tree/main/wacca_ws2813_rev20220814> and opening it in kicad and making your own gerber. Detailed instructions below.

2) Speedy labs is selling their revision of the PCB <https://www.speedylabs.us/product/wacca-ws2813-led-pcb/> you'll need 60 of them to replace all your touch units. CensoredUsername is another source for the EU <https://docs.google.com/forms/d/e/1FAIpQLSfETDKtABUGxhhcBXFDWuHlz1cwHNNozOXztCPOOsENcN5KxA/viewform>

As a sidenote, it would be interesting to see someone make a APA102 variant of the LED PCBs on an ASC.

## Details on manufacturing your own LED PCBs

1) Clone Isola's repo or download the ZIP from the Code button <https://github.com/mnm-isola/wacca_ws2813>. wacca_ws2813_rev20221021 is the revision we want (the main difference is that the capacitor at C9 is SMD instead of THT. if you need THT, the previous August revision will do just fine)
2) Download KiCad <https://www.kicad.org/download/>
3) Open wacca_ws2813.kicab_pcb
4) File --> Fabrication Outputs --> Gerbers (.gbr). Set your output directory appropriately.
5) Click "Generate Drill Files..." and ensure that the drill units are in millimeters. Click "Generate Drill File" and "Generate Map File"
6) Click "Plot"
7) You should now have 13 files. Zip these (select all, right click, send to, compressed zip folder) and goto your favorite PCB manufacturer (i like JLCPCB). You need 60 PCBs to do a full replacement.
It should be as simple as uploading the zip, and clicking through and purchasing. I didn't change any of the default options except to make the PCB solder mask white.
It took a total 7 days for 200 PCBs to produce, ship, and arrive from China to California. YMMV. About $45 for the PCBs and $47 for shipping.

If someone has a cool wacca related silkscreen, please give. Maybe one of each navigator.

Now that your PCBs are fabricating, it's time to order the parts you'll need.
<https://www.lcsc.com/> is the recommended shop for these, they ship right out of shenzhen and it's quite quick, considering.

## BOM (for use with WS2813B-V5)

| Footprint | Parts                  | Size | Value  | LCSC    | Remark                                      |
| --------- | ---------------------- | ---- | ------ | ------- | --------------------------------------------|
| C1-C8     | Not Needed             | N/A  | N/A    | N/A     | WS2813B-V5 do not require decoupling caps   |
| C9        | Tantalum Capacitor     | 7343| 220uF   | [**C8024**](https://www.lcsc.com/product-detail/Tantalum-Capacitors_Kyocera-AVX-TAJD227K010RNJ_C8024.html) | Optional but adds protection. 10V.         |
| CN1,CN2   | JST XA 3 pin           |      |        | [**C265055**](https://www.lcsc.com/product-detail/Wire-To-Board-Wire-To-Wire-Connector_JST-Sales-America-B03B-XASK-1-LF-SN_C265055.html) | B03B-XASK-1(LF)(SN)                         |
| CN3       | JST XA 4 pin           |      |        | [**C264994**](https://www.lcsc.com/product-detail/Wire-To-Board-Wire-To-Wire-Connector_JST-Sales-America-B04B-XASK-1-LF-SN_C264994.html) | B04B-XASK-1(LF)(SN)                         |
| D1-D8     | Worldsemi WS2813B-V5   |      |        | [**C965558**](https://www.lcsc.com/product-detail/Light-Emitting-Diodes-LED_Worldsemi-WS2813B-V5_C965558.html) |                                             |
| R1,R2     | 0805W8F1000T5E         | 0805 | 100R   | [**C17408**](https://www.lcsc.com/product-detail/Chip-Resistor-Surface-Mount_UNI-ROYAL-Uniroyal-Elec-0805W8F1000T5E_C17408.html)  |                                             |
| U1,U2     | MMBD1503A              |      |        | [**C242273**](https://www.lcsc.com/product-detail/Diodes-General-Purpose_onsemi-MMBD1503A_C242273.html) |                                             |

So to do the math for you, to replace all of your lights, that's 60 PCBs you need.

```text
60x  C8024 [these ship in multiples of 1]
120x C265055 [these ship in multiples of 10]
60x  C264994 [these ship in multiples of 10]
480x C965558 [these ship in multiples of 5]
120x C17408  [these ship in multiples of 100, you'll have 80 extra]
120x C242273 [these ship in multiples of 5]
```

The parts at the time of writing were $61.94 with $14.24 slower shipping from China to California

## Soldering it all together

If you're reading this, you probably know the basics on soldering and soldering SMD components.
If you're totally new to soldering, SMD might be a bit tricky. I'd suggest picking up an interesting keyboard project (like the corne) and studying lots of youtube videos on the matter.
Just remember to use solder with flux (kester 63/37 .031 inch leaded solder recommended), and to use a smoke absorber for your safety (Hakko FA400-04 recommended). When in doubt, flux flux flux.

One way to shave a lot of time off mass producing these PCBs is to use solder paste and order a stencil from <https://www.oshstencils.com/>
Upload the gerber zip, select the side that has all the LEDs as the top stencil (wacca_ws2813_f_paste.gtp), and make frameless stainless steel 5mil. Should cost about $50. Ordering the jig accessory can help as well, but you can just use other PCBs to hold the position of the one you're squeegeeing.
Get some solder paste and apply it to the PCB using the stencil (spread over stencil and squeegee. if no stencil, careful syringing), apply the SMD components, put it in a modified oven or on top of a modified clothes iron (or maybe you can use hot air at low flow)

## Replacing the board on the touch panel

Remove the control panel with single screw on the left and right side.

![Control panel](https://cdn.discordapp.com/attachments/780283383069540393/1054935055333605457/PXL_20221221_013513863.jpg)

You don't need to remove the acrylic, just unplug the harnesses. Unplug, feed them up, slide the control panel out.

![Harnesses](https://cdn.discordapp.com/attachments/780283383069540393/1054948737845301338/PXL_20221221_022911966.jpg)

After you have the outside plastic pieces taken off, disconnect the led data only wires, LED power on the middle LED board, and the touch board cable.  Then remove the two outside screws for the panel and pull it straight out

![Metal bracket screws](https://cdn.discordapp.com/attachments/780283383069540393/1054930972799414382/image.png)

Remove the ribbon from the pentel touch pcb and unscrew and remove the pcb. You can try to get away with not removing the touch PCB by loosening the screws on the touch board enough to get clearance to pull the LED board out, but this is risky and not recommended.

Unscrew each LED PCB and pull them out

Place in the new PCB and screw everything back together

Tip: You can "grip" the ribbon to feed it back through the hole to get it back into the pcb by using painter's tape.
Be gentle here though, broken ribbons are no fun.

Note: You may need to remove the pop / marquee to get to the touch panels on the top of the machine. This may require security torx bits (not all cabs have security torx for some reason)

If the cab is powered on you will need to go to "connection test of touch devices " and "reconnect touch devices" in the test menu after re-connecting the touch board

Video instructions: <https://youtu.be/iyhxQFl7XyE>

---

<br>

# Other

## Network Router

For connecting to a private server you'll want one of the following

- GL.iNet GL-AR750 (Creta)
- GL.iNet GL-AR750S (Slate)
- GL.iNet GL-MT300N-V2 (Mango)

or any router that supports OpenWrt 22.03

If you need wifi, Slate is the recommended one to go with. however, you *can* make mango's perform adequately with wifi on dedicated APs.

The routers are powered via usb, so you can plug it into the ALLS. However, ALLS USB ports aren't always live, so startup will be a race condition between the game's network check & error and your router's boot/connection, particularly if you are on a Mango. It's best to plug it into wall power instead (also on wifi, you'll want more current).  If you're wired on creta/slate, you'll be fine off ALLS usb. Something to note, having the Creta reboot every so often helps them stay connected, probably because NAT connection state loss on (an) upstream router(s).

Total Power plugs needed if building from scratch: 4
ALLS, TV, PCB I/O, Network Router

On a real cab, it all feeds into a built in row of outlets (router has a power connector), and goes out 1 cord in the back. You'd still need to add your own wall wart for private server router, preferably.

## Working inside the ALLS

You can get away with using a phillips screwdriver but you really do risk stripping the screws used here. Noticed how each of the screws look like phillips but have a dot? These are JIS screws! You'll want to purchase JIS screwdrivers to use.

The main interest in opening the ALLS is getting to the solid state drive that's inside. It's a bit of a pain but you don't have to disassemble too much of it to be able to get it out (I was able to strain the ATX connector a bit to unscrew the drive without tampering any cable ties).

To make this process much easier the second time around, it's recommended to either get a long SATA cable and plug your drive somewhere more accessible or to get an enclosure that fits in the open PCI slot on the ALLS, this is the one people have used <https://www.amazon.com/StarTech-com-2-5in-Removable-Drive-Expansion/dp/B002MWDRD6>

## Imaging your ALLS drive

ALLS uses various tamper protections such as bitlocker, tpm, etc. that are provisioned from the factory. As such, you can't just stick in any drive and expect it to work, even with keychip.
Your drive contains your unique PCBID, so it's a very good idea to image your drive, so you can restore it and have it work, or to just have a 2nd drive handy.

Boot Linux through a USB drive (i recommend using Linux Mint and Rufus to create the bootable USB. plenty of guides on this). Do NOT use Windows, this can trigger bitlocker and your drive will get wiped.

Plug in an external drive if your boot USB drive isn't large enough to contain a 120gb image

Plug in your wacca drive via usb sata enclosure device. Any sata enclosure will work, these are 2.5" drives so they don't need more than USB to power them but the ac powered 3.5" / 2.5" enclosures will be fine too.

Use DD to image the drive <https://linuxhint.com/make-disk-images-dd-command-linux/>

<details><summary>Confused? Click here for a line by line tutorial of this procedure</summary>

Begin by installing lsscsi.

`sudo apt install lsscsi`

`lsscsi`

lists all the drives plugged in, look for your wacca drive (if you have some kind of complex setup, do the command prior to plugging in the drive and then after to discover which one)

`sudo fdisk /dev/sd<wacca-drive>`

we want to access the wacca drive. replace `/dev/sd<wacca-drive>` with whatever you saw in the previous step

  `p`

  This will list all the partitions on the drive and the exact sector count. Important to note them.

  `q`

  quits out of fdisk

  `sudo dd if=/dev/sd<wacca-drive> of=/pathtostorage/wacca.img bs=100M conv=noerror`

  Creates a clone image of the specified input `if` to the specified destination `of`

`ls -lh wacca.img`

  Checks permission of the drive, should match the original

  `fdisk -l wacca.img`

  To compare the sector count, should match the original

then restore using

  `sudo dd if=<wacca.img> of=<newdrive> bs=100M conv=noerror`

You'll want to restore on a 120gb or at most 240gb drive to be compatible with how a main storage format works at the moment. (but if you aren't doing that, any larger sized ssd can work)

UNKNOWN: expand the existing partition possible? would be good for the future of wacca+ / omnimix etc.
</details>

## USB capture cards

They can be used to stream Wacca.

This will also show additional song stats on the parts of the screen that are otherwise not visible from the cab. This is the recommended one to use <https://www.amazon.com/gp/product/B0BJ6XLK45> but anything 1080p60 is good, there's no EDID fuckery.

Burrito has a neat Wacca Lily R stream overlay, and a Reverse version is in the works with some nice move transitions.

## Gooseneck Phone mount thing

There's a little bracket on the top right of your machine that is designed for you to clamp a gooseneck phone mount onto to record gameplay.

TODO: Update this with a recommended mount that has appropriate length etc.

## Gloves

You will want to wear gloves to play the game because you *will* burn the skin on your fingertips from doing slides on the acrylic. Any cotton gloves are recommended, lots of people like the white gloves available at Daiso. Thick or thin gloves depending on your preference, I like thin but people want to feel less friction from the touch segments and so they go thick.

If you wanna go full Wacca, the custom gloves made by marv are OEM these :
<https://www.amazon.co.jp/-/en/gp/product/B0767CMNDQ/>
<https://www.amazon.co.jp/-/en/gp/product/B07DJ2KJ1S/>
(However do note that they are thin, and probably won't last long).

TODO: Upload the trace file of the glove's design

## Custom charts

A charter exists here: <https://github.com/Goatgarien/BAKKA-Editor/> and custom song injection is fully working. Join their discord for more information.

## Enabling front panel headphone jack on Fresh Windows Install

Download realtek audio driver from <https://www.gigabyte.com/Enterprise/Embedded-Computing/MDH11BM-rev-10#Support>

Open realtek manager

Remap ports based on sticker (front/rear)

Enable the Quadraphonic layout

<br><img src="https://github.com/jbamuro/waccamole/raw/main/img/realtek.png" data-canonical-src="https://github.com/jbamuro/waccamole/raw/main/img/realtek.png" width="371" height="1251"/> <br>
