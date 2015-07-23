# Schematic-Style-Guide


# Draft

# Schematic Style Guide


After the block diagram, the schematic drawing is the very first stage in fleshing out your idea into a working design. It’s when you figure out your project’s electrical flow, and it serves as a crucial reference during the layout stage. For these reasons, it’s incredibly important to build your schematic in a way that is clear, comprehensive, and organized for both you and your teammates. A clean schematic will minimize your chances of making translational errors down the road, making reviews and debugs a breeze.
Here’s a style guide to help you keep your schematics legible and consistent (you can download a printable checklist of the Style Guide here!).

## Strive to maintain a left-to-right flow.
Have inputs on the left of symbols, outputs on the right -- of course it's not always possible but it's
a good rule-of-thumb. In general, don't place pins on the tops of symbols (particularly true for
rectangular symbols representing ICs, but there are exceptions, like an opamp symbol). Power
symbols/flags should be pointed up and GND symbols pointed down.

## Use flags/indirect connections rather than directly drawn nets.
Only make direct net connections if they are short. This prevents the dreaded “spaghetti” effect and keeps the schematic readable.
