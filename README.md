Chip used :- STM32WB55CEU6.

Important Online Note :-
<https://www.st.com/resource/en/application_note/an5165-how-to-develop-rf-hardware-using-stm32wb-microcontrollers-stmicroelectronics.pdf>

![A diagram of a circuit board AI-generated content may be
incorrect.](images/media/image1.png)This is the reference :-

Use STM32CubeIDE to get more information about the Chip :-

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image2.png)

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image3.png)Here I have enabled I2C on PB8 and PB9
corresponding to Pin 5 and 6 respectively.

In Kicad, import the board STM32WB55CEUX.

Ground the Pins VSS5MP5, VSSRF and VSS.

![A screen shot of a computer AI-generated content may be
incorrect.](images/media/image4.png)

As illustrated on the reference manual, the Pin VDDUSB, VDDA, VDD, VDD,
VDD and VBAT are connected to 3.3V power supply through bigger capacitor
(4.67uF) and smaller capacitors (100nF : local supply).

![A screen shot of a graph AI-generated content may be
incorrect.](images/media/image5.png)

For VDDRF, connect it to 100nF capacitor along with power supply

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image6.png)

We need Stepdown converter to step down voltage for lower voltage. For 8
MHz we use 2.2uH inductor and for 4MHz we use 10uF inductor. SMPSLX --
Switch Mode Power Supply

SMPSFB -- Switch Power Supply Feed Back

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image7.png)

The low frequency oscillator(Crystal) is connected to Pin 2 and 3.

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image8.png)

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image9.png)The high frequency
oscillator(Crystal_GND24) are connected to Pin 24 and 25.

We can add resistor in HSC_IN to increase the longevity of oscillator.

![A diagram of a circuit AI-generated content may be
incorrect.](images/media/image10.png)RF Section:-

We need low pass filter for 2.4GHz and 5GHz.

For that we need to create a footprint and symbol of DLF162500LT-5028A1.

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image11.png)From File, Add library\> DLF162500LT-5028A1

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image12.png)Go to the Pin table and add pins.

Use the rectangle tool on the right side to draw the rectangle touching
the pins.![A screen shot of a computer AI-generated content may be
incorrect.](images/media/image13.png)

Use the Text "T" tool to add the text label "2.4GHz- 2.5GHz".

Save the symbol. Now it's time to create the physical footprint of the
symbol.

Use this footprint editor to create the new footprint.![A screenshot of
a computer AI-generated content may be
incorrect.](images/media/image14.png)

Go to file \> Add library and name your library.

Here the newly added library is STM32_RF_LowPassFilterFootPrint

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image15.png)

In the new library, add new Footprint and name it as Component name eg.
"DLF162500LT-5028A1"

This is the dimension of
[footprint](https://product.tdk.com/system/files/dam/doc/product/rf/rf/filter/catalog/rf_lpf_dlf162500lt-5028a1_en.pdf).

![A blueprint of a diagram AI-generated content may be
incorrect.](images/media/image16.png)

![A screenshot of a phone AI-generated content may be
incorrect.](images/media/image17.png)Add pad from here.

According to the dimension, the centre of origin:-

X : ½ ( 0.275 + 0.45) + 0.25 = 0.6125.

Y : ½ (0.245 +0.21) = 0.2275

This is the position and dimensions of pad1 :-

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image18.png)

This is the position and dimensions of pad 3:-

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image19.png)

This is the position and dimensions of pad 2:-

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image20.png)

This is the position and dimensions of pad 4:-

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image21.png)

Download 3D Model of symbol from ![A screenshot of a computer
AI-generated content may be
incorrect.](images/media/image22.png)ultralibrarian in .step format.

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image23.png)In Kicad go to footprint properties and
add the 3d model. Our pad aligns with physical pins.

![A screen shot of a computer AI-generated content may be
incorrect.](images/media/image24.png)With silkscreen layer selected, click
circle tool to add indicator for pin 1.

Using the symbol editor, assign newly created footprint to the symbol we
just created.

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image25.png)

Place newly created symbol to the schematic and connect to pin 1.![A
diagram of a circuit AI-generated content may be
incorrect.](images/media/image26.png)

Add a Co-Axial connector.

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image27.png)

![A computer diagram of a circuit board AI-generated content may be
incorrect.](images/media/image28.png)This is our current progress.

Now, we need to add the programming interface.

The PA 13, PA 14 and PA3 can be used to program and debug the board.
Along with those pins NRST has to be low (0) for programming mode and
high (1) on normal mode.

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image29.png)

Connect the tag connector "Conn_ARM_SWD_TagConnect_TC2030". Connect the
tag connector to respective pin as shown. For NRST( Reset) pin connect
it through 100nF capacitor at Pin 7.

![A diagram of a circuit board AI-generated content may be
incorrect.](images/media/image30.png)

PH3 is bootload pin and should 0 be on bootload. When the pin Switch is
not pressed, the PH3 is grounded but on pressed, the connection acts as
lowpass RC filter.

![A diagram of a circuit AI-generated content may be
incorrect.](images/media/image31.png)

Add USB "USB_C_Receptacle_USB2.0_16P" and we are going to use pin 37 and
38.

![A computer screen shot of a circuit board AI-generated content may be
incorrect.](images/media/image32.png)

Add a USB protector between the USB Connector and Pins.

![A diagram of a circuit board AI-generated content may be
incorrect.](images/media/image33.png)

The D- pins and D+ pins are connected each other and then to Pins 1 and
3 respectively on the USB protector. The VBUS is connected to Pin 5. Pin
6 and 4 are connected to Pin 37 and 37 respectively on the STM32
Microcontroller.

The pull down resistors are tied on the Pin A5 and B5.

Convert 5V of VBUS to 3.3V using LDO voltage regulator.

Search LDO voltage regulator by putting requirement on mouser. Add a
voltage regulator "MIC5365-3.3YD5" to get 3.3V output.

![A computer circuit board with many wires AI-generated content may be
incorrect.](images/media/image34.png)

![A diagram of a circuit AI-generated content may be
incorrect.](images/media/image35.png)Add a Peripheral connection on PA2 and PA2
using Generic 01\*04 Connector.

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image36.png)Use PA7 for PWM Output signal generation.

Add LED to Pin 16 (PA7) and add current limiting 220 Ohm resistor.

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image37.png)

![A computer diagram of a circuit board AI-generated content may be
incorrect.](images/media/image38.png)Overall schematic :-

![A computer screen shot of a computer program AI-generated content may
be incorrect.](images/media/image39.png)Run electric rule checker and make sure all
wirings are correct.

Add footprint to the capacitor.

![](images/media/image40.png)

Add footprint to all the components.

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image41.png)

Create Bill of Materials for all the components.

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image42.png)

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image43.png)Add netclass to group the components.

Setup layers

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image44.png)

Select 4 layers and impedance controlled

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image45.png)

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image46.png)Select these layer width

Lead free copper

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image47.png)

Solder Mask

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image48.png)

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image49.png)Fill in these board capabilities and
requirements

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image50.png)Board rule

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image51.png)These tracks are calculated on 50 ohm
impedance.

Press Ok

Multi layer PCB![A diagram of a layer of copper layer AI-generated
content may be
incorrect.](images/media/image52.png)

Press F8 to apply the footprints

![A computer screen shot of a computer AI-generated content may be
incorrect.](images/media/image53.png)This is the current 3D view:-

Update the 3D Model STEP file for J2 connector downloaded from
[MOLEX](https://www.molex.com/en-us/products/part-detail/530480410).

![A computer screen shot of a computer AI-generated content may be
incorrect.](images/media/image54.png)

Add 3D model for STM32 from
[here](https://gitlab.com/kicad/libraries/kicad-packages3D/-/blob/5.1.10/Package_DFN_QFN.3dshapes/QFN-48-1EP_7x7mm_P0.5mm_EP5.6x5.6mm.step)

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image55.png)

3d model can be downloaded from here:-

> 3D content central
>
> Grabcad

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image56.png)Select blue color for SWD routing

Select net colors to blue for all

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image57.png)Do the same all others

Create a layout

Select 1 mmm grid

![A machine with colorful lights AI-generated content may be
incorrect.](images/media/image58.png)Move the chip by moving around with M.

Move critical section first like RF, USB connector close to
microcontroller. Also keep crystal and power close to microcontroller.

Debug,BOOT0 , Reset, TX and RX are less critical. BI coupling capacitor
needs to be close .

![A computer screen shot of a computer chip AI-generated content may be
incorrect.](images/media/image59.png)Keep Connector to left of IC.

Place USB connector to left of tag connector and rotate as indicated.

![A computer screen shot of a computer chip AI-generated content may be
incorrect.](images/media/image60.png)

![A computer screen shot of a computer AI-generated content may be
incorrect.](images/media/image61.png)Place RF connector to right of IC and place
filter in between the IC and connector.

Place the crystal as indicated.

![A computer chip with many colors AI-generated content may be
incorrect.](images/media/image62.png)

![A computer screen shot of a computer chip AI-generated content may be
incorrect.](images/media/image63.png)Place the L1, L2 and C14 to top of IC for
now

Place UART connector and resistor to bottom of IC.

![A computer chip with many different colors AI-generated content may be
incorrect.](images/media/image64.png)

![A computer screen shot of a computer AI-generated content may be
incorrect.](images/media/image65.png)Place USB protector as shown

Place the RF components as shown

![A screenshot of a video game AI-generated content may be
incorrect.](images/media/image66.png)

![A computer chip with many different components AI-generated content
may be incorrect.](images/media/image67.png)This is the current 3D view

Place capacitor to crystal oscillator

![A computer screen shot of a computer AI-generated content may be
incorrect.](images/media/image68.png)

![A computer screen shot of a computer AI-generated content may be
incorrect.](images/media/image69.png)Finetune this SMP power supply layout.

Place RF decoupling capacitor close to Pad 23

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image70.png)

Place another capacitor for pin 20

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image71.png)

Place capacitor like this near pin 40 to make room to route trace for
Serial DIO

![A computer chip with numbers and symbols AI-generated content may be
incorrect.](images/media/image72.png)

Place decoupling capacitor for pin 34 and 35

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image73.png)

![A computer chip with many different colored lights AI-generated
content may be
incorrect.](images/media/image74.png)Re arrange this section

Make a room for reset pin

![A computer chip with many different colored lights AI-generated
content may be
incorrect.](images/media/image75.png)

![A computer screen shot of a computer chip AI-generated content may be
incorrect.](images/media/image76.png)Move SMP close to microcontroller but put crystal
away

![A screenshot of a video game AI-generated content may be
incorrect.](images/media/image77.png)Place LDO 3.3V regulator as shown

Place resistors around USB C connector

![A computer screen shot of a computer AI-generated content may be
incorrect.](images/media/image78.png)

Place reset capacitor C13

![A computer chip with many different colors AI-generated content may be
incorrect.](images/media/image79.png)

Place the switch and resistors around the switch

![A computer screen shot of a computer AI-generated content may be
incorrect.](images/media/image80.png)

![A computer chip with many different components AI-generated content
may be incorrect.](images/media/image81.png)This is the current 3D layout of the board

![A computer screen shot of a computer program AI-generated content may
be incorrect.](images/media/image82.png)Define board out line. Select Edge.cuts
layer. Select line tool and draw the line.

You can also use the arc tool to draw the arc around the edge of the
board

![A screen shot of a computer AI-generated content may be
incorrect.](images/media/image83.png)

Start routing with most critical component. We can use top layer for
power and bottom layer for ground.

Signal -- GND -GND -Signal ( 4 layers) GNB Layer in Inner 1 and Inner 2

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image84.png)Select In1.Cu. Add a GND Layer and adjust
the electrical properties.

Draw outline of the board. Select B to fill the board.

![A computer screen shot of a circuit board AI-generated content may be
incorrect.](images/media/image85.png)

Add a mounting hole with this footprint.\
![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image86.png)

Add fiducial marker to automate assembly.

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image87.png)

![A computer screen shot of a computer AI-generated content may be
incorrect.](images/media/image88.png)Place the mounting hole and marker as
shown.

Use Via to jump between layer 0.7mm/0.33mm via

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image89.png)

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image90.png)Connect the via and track with GND Pad

Copy and paste these tracks and via on 0402 components.

![A computer screen shot of a computer chip AI-generated content may be
incorrect.](images/media/image91.png)

Place the via on the chips for heat sinking purpose.

![A green screen with white text AI-generated content may be
incorrect.](images/media/image92.png)

![A computer screen shot of a computer chip AI-generated content may be
incorrect.](images/media/image93.png)Add 3.3V via

For RF trace we would use 0.190mm trace for control impedance of 50 Ohm

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image94.png)Set the width of RF in NetClass properties.

![A computer screen shot of a computer AI-generated content may be
incorrect.](images/media/image95.png)Route the RF section

Route the high frequency HSC clock.

![A computer screen shot of a circuit board AI-generated content may be
incorrect.](images/media/image96.png)

![A computer screen shot of a circuit board AI-generated content may be
incorrect.](images/media/image97.png)Trace Low frequency clocks

Add 0.250 mm track width for Switch Model. Press W to increase the mad
width.

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image98.png) We can also use this for the feedback

Ground the Pin

![A screen shot of a computer AI-generated content may be
incorrect.](images/media/image99.png)

Use differential pair by pressing 6 and selecting the netclass "USB" to
route the two usb wires together

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image100.png)Route the rest

![A computer screen shot of a circuit board AI-generated content may be
incorrect.](images/media/image101.png)

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image102.png)Route the UART Section

![A computer screen shot of a circuit board AI-generated content may be
incorrect.](images/media/image103.png)Use Via to jump between top and bottom
layer to route the Boot0

![A computer screen shot of a computer AI-generated content may be
incorrect.](images/media/image104.png)We can place the GND via near transitional jump for
higher bandwidth circuit

![A computer screen shot of a circuit board AI-generated content may be
incorrect.](images/media/image105.png)Complete the rest of the USB connector section.

Complete the led section

![A screenshot of a video game AI-generated content may be
incorrect.](images/media/image106.png)

