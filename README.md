# Schematic Style Guide

After the block diagram, the schematic drawing is the very first stage in fleshing out your idea into a working design. It’s when you figure out your project’s electrical flow, and it serves as a crucial reference during the layout stage. For these reasons, it’s incredibly important to build your schematic in a way that is clear, comprehensive, and organized for both you and your teammates. A clean schematic will minimize your chances of making translational errors down the road, making reviews and debugs a breeze.

Here’s a style guide to help you keep your schematics legible and consistent.

## Organization

* **Strive to maintain a left-to-right flow** - 
Have inputs on the left of symbols, outputs on the right -- of course it's not always possible but it's a good rule-of-thumb. In general, don't place pins on the tops of symbols (particularly true for
rectangular symbols representing ICs, but there are exceptions, like an opamp symbol). Power
symbols/flags should be pointed up and GND symbols pointed down.

* **Use flags/indirect connections rather than directly drawn nets.** - 
Only make direct net connections if they are short. This prevents the dreaded “spaghetti” effect and keeps the schematic readable.

* **Make all your pins visible. Avoid invisible pins, even if your CAD tool supports it.** - 
It’s better to keep everything visible to make it more likely that errors are caught.

* **If a pin is purposely left unconnected, mark it and avoid ambiguity.** - 
You can do this using your CAD tool’s no-connect symbol (typically an “X”). This signals to reviewers that the no-connect is intentional.

* **Avoid using 4-way connections** - 
They make it unclear whether the connection is deliberate or a mistake. Use two 3-way connections to make it clear that it was intentional. This way, all 4-way connections default to being a mistake.

* **Place large groups of decoupling caps (ex. for large BGAs) in a separate dedicated section.** - 
It’s OK to place decoupling caps right beside the IC if there are fewer than 5. This keeps things clean.

*  **Be consistent with the placement of your text.** - 
Things like reference designators, values, part numbers, etc. should be placed in the same manner for all components.

* **Organize your schematic by creating sections for major functions.** - 
These may be: FPGA, Processor, Memory, Power - switching regulators, Power - linear regulators, Clock Generation, PCIe, Audio, Video, Board inputs, Board outputs, Decoupling

## Naming Conventions

* **Give all nets clear, descriptive names.** - 
You should be able to tell what a net’s function is by its name alone. For example, use MEM_FLASH_A15 instead of just A15. This way, you know it’s address bit-15 of the flash memory.

* **Same things with Power**
 * Always start with “VCC”. Makes all power nets easy to identify.
 * Include the voltage in the name to make debugging easier (ie. VCC_5V, VCC_3V3, VCC_0V9).
 * Special analog power nets can be designated with AVCC.

* **Ground: GND** - 
If you have separate ground islands, name them AGND, AGND_AUDIO.

* **Name all active low pins with a lowercase ‘n’ instead of an overline.** - 
(ie. RESETn, INTn,)

* **Indicate the positive and negative legs of differential pairs using lowercase 'n’ and 'p’.** - (ie. CLK_DDRp, CLK_DDRn)

* **Begin clock net names with “CLK”.**

* **Special attention is often paid to clock routing during layout so this naming convention is a worthwhile practice.**

* **Use uppercases for all other pin names and net names.** - 
That is, except for the n/p suffixes mentioned above. Consistency is important to readability.

* **Use reference designators for all components and follow standard conventions.** - 
* **BT** – battery
* **R** – resistors
* **RN** – resistor networks
* **C** – general capacitors
* **XC** – decoupling capacitors (designs with hundreds of decoupling caps, like for large BGAs, may quickly run up the count if you only use “C”, so it’s good practice to keep a separate ref des for decoupling caps)
* **L** – inductors and ferrites (alternative FB for ferrite bead)
* **FC** – fiducial
* **T** – transformers
* **D** – diodes (this often includes LEDs)
* **Y** – crystals
* **Q** – transistors
* **P** – multi-pin connectors
* **J** – simple connectors (video connectors, audio connectors, etc.)
* **U** – ICs
* **RG** – power regulators (like LDOs)
* **SW** – switches
* **TP** – test points
* **H** – holes/vias (sometimes it makes sense to include specific components on the schematic to designate corresponding holes on the layout, like in DDR routing)

* **Be specific with I/O pins.**
Parts with programmable I/O or I/O that can take on multiple functions should use pin names that reflect the function(s) selected for the particular design, rather than listing all the possible functions or using the generic pin names (like IO_B7_255). For busses, indicate the signal direction (input into the device, output from the device, or bi-directional) using lowercase i,o, and io prefixes to the signal names.

 * This is particularly useful for FPGAs (where almost all I/O are programmable). It’s very good practice to define your FPGA’s top pin-assignment in your FPGA software, compile to make sure it’s valid, export the pin-assignment, and use this as the basis for creating the symbol.

* **If your CAD software doesn’t have good features to indicate a net’s controlled impedance, include it in the net name.** - For example: VIDEO_IN_CVBS_Z75 (Z=Impedance, 75=ohms), PCIE_TX_ZD85 (ZD=differential impedance, 85=ohms)

## Symbols

* **Order pins on the symbols by function, not by number.** - 
Place power pins near the top and ground pins near the bottom.

* **For IC packages with a thermal pad, create an additional pin on the symbol to connect it to the ground plane.** - The clearest way to do this is to name it GND_PAD with a pin number one greater than the total number of pins.

* **Create symbols by copying/pasting the pinout table from the datasheet into a spreadsheet.** - 
Then import this spreadsheet into your CAD tool. This is opposed to typing in the pin names/numbers manually. Copying and pasting minimizes the chances of data entry errors.

* **Use multi-part symbols for large devices to keep things organized.**
Break up the sub-symbols by major function. Have a separate symbol for power and ground. Using multipart symbols applies not only to large ICs but also to components like resistor networks (ie. a 16-pin package containing 8 resistors). Resistor networks are often used for series termination on large busses. It’s often cleaner to create a multi-part symbol where each part is a single resistor. This way, you can order the resistors on your schematic without nets crossing over when directly connecting them.

## General

* **Include non-electrical components on the schematic to make sure they get included in the BOM and that the layout engineer knows about them.** - Things like fiducials, tooling/mounting holes, fans/heat sinks, breakaway tabs, etc.

* **Create a test-point symbol and connect it to pins for which you specifically want a test-point via to probe during debug.**

* **Include lots of notes!**
Use brief text notes to explain why you connected certain things in a certain way. If a part has some pin-based config settings (using pull-ups/downs), use notes to indicate which settings you’ve specified for the design – you’d be surprised how often such pins are hooked up incorrectly compared to the note. Include notes to specify the I2C/SMBus addresses of various devices so you don’t have to look these up in the datasheets during debug. Use notes to convey layout guidelines. It’s always better to have more information than too little.


## References

Original article: http://blog.upverter.com/post/102541405327/schematic-style-guide

