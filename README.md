Boss CE-2 Clone
===============

**Andrew Martin, September 2025**

*Please note that I don't yet have this working! I believe this is a result of a bad clone MN3007!*

Introduction
------------

The Boss CE-2 is one of the best-known chorus pedals around and there
have been several clones with and without modifications. In the
`Schematics` folder, there is a collection of freely-available
schematics and information while the `Analysis` folder contains some
information on chorus effects and a full analysis of the workings of
the Boss CE-2 from ElectroSmash.

The `kicad` folder contains my schematic for a clone which is
essentially the original version with the 'anti-tic' modification and
with 2N5088 transistors throughout. Within that are two sub-folders,
`V0.1` and `V1.1`. *Do not use V0.1* - this was an erroneous design
where the inputs to the RC4558 (U1) were swapped by mistake!

V1.1 is my first correct layout with (optional) LED and (bypassable)
-ve power supply resistor and diode (see some of the schamatics and
analyses for references to this). It is a very tightly packed 57x87mm
board.

V1.2 is the current version in which the PCB layout is inspired by the
one used by Azure. This one contains the (bypassable) -ve power supply
resistor and diode, but not the LED as the intention is to use it with
my FootSwitch board. This is a somewhat less tightly packed board
(73x83mm) with wider (1mm) tracks; there was notable resistance
with the narrow tracks of V1.1.

Kicad
-----

The design uses my own symbol for the 2N5088 which is in my
`ACRM_KiCad_Libs` library.

The rate and depth pots (both are 100K linear pots) are not included
in the schematic - instead there are just positions for Molex KK254
connectors. If you wish, you can omit the connectors and wire direct
to the board.

Testing
-------

Note that the MN3007/MN3101 need a negative power supply, so it is
correct that the GND pin (Pin 1) on both is connected to the +9VA rail
and the input voltage VDD pin (Pin 3 on the MN3101 and Pin 5 on the
MN3007) is connected to GND.

Faulty (apparently they are very static sensitive, but I haven't seen
that), or bad clone, MN3101s are common, so it's a good idea to check
that it's working properly. There are three things to check in the circuit:

- Connect a meter across pins 1 (your black test lead) and 3 (red test
  lead) to find the power supply voltage you are getting. This should
  be showing a value of around -8.5V. Make sure you note what the
  exact voltage is.

- Connect a meter across pins 1 (black test lead) and 8 (VGG_OUT, red
  test lead). This should read VDD*14/15, so if your VDD was -8.5, you
  should be obtaining -7.93V.

- Put a 'scope on pin 2 (CP1) and then on pin 4 (CP2). You should see
  a (roughly) square wave form that expands and contracts. The amount
  of variation changes with the depth pot and the rate with the rate
  pot.

If those tests all work, then your MN3101 is working correctly.

Setup
-----

Turn the **Rate** pot fully **anti-clockwise** (minimum rate) and the
**Depth** pot fully **clockwise** (maximum depth).

Use a signal generator to feed a 200Hz, +3dBm sine signal into the
input. This comes from the setup information I have seen online.

+3dBm is 0.893V peak-to-peak (0.316V RMS) assuming an input impedance
of 50R. However, with the 1M Rin1 input resistor, the impedance should
be closer to 1M, and that would require an input signal of >126V
peak-to-peak (44.7V RMS)!!!

I would start with 1V peak-to-peak. Connect an oscilloscope to the
emitter of Q3 and turn the bias pot (the trimmer on the board) until
you see a center point where the sine wave is symmertrical (equally
clipped at top and bottom). If you don't see any clipping, then
increase the input sine wave voltage until you do.


