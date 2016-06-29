# RC2014 Bank Switcher
Implements a minimal bank switcher to swap the RC2014 boot ROM for 32kB of RAM with 1x 74HCT00, 1x 74LS32, and 1x 74HCT04.

Designed to work with one standard RC2014 ROM module and two standard RC2014 RAM modules.

One RAM module and the bank switcher are installed in any slot in the centre of the backplane (slots 3-8). The ROM and the second RAM module need their A15 signal replaced with output from the bank switcher. This is most easily achieved through the jumpers on the RC2014 backplane between slots 2 and 3 and slots 6 and 7.

In my setup the extra RAM is installed in slot 2 and the ROM installed in slot 7, any RC2014 board that does not require A15 (eg. the serial board, IO board, clock board) can be installed in slots 1 and 8. Jumpers A14 to A0 and D0 to D7 are bridged on both sides of the backplane. Pin headers are installed in Tx, Rx and the four auxilliary bus lines. The replacement A15 signals for the ROM and the extra RAM are brought out to Aux 1 and Aux 2 by setting jumpers on the bank switcher board. Aux 1 is then connected to A15 on the slot 2 side of the left A15 jumper. Aux 2 is conneccted to A15 on the slot 7 side of the right A15 jumper.

The ROM and RAM A15 signals are also brought out to a header at the A15 end of the bank switcher board to simplify alternative setups.

ROM is mapped as usual (0x0000 to 0x2000) on reset. Any write to IO address 0xf0 to 0xff will disable the ROM and enable a standard RC2014 32kB RAM module. It is not possible to switch the ROM back in except on a reset.

The gerbers in v1_0 have been tested. Later versions have not been built. v1_0 works electrically but the hole for pin A8 of the RC2014 bus header is too small for a standard header. This signal is not used so the problem is resolved by simply removing the pin from the header.

v1_0 - Initial revision.
v1_1 - Enlarged A8 of the RC2014 bus header. Enlarged holes for P3 (auxilliary A15 output header).
