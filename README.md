# Calculator

a breadboard calculator made from logic chips, with no microcontroller or firmware

the plan is a number keypad, addition, subtraction, multiplication and division. it will take whole-number inputs from 0 to 9999, show negative results, and have overflow and divide-by-zero indicators

the display will have six digits so division results can show two decimal places. whole-number results are limited to 9999 in magnitude. the buttons and display will fit into a printed front panel, with the breadboards mounted behind it

the arithmetic plan uses three number registers and one shared decimal adder, working through one digit at a time. multiplication reuses addition, and division works through the digits like long division. division results will round to the nearest hundredth

i've drawn the number registers, shared decimal adder, digit sequencer and main arithmetic controller. fixed gates choose the next step using carry, zero and overflow flags. multiplication and division reuse the adder through those loops

i checked the drawn connections from an accepted command through to the display update, including negative results, rounding, overflow, divide-by-zero and Clear. the tests still supply keypad and entry commands. the keypad scanner, entry controls, display drivers, clock source and power-on reset circuit still need drawing

i'll reuse the breadboards and 5V supply from my Ben Eater computer, with some extra male-to-male jumpers. sharing control gates removed 18 chips, but the current design still exceeds the existing plank and $100 target. the [parts and space check](BUILD.md) shows what is included and what still needs reducing

open [calculator.kicad_pro](calculator.kicad_pro) in KiCad 10. the number registers link to the arithmetic, timing and main-controller sheets. nothing has been built yet

![number registers and feedback selectors](images/registers-linked.png)

the two selectors at the bottom choose the digit to append: zero, a keypad digit, a quotient digit or the leading digit from A

![digit input selectors](images/digit-input-selectors.png)

the adder works through one decimal digit at a time. a second adder corrects the result, and the carry is saved for the next digit

![shared decimal adder](images/decimal-adder-detail.png)

two counters track the current phase and digit. arithmetic uses eight digit steps; display transfers give each latch time to close before moving the data

![phase and digit counters](images/sequencer-counters.png)

Clear goes through a flip-flop so the display latch closes one clock before the number registers reset

![clocked bank reset](images/clocked-bank-reset.png)

the main state counters run the operation sequence. branch gates send the controller back through multiplication and division loops, or on to the result and error states

![main state counters](images/main-state-counters.png)

the division counters track the current quotient digit and position. a separate register keeps the display format and error indicators

![division counters and display status](images/division-counters-status.png)

progress is in [JOURNAL.md](JOURNAL.md)

made for Hack Club Half Life, week 5
