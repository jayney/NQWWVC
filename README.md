# NQWWVC
Not Quite the Worlds Worst Video Card

This is a re-creation of Ben Eater's "World's Worst Video Card", using programmable logic devices, 
specifically ATF22V10C, to replace the discrete logic used for the horizontal and vertical sync and
blanking signal generation. The result is a reduction in chip count from 20 to 4. The downside is
that these chips are quite power hungry. The 10ns versions I used draw around 110mA EACH...

The counter outputs connect to a SST39SF010A flash ROM, huge overkill, but they are cheaper and
faster than 28C series EEPROMS, so I simply pull the unused address lines low. /CS is driven from
the vertical blanking signal, and /OE is driven by the horizontal blanking. Otherwise, the circuit is
functionally identical to Ben Eater's version at the end of the second episode in that series.

The horizontal section uses one ATF22V10C as a 10 bit counter replacing the 3 x 74LS161 counters, 
and the outputs feed in to a second ATF22V10C which then provides 4 outputs at the required times. 
Each output is equivalent to one of 8 input NAND gates that Ben used. As there were 6 unused outputs, 
I decided to incorporate the two SR flip flops too. And since product terms for PLD's can use inverted
or non-inverted inputs, the two inverting buffer chips Ben used also disappear.

The vertical section uses the same 10 bit counter as the horizontal section, but the timings are different,
so the chip replacing the 8 input NAND's and the SR flip flops is different, but only in the input values 
used to trigger the ouptuts.

WinCUPL, as horrible and buggy as it is, was used for creating the firmware, but jed files are included,
so chips can be flashed with a compatible programmer, the TL866II for example. There's nothing terribly
complicated, so converting to Galasm/Galer should be fairly trivial.

The finch test image can be downloaded from Ben Eater's site, and programmed in to any ROM of 32k (x8) or
more.
