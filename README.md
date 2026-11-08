# Calculator

a calculator built from logic chips. there is no microcontroller or firmware.

it takes whole numbers from 0 to 9999 and does addition, subtraction, multiplication and division. it shows negative results, rounds division to two decimal places, and has lights for overflow, divide by zero and a full input.

three registers hold the numbers. a shared decimal adder works through them one digit at a time. the controller runs the loops for multiplication and long division.

## calculation times

calculated at a 96 kHz clock.

| calculation | clock cycles | time |
| --- | ---: | ---: |
| 27 + 15 or 27 − 15 | 43 | 0.45 ms |
| 12 × 34 | 369 | 3.84 ms |
| 99 × 99 | 2,253 | 23.47 ms |
| 7 ÷ 2 | 373 | 3.89 ms |
| 9999 ÷ 1 | 709 | 7.39 ms |

## pcb

the board is 140 × 120 mm. the keypad and display are on the front, with surface mount logic on both sides. it runs on 5 V.

open [calculator.kicad_pro](calculator.kicad_pro) in KiCad 10. the [build notes](BUILD.md) have the board status and parts list. progress from the breadboard design is in [JOURNAL.md](JOURNAL.md).

![pcb layout](images/pcb-front.png)

![shared decimal adder](images/decimal-adder-detail.png)

made for Hack Club Half Life, week 5
