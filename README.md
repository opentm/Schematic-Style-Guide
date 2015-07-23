# Schematic Style Guide

After the block diagram, the schematic drawing is the very first stage in fleshing out your idea into a working design. It’s when you figure out your project’s electrical flow, and it serves as a crucial reference during the layout stage. For these reasons, it’s incredibly important to build your schematic in a way that is clear, comprehensive, and organized for both you and your teammates. A clean schematic will minimize your chances of making translational errors down the road, making reviews and debugs a breeze.

Here’s a style guide to help you keep your schematics legible and consistent.

# Organization

## Strive to maintain a left-to-right flow.
Have inputs on the left of symbols, outputs on the right -- of course it's not always possible but it's
a good rule-of-thumb. In general, don't place pins on the tops of symbols (particularly true for
rectangular symbols representing ICs, but there are exceptions, like an opamp symbol). Power
symbols/flags should be pointed up and GND symbols pointed down.

## Use flags/indirect connections rather than directly drawn nets.
Only make direct net connections if they are short. This prevents the dreaded “spaghetti” effect and keeps the schematic readable.

## Make all your pins visible. Avoid invisible pins, even if your CAD tool supports it.
It’s better to keep everything visible to make it more likely that errors are caught.

## If a pin is purposely left unconnected, mark it and avoid ambiguity.
You can do this using your CAD tool’s no-connect symbol (typically an “X”). This signals to reviewers that the no-connect is intentional.

## Avoid using 4-way connections.
They make it unclear whether the connection is deliberate or a mistake. Use two 3-way connections to make it clear that it was intentional. This way, all 4-way connections default to being a mistake.

## Place large groups of decoupling caps (ex. for large BGAs) in a separate dedicated section.
It’s OK to place decoupling caps right beside the IC if there are fewer than 5. This keeps things clean.

## Be consistent with the placement of your text.
Things like reference designators, values, part numbers, etc. should be placed in the same manner for all components.

## Organize your schematic by creating sections for major functions.
These may be:
FPGA, Processor, Memory, Power - switching regulators, Power - linear regulators, Clock Generation, PCIe, Audio, Video, Board inputs, Board outputs, Decoupling

# Naming Conventions

## Give all nets clear, descriptive names.
You should be able to tell what a net’s function is by its name alone. For example, use MEM_FLASH_A15 instead of just A15. This way, you know it’s address bit-15 of the flash memory.

# Same things with Power
* Always start with “VCC”. Makes all power nets easy to identify.
* Include the voltage in the name to make debugging easier (ie. VCC_5V, VCC_3V3, VCC_0V9).
* Special analog power nets can be designated with AVCC…

## Ground: GND
If you have separate ground islands, name them AGND, AGND_AUDIO.

## Name all active low pins with a lowercase ‘n’ instead of an overline.
(ie. RESETn, INTn,)

## Indicate the positive and negative legs of differential pairs using lowercase 'n’ and 'p’. (ie. CLK_DDRp, CLK_DDRn)

## Begin clock net names with “CLK”.

## Special attention is often paid to clock routing during layout so this naming convention is a worthwhile practice.

## Use uppercases for all other pin names and net names.
That is, except for the n/p suffixes mentioned above. Consistency is important to readability.

## Use reference designators for all components and follow standard conventions.

** BT – battery
** R – resistors
** RN – resistor networks
C – general capacitors
XC – decoupling capacitors (designs with hundreds of decoupling caps, like for large BGAs, may quickly run up the count if you only use “C”, so it’s good practice to keep a separate ref des for decoupling caps)
L – inductors and ferrites (alternative FB for ferrite bead)
FC – fiducial
T – transformers
D – diodes (this often includes LEDs)
Y – crystals
Q – transistors
P – multi-pin connectors
J – simple connectors (video connectors, audio connectors, etc.)
U – ICs
RG – power regulators (like LDOs)
SW – switches
TP – test points
H – holes/vias (sometimes it makes sense to include specific components on the schematic to designate corresponding holes on the layout, like in DDR routing)