Select Mounting hole. Select 2 and Press E to change the copper zones to
Solid

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image107.png)

![A computer screen shot of a circuit board AI-generated content may be
incorrect.](images/media/image108.png)Connect the 5Vs power supply traces and
draw polygon layer for 3V power supply.

![A computer screen shot of a star AI-generated content may be
incorrect.](images/media/image109.png)Select only the bottom select by selecting
"Hide all planes but active" and draw traces connecting 3.3V Vias

The other way to do is to convert the bottom layer polygon to 3.3V
layer. For that select the GNB polygon, Crl +C and paste it. Press E to
select the new layer and select 3.3V for bottom layer

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image110.png)

![A screenshot of a video game AI-generated content may be
incorrect.](images/media/image111.png)Now, 3.3V is the bottom layer.

![A computer screen shot of a computer chip AI-generated content may be
incorrect.](images/media/image112.png)Connect rest of the 3.3V and GNB
connections

For copper balancing, change the top copper layer to GND. To do this
Select In1.cu and double click on GND layer. Choose F.CU to GND Layer.

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image113.png)

Press B to repull and now we have GND layer on top layer.

![A computer screen shot of a circuit board AI-generated content may be
incorrect.](images/media/image114.png)

These coppers which are really close could affect the impedance for the
RF section. The traces should be at least 3 times the dielectric width
away.

![A video game screen with a green background AI-generated content may
be incorrect.](images/media/image115.png)

Currently the dielectric is 0.1mm. We want the separation to be at least
0.3mm.

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image116.png)

Draw keypad area to keep out the copper fills.

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image117.png)

Press B to keep out the copper fills.

![A screenshot of a video game AI-generated content may be
incorrect.](images/media/image118.png)

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image119.png)Instead, we can also change the clearance
to 0.35mm.

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image120.png)We can also try thermal relief to have
smaller gap and larger spoke width.

We need to Stitching via to reduce impedance between ground plane and
vias. Place it around the board. The spacing can be calculated as

(3 \* 10\^8)/ (20\* sqrt(4.29) \*2.4\*10\^9) \*10\^3

Speed of light / 20 \* Sqrt of dielectric constant \* Frequency

=3mm

![A computer screen shot of a circuit board AI-generated content may be
incorrect.](images/media/image121.png)

![A green circuit board with many small chips AI-generated content may
be incorrect.](images/media/image122.png)This is what the board looks like

Move the marking on the silkscreen so that the markings do not overlap.

![A computer screen shot of a computer chip AI-generated content may be
incorrect.](images/media/image123.png)

We can add teardrops for smooth transition between wide and narrow
traces. Else, go to tools\> Remove unused pads

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image124.png)

Run DRC Checker.

Fix clearance violation by decreasing the pad size.

![A screen shot of a computer AI-generated content may be
incorrect.](images/media/image125.png)

Reduce the pad size in X axis.

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image126.png)

To solve this error, uncheck the fiducial marker pad from F.Cu.

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image127.png)

To fix it, connect the pad to GND via.

![Uploaded image](images/media/image128.png)

Clearance violation

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image129.png)

Move the GND via.

![A computer screen shot of a green and red line AI-generated content
may be
incorrect.](images/media/image130.png)

Now, we have 0 DRC violation

![A computer screen shot of a computer AI-generated content may be
incorrect.](images/media/image131.png)

Final Board:-

![A computer screen shot of a green circuit board AI-generated content
may be
incorrect.](images/media/image132.png)

Go to Tools \> Generate Bill of Materials to generate the components
needed and their designator values on the PCB.

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image133.png)

We need to know the coordinate of the components to know where the
components are on the PCB.

At the Place \> Grid Place Origin and Drill Place Origin, put the origin
to bottom left.

![A green screen with black dots and white text AI-generated content may
be incorrect.](images/media/image134.png)

Go to files \> Fabrication Output \> Generate Placement files

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image135.png)

.pos file will appear on the project directory.

We now need the Gerber files. Go to files \> Fabrication Output \>
Generate Gerber files. Include the following layers and options.

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image136.png)

Go to generate layers and generate drill files.

You can check the gerber files using Kicad Gerber viewer. These are the
files we need to upload to manufacturer ( Gerber, Position files and
Bill of Materials). We can also send additional notes such as Control
Impedance, clearance and so on.

![A computer screen shot of a computer AI-generated content may be
incorrect.](images/media/image137.png)

To order the PCB, create and upload zip files of Gerber.

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image138.png)

It automatically identified the board requirements

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image139.png)

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image140.png)Select these options

We can have PCBway assemble the whole PCB

![A screenshot of a computer AI-generated content may be
incorrect.](images/media/image141.png)

Then you will have to upload Bill of Material files, Centroid files
(CPL.txt) and assembly drawing optional).
