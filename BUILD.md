# parts and space

i checked the circuit against the standard 14-board Ben Eater setup. the current design is still too large for that plank and the $100 target when buying the chips new.

i shared repeated control logic and packed gates from different schematic sheets into the same physical chips. that removed 18 chips. addition, subtraction, multiplication, division and Clear still pass the same checks.

| | before | current |
| --- | ---: | ---: |
| chips drawn | 144 | 126 |
| chips including known remaining allocations | 166 | 148 |
| approximate IC cost with quantity breaks | $135 | $124 |
| minimum 63-row boards, with no gaps | 20 | 18 |
| example packing with two empty rows between chips | 26 | 24 |

the cost is for the known IC allocation only. it leaves out the remaining keypad/entry gates, displays, switches, resistors, capacitors, extra jumpers, any extra boards, tax and shipping. breadboards, existing wire and the 5V supply are being reused. possible savings from owned chips are not counted yet.

[parts-estimate.csv](parts-estimate.csv) has the quantities, seller listing prices and links retrieved on November 4. some quantities are rounded up where buying a few spares costs less. these are listing snapshots from DigiKey, Mouser and Newark, not an order or a delivered quote. prices and stock need checking again before buying anything.

the board count uses the pin rows occupied by each DIP package. it is a size check, not a wiring layout. decoupling, clock distribution, power connections and wire clearance still need planning. the 126 chips already drawn need at least 16 boards even without gaps, before adding the remaining circuits.

Ben Eater's [parts list](https://eater.net/8bit/parts) has 14 breadboards and mostly 74LS chips. this design currently uses 74HC parts. reused chips need their part numbers and voltage levels checked before substitution.

the compacted circuit passed 4,593 state/flag/command checks, 272 complete calculations and 307 Clear/restart cases using KiCad's exported connections. keypad commands and the saved key digit still come from the test setup. physical timing and hardware have not been tested.

the next design decision is whether to keep the existing plank and $100 as hard limits, or allow extra boards and spending. the current parts list is not ready to order.
