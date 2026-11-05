# pcb build

the calculator is going on one 140 by 120 mm board. there are four copper layers, with 5V and ground on the inside. the keys and display are on the front. the surface mount parts use both sides.

J101 takes regulated 5V. pin 1 is 5V and pin 2 is ground. TP1 and TP2 are the supply test points, TP3 is the clock, and TP4 is power-on reset. the clock is about 96 kHz. the displays and power connector are through-hole.

[pcb-bom.csv](pcb-bom.csv) lists the parts on the board. the prices filled in so far add up to $82.47. that leaves the other parts, the board, assembly, shipping and tax to price. the total target is still $100.

the full schematic passed the KiCad error check. i tested 188 calculations from key samples through the display latches. that included rounding, negative results, overflow and divide-by-zero. i also ran the key timer for a complete calculation and Clear.

the parts are placed and most of the power pads connect to the inner planes. the board and schematic match in KiCad. signal routing, the remaining power connections and the final board check still need to finish before ordering.

[parts-estimate.csv](parts-estimate.csv) is the earlier breadboard price check.
