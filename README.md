# AmiExtFDD

AmiExtFDD is an External Floppy Disk Drive Interface for Amiga computers. It is extremely versatile and flexible, allowing connection of PC drives, Amiga drives and various floppy drive emulators.to any Amiga computer.

## Summary
*(The following is an English translation of the original author's notes, by Google Translate and manual intervention from SukkoPera)*

I made my own version of the interface to connect an external floppy drive (or FDD emulator) to the *DISK DRIVE* connector. First, the drive must be connected to the interface with a straight cable (without any twists). You can connect the original, internal DD (Double Density) drive from the Amiga or HD (High Density) drives from the PC (converted or not). Regardless of the type of connected drive, it will be seen by the Amiga as a DD drive (880 kB). If you connect a PC HD drive and use HD floppy disks (i.e.: "with two holes"), the second hole should be sealed, otherwise you will experience read/write errors. The advantage is that the PC drive can be used without changing its number from DS1 to DS0 (you would need a soldering iron in order to do this on most drives).

The interface is powered from the disk drive connector (pin 12) and consumes a current of approximately 10 mA. The drive itself can also be powered from this connector or directly from the power supply that the Amiga is powered by.

The 74LS38 chip was used to adapt the *MOTOR ON/READY* signal to the FDD bus standard, which uses open collector (OC) outputs. However my tests show that it can be done with a regular 74LS00.

The interface is located on a double-sided board (38 vias) of 6x5 cm, with surface-mount components on the upper layer only. The board can be used with either straight or angled DB23 connectors (after straightening the legs). As a small curiosity, I would like to add that I made the prototype board without etching (with a mini drill and a small cutter).

## Configuration
*(Still from the original author's notes)*

Depending on the type of the connected floppy disk drive, the interface jumpers should be set appropriately (they must not be changed while the interface is powered on):
- J1 responsible for the *READY* signal. If you connect a non-converted drive to a PC, set this jumper in position 1-2 (the *READY* signal will be generated based on *SELx* and *INDEX* signals). Setting the jumper in position 2-3 will cause that the *READY* signal will be read directly from pin 34 of the floppy disk drive (Amiga or a converted PC one). **NOTE: Due to a construction error, this jumper must always be set to the 1-2 position.**

- J2 responsible for the *DISK CHANGE* signal. If you connect a non-converted drive from the PC, set the jumper in position 1-2 (the *DISK CHANGE* signal will be read directly from pin 34 of the drive). Setting the jumper in position 2-3 will cause the *DISK CHANGE* signal to be read directly from pin 2 of the floppy disk drive (Amiga or a converted PC one).

- J3 is responsible for the *SELx* activation signal that must reach the drive. Most floppy drives have a jumper to select the drive number (DS0 or DS1). Depending on the set drive number, the *SELx* signal must be given to the appropriate drive pin. If the drive is set as DS1 (e.g.: unmodified PC drives and drives without a jumper for selecting the number), the J3 jumper must be set in position 1-2 (*SELx* signal will hit pin 12 of the drive). If the drive is set as DS0 (Amiga or a converted PC one), then the J3 jumper must be set in position 2-3 (*SELx* signal will hit pin 10 of the drive).

- J4 is used to select the floppy disk drive number under which it will be visible in the Boot Menu and in the AmigaDOS/Workbench operating system. This number depends on the jumper position: 1-2 = DF1, 3-4 = DF2, 5-6 = DF3. On the Amiga CDTV this is different: 1-2 = DF0, 3-4 = DF1, 5-6 = DF2.

## Compatibility
*(Still from the original author's notes - **I (SukkoPera) haven't tested this board yet**.)*

I tested on Amiga 500 (KS 2.05) and Amiga 600 (KS 3.1) interface interoperability (all jumpers in position 1-2) with five unmodified PC drives, which I powered from the *DISK DRIVE* connector:
- TEAC FD-235HF (6291)
- NEC FD1231H
- SONY MPF920 Z / 131
- ALPS DF354H090F
- Samsung SFD-321B (/E REV.A)

I tested each of them in *D-Copy 2.0* and *X-Copy 2.9* by reading the floppy disk into RAM, rewriting it and verifying the data. Only the Samsung SFD-321B drive had read errors (red "4"), but only in D-Copy and only on Amiga 500 (rev. 6A), both with Kickstart 2.05 and 3.1. The same problems occurred with this one drive when converted to work natively with Amiga and connected as internal DF0. In this case, the reading errors in D-Copy were on both the Amiga 500 and 600. This is a fault of the drive itself, generating incompatible signals.

I don't have any FDD emulators for testing, but they should all work with the interface.

NOTE: If the interface is plugged into the *DISK DRIVE* connector and no drive is connected to it, it will be detected by the Amiga anyway (it will have the number set with the J4 jumper). This drive will be visible in the Boot Menu and its icon `DFx: ????` will appear on the Workbench counter.

## History
I'm not sure of how this board came into existance, but I think the original version was developed by Roman „RomanWorkshop“ Breński. It is available [on GitHub](https://github.com/Sakura-IT/AmiExtFDD).

Those board design files, though, do NOT match the Gerbers that are available in the accompanying `Gerber_AmiExtFDD.zip` file. The latter is a more advanced design and I think it is what Sakura used to produce the board that went into their [External Floppy Drives](https://retroami.com.pl/index.php?id_product=153&controller=product&id_lang=1&search_query=sakura&results=1) that were sold at RetroAmi. The manual for that interface additionally credits the work to Jarosław „jarob“ Bieliński and Radosław „strim“ Kujawaauthor.

The board design is done in Eagle and appears to be for version 1.01. The board file is not routed and components haven't even been placed.

I later [found some updated files for version 1.02](http://romanworkshop.blutu.pl/elec/amiextfdd.htm), so I thought I would fork the original repo to merge it with the update and try to reconstruct the history of this nice piece of hardware. I'm not sure what is changed in this version, but at least the components have been placed on the board, even though they do not seem to match the final design the author is talking about in one of the accompanying PDF documents.

So here we go: the schematics, board design and gerbers we have are all for different revisions of the board.

To be clear: all I (SukkoPera) did was collect original design files and inspect them. I had no part in the design of this board.

## License
AmiExtFDD is Copyright &copy; 2014-2015 by [RomanWorkshop](http://romanworkshop.blutu.pl).

All schematics and board layout files are licensed under the [Creative Commons Attribution-ShareAlike 4.0 license](https://creativecommons.org/licenses/by-sa/4.0/).

## Bill Of Materials
- Resistors:
  - R1-R3 - 2.2k
- Capacitors:
  - C1, C2 - 100n
- Integrated circuits:
  - U1 - 74LS74
  - U2 - 74LS38 (74LS00)
- Connectors:
  - CON-AMIGA - DB23M straight (male)
  - CON-FDD - IDC34M straight (male)
- Other:
  - J1-J3 - 3x1 jumper
  - J4 - 3x2 jumper
  - U1, U2 - DIP14 standard socket
