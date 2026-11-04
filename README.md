# Calculator

a breadboard calculator made from logic chips, with no microcontroller or firmware

the plan is a number keypad, addition, subtraction, multiplication and division. it will take whole-number inputs from 0 to 9999, show negative results, and have overflow and divide-by-zero indicators

the display will have six digits so division results can show two decimal places. whole-number results are limited to 9999 in magnitude. the buttons and display will fit into a printed front panel, with the breadboards mounted behind it

the arithmetic plan uses three number registers and one shared decimal adder, working through one digit at a time. multiplication reuses addition, and division works through the digits like long division. division results will round to the nearest hundredth

i've drawn the number registers, shared decimal adder, status registers and digit sequencer. the sequencer runs eight arithmetic steps per word and transfers digits into the display latches. Clear closes those latches before resetting the number registers

i checked the drawn connections against calculations and Clear/restart sequences. the main controller still uses simulated state selections. its decoder, keypad electronics and display drivers still need drawing, along with the clock and power-reset circuit

i'll reuse the breadboards and 5V supply from my Ben Eater computer, with some extra male-to-male jumpers. the complete parts cost is still being worked out

open [calculator.kicad_pro](calculator.kicad_pro) in KiCad 10. the number registers link to the arithmetic, sequencer and display-timing sheets. nothing has been built yet

![number registers and feedback selectors](images/registers-linked.png)

the two selectors at the bottom choose the digit to append: zero, a keypad digit, a quotient digit or the leading digit from A

![digit input selectors](images/digit-input-selectors.png)

the adder works through one decimal digit at a time. a second adder corrects the result, and the carry is saved for the next digit

![shared decimal adder](images/decimal-adder-detail.png)

two counters track the current phase and digit. arithmetic uses eight digit steps; display transfers give each latch time to close before moving the data

![phase and digit counters](images/sequencer-counters.png)

Clear goes through a flip-flop so the display latch closes one clock before the number registers reset

![clocked bank reset](images/clocked-bank-reset.png)

progress is in [JOURNAL.md](JOURNAL.md)

made for Hack Club Half Life, week 5
