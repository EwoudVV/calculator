# Calculator

a breadboard calculator made from logic chips, with no microcontroller or firmware

the plan is a number keypad, addition, subtraction, multiplication and division. it will take whole-number inputs from 0 to 9999, show negative results, and have overflow and divide-by-zero indicators

the display will have six digits so division results can show two decimal places. whole-number results are limited to 9999 in magnitude. the buttons and display will fit into a printed front panel, with the breadboards mounted behind it

the arithmetic plan uses three number registers and one shared decimal adder, working through one digit at a time. multiplication reuses addition, and division works through the digits like long division. division results will round to the nearest hundredth

i'm working out the control circuit next. i'll reuse the breadboards and 5V supply from my Ben Eater computer, with some extra male-to-male jumpers

open [calculator.kicad_pro](calculator.kicad_pro) in KiCad 10. the schematic and PCB files are empty for now; the build is planned for breadboards

made for Hack Club Half Life, week 5
