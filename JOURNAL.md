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

## Drew the shared decimal adder

2026-11-03, 4 hours

i drew the arithmetic section and connected it to the three number registers. two HC283 adders handle the binary sum and decimal correction. for 9+9, the circuit stores 8 in the current digit and carries 1 into the next.

subtraction uses the same adder by selecting the nine’s complement of the second digit and starting with carry set to 1. i added a register to keep the carry and track zero, negative results and numbers that are too large.

i checked the arithmetic using KiCad’s exported connections, including carries across digits, negative subtraction and Clear/reset. these checks use simulated control signals. the controller, keypad and display-driver circuits still need drawing, and nothing has been built yet.

![shared decimal adder](images/shared-decimal-adder.png)

![decimal adder detail](images/decimal-adder-detail.png)

![arithmetic flags](images/arithmetic-flags.png)

![registers linked](images/registers-linked.png)

## Drew the digit sequencer

2026-11-04, 6 hours

i drew the timing section that moves the calculator through each digit. two counters track the current step and digit position, so the adder gets eight digit steps before the controller moves on.

i added the display latch controls too. they select one display position, let it take the digit, then close it before the number register shifts. whole-number results leave the two decimal positions blank, while division uses all six.

connecting the gates exposed another Clear timing problem. resetting straight from the controller state could clear the number registers as a display latch closed. i added a flip-flop to delay reset by one clock and keep the digit data steady.

i checked the exported circuit through calculations, clearing partway through and starting again. the main state decoder, keypad electronics, display drivers, clock source and power-on reset circuit still need drawing. nothing has been built yet.

![phase and digit counters](images/sequencer-counters.png)

![display latch register](images/display-latch-register.png)

![clocked bank reset](images/clocked-bank-reset.png)

![display timing](images/display-transfer.png)

![word sequencer](images/word-sequencer.png)

![registers linked](images/registers-linked.png)

## Drew the main controller

2026-11-04, 5 hours

i drew the main controller that chooses what happens next. it waits for each eight-digit pass to finish, then uses carry, zero and overflow flags to choose the next step.

multiplication loops through addition under that control circuit. division has counters for the quotient digit and current position, with branches to subtract, restore the remainder and round the answer. i also drew the display-format and error registers.

i checked the controller using KiCad's exported connections, including full calculations, Clear partway through and starting again. the tests supply accepted keypad commands, and the drawn gates run the sequence after that.

the keypad scanner, entry controls, display drivers, clock and power-on reset still need drawing. the design has grown a lot, so i need to check the full parts cost and breadboard space before building it.

![main state counters](images/main-state-counters.png)

![arithmetic branch gates](images/arithmetic-branch-gates.png)

![division counters and display status](images/division-counters-status.png)

![controller outputs](images/controller-outputs.png)

![main controller](images/main-controller.png)

## Moved the calculator to a PCB

2026-11-05, 8 hours

the breadboard version was going to take too long to wire, so i switched to a pcb. i picked surface mount versions of the logic chips and added the keypad circuit, display drivers, clock and power-on reset to the schematic.

the board is 140 x 120 mm. the buttons and display are on the front, and i put parts on both sides to fit the circuit. i placed all the parts and started connecting them to 5v and ground on the inner layers.

i ran 188 calculations in the circuit simulation with the new keypad logic and display latches. i checked negative results, division rounding and Clear. i still need to finish the routing and price out the full build before ordering a board.

![front of the pcb in KiCad](images/pcb-front.png)

![back of the pcb in KiCad](images/pcb-back.png)

## Routed power and control on the PCB

2026-11-05, 15 hours

i finished connecting 5V and ground across the board and routed the clock, power-on reset and Clear. the clock reaches the registers and control logic, and the reset and Clear signals reach the circuits they need to reset.

i also routed a lot of the signals between chips. some traces run on the inner layers alongside the power and ground pours. KiCad went from 1,319 open connections to 506.

the board still matches the schematic. KiCad flagged two spots where the copper pour gets very narrow. i still have signal traces left to route before i can order the board.

![front copper in KiCad](images/routing-front.jpg)

![back copper in KiCad](images/routing-back.jpg)

## Finished routing the PCB

2026-11-07, 15 hours

i kept routing signals on the 4-layer board, using 0.16 mm traces and smaller vias where space was tight. i added short links where new traces cut the power planes apart. KiCad went from 506 open connections to 426, but the middle of the board was full.

i checked how much wiring the board needs against how much it can fit. the chips for each section are spread across the whole board, so most signals have to cross the middle. it needs about twice what 4 layers can hold, and even 6 layers left 301 connections unrouted.

i moved to a 16-layer board with finer rules: 0.105 mm spacing, 0.11 mm traces and 0.45 mm vias with 0.2 mm holes. the autorouter connected everything, and i cleaned up 172 leftover traces and vias that didn't connect to anything.

KiCad now shows 0 open connections and no errors, and the board still matches the schematic. 5 small warnings are left: silkscreen overlaps and one copper sliver. i also worked out calculation times at a 96 kHz clock. addition takes 0.45 ms and 99 × 99 takes 23 ms.

16 layers will cost a lot more than my budget, so i need a quote and to check the manufacturer can make the finer spacing before ordering. grouping each section's chips closer together could get it back to fewer layers.

![3D view of the front](images/pcb-3d-front.png)

![3D view of the back](images/pcb-3d-back.png)

![front copper](images/routed-front.png)

![back copper](images/routed-back.png)

![inner layer 1, ground](images/routed-inner-1-ground.png)

![inner layer 2](images/routed-inner-2.png)

![inner layer 3](images/routed-inner-3.png)

![inner layer 4](images/routed-inner-4.png)

![inner layer 5](images/routed-inner-5.png)

![inner layer 6, 5V](images/routed-inner-6-5v.png)

![inner layer 7](images/routed-inner-7.png)

![inner layer 8](images/routed-inner-8.png)

![inner layer 9](images/routed-inner-9.png)

![inner layer 10](images/routed-inner-10.png)

![inner layer 11](images/routed-inner-11.png)

![inner layer 12](images/routed-inner-12.png)

![inner layer 13](images/routed-inner-13.png)

![inner layer 14](images/routed-inner-14.png)