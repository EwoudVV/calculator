# Journal

## Planning the calculator

2026-11-02, 2 hours

i’m making a breadboard calculator from logic chips, with no microcontroller or firmware. it will take whole-number inputs from 0 to 9999 and do addition, subtraction, multiplication and division. division results will show two decimal places.

i worked through an arithmetic plan using three number registers and one shared decimal adder. multiplication reuses addition, and division works through the digits like long division. i checked those arithmetic steps in a Python simulation and started looking at parts.

i’ll reuse my Ben Eater breadboards and 5V supply, with a printed front panel for the buttons and display. the controller, complete parts cost and actual schematic still need working out.

## Drew the number registers

2026-11-02, 5 hours

i drew the number-storage section in KiCad. A holds the first number, B holds the second, and W holds the working result. the chips can store and shift digits, which removes some extra selector circuitry.

i connected the keypad, arithmetic and display in the control simulation. it now takes button presses through to a displayed answer. i checked held and bouncing keys, rejecting a fifth digit, arithmetic errors and starting another calculation after a result.

Clear exposed a display timing problem: the digit data could change while a display latch was closing. i changed the sequence to close the latch, hold the data, then reset the registers.

the storage schematic includes the selectors, decoupling capacitors and power connection. its exported connections match the intended wiring. the arithmetic unit, controller gates and display circuit still need drawing. nothing has been built yet.

![number registers](images/number-registers.png)

![number register bank](images/number-register-bank.png)

![register feedback selector](images/register-feedback-selector.png)

![digit input selectors](images/digit-input-selectors.png)

![register bit lane](images/register-bit-lane.png)
