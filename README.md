# Ultra Affordable EFI

🟢[$175 base model rusEFI store](https://www.shop.rusefi.com/shop/p/uaefi-ultra-affordable-efi)🟢

## Community Support

🔴Community support ONLY 🔴 https://www.facebook.com/groups/rusEfi 🔴 [Discord](https://github.com/rusefi/rusefi/wiki/Discord)🔴 [Commercial Support](https://www.shop.rusefi.com/shop/p/details-about-rusefi-ecu-technical-support) 🔴

## Technical Details

Open Source KiCAD hardware powered by [Hellen-One](https://github.com/andreika-git/hellen-one)

Powered by [rusEFI firmware](https://github.com/rusefi/rusefi)

[User Documentation](https://github.com/rusefi/rusefi/wiki/uaEFI)

![x](https://raw.githubusercontent.com/rusefi/uaefi/master/docs/uaefi-a-top.png)

![x](https://raw.githubusercontent.com/rusefi/uaefi/master/docs/uaefi-a-back.png)

## MCU options

1mb of flash is _required_.

One day we shall try https://jlcpcb.com/partdetail/Stmicroelectronics-STM32F427VIT6%2FC57097#EC or https://jlcpcb.com/partdetail/Stmicroelectronics-STM32F437VIT7%2FC1338578#EC

## rusEFI Store

https://www.shop.rusefi.com/shop/p/uaefi-ultra-affordable-efi

## HOWTO JLCPCB

You would need three files from ``boards/uaefi-a/board`` folder to place your JLCPB Assembly order: gerber.zip BOM-JLC.csv and CPL.csv


### Q: having trouble with opening uaefi board project. library path seems ok, i do not know how to solve missing modules issue

A: missing modules are closed source. they are filled in by github magic
github magic combines gerbers and spits out a complete bom/pcl/new gerbers to upload to jlc/friends. See https://github.com/rusefi/hellen-one/tree/master?tab=readme-ov-file#tldr for more info

### Q: Magic modules? How do I see schematics of those?

A: https://github.com/rusefi/hellen-one has full documentation for each module

### Q: Something wrong with BOM?

A: Nope, that's normal nothing to worry about click 'Continue'.

![image](https://github.com/rusefi/uaefi/assets/48498823/1b708b27-13b7-40da-857d-7ef85a8ad960)

### Q: how do I get more RAM for Lua?

A: fabricate with STM32F42xVI firmware would defect extra RAM and give you extra Lua. Once your script does not fit into STM32F42xVI it's F7 time or help us leverage F413.

### Q: I've place an order with JLCPCB and I see scary looking wrong orientation?

A: that's expected. See [boards/uaefi-c/board](boards/uaefi-c/board) ``Original*.png`` files and ``Produce*.png`` after JLCPCB manual review process.

## Bluetooth power issue fix

It was found that board with installed BT module may be affected by power issue.

During power on BT module consume too much inrush current on 3.3V line causing 3.3V drop below MCU reset hreshold. This may lead to unstable start or infinity reset loop.

To fix this please install additional capacitors to 5V and 3.3V powerlines.

Polarized electrolytic capacitors with at least 10V rating and extended temperature range are recommended. Tantalum and solid electrolytic capacitors are also suitable.

**Please carefully follow illustrated polarity.**

33..47uF should be added to 5V powerrail. [This](https://www.digikey.com/en/products/detail/w%C3%BCrth-elektronik/860020372004/5727028) or [this](https://www.digikey.com/en/products/detail/w%C3%BCrth-elektronik/860080372001/5727224) or [any of these](https://www.digikey.com/en/products/filter/aluminum-electrolytic-capacitors/58?s=N4IgjCBcpgbFoDGUBmBDANgZwKYBoQB7KAbRAGYBOAJnOoAYQBdAgBwBcoQBldgJwCWAOwDmIAL4FYlBCGSR02fEVIgALGDAAOSgHZmbTpB79hYyeEo7Z8xbgLFIZRkwsM1M6HNSZ7Kp%2Bq6AAQArQBiBiAcXACqQgLsAPIoALI4aFgArnw4EgQMup5IPkoOqnBBAGqR0cZxCclpGdm5FgC01DZQ-JnKjmQArMzibqpqwZkoQXAAbsNAA).

![photo_2025-10-21_10-22-45](https://github.com/user-attachments/assets/7ddaa8e7-37e0-40ae-88a0-fa5ab64d6386)

And 220..470uF should be added to 3.3V powerrail. [This](https://www.digikey.com/en/products/detail/w%C3%BCrth-elektronik/860010273011/5726952) or [this](https://www.digikey.com/en/products/detail/w%C3%BCrth-elektronik/860020273011/5727148) or [any of these](https://www.digikey.com/en/products/filter/aluminum-electrolytic-capacitors/58?s=N4IgjCBcpgbFoDGUBmBDANgZwKYBoQB7KAbRAGYBOAJnOoAYQBdAgBwBcoQBldgJwCWAOwDmIAL4FYlBCGSR02fEVIgALGDAAOSgHZmbTpB79hYyeEo7Z8xbgLFIZRkwsM1M6HNSZ7Kp%2Bq69AAEAK0AYgYgHFwAqkIC7ADyKACyOGhYAK58OBIEDLqeSD5KDqpgIQBqUTHG8Ykp6Zk5eRYAtNQ2UPxZyo5kAKzM4qNAA).

![photo_2025-10-21_10-22-50](https://github.com/user-attachments/assets/d94e34c5-9f30-4abf-9085-91c20cea7fc0)


## HOWTO EGT chip

This board has a placeholder for MAX31855 (or MAX6675) termocouple-to-digital chip. **This chip is not populated by default!**

<img width="1061" height="553" alt="Screenshot from 2025-09-26 11-15-15" src="https://github.com/user-attachments/assets/5a5db5be-c184-4fea-9b31-ffddb2f7b5a9" />

D8 is **optional** ESD protection and also is not populated by default. You need to solder U4 only, D8 is optional. All passive components are already populated.

**MAX31855** works without addtional modification.

For **MAX6675** connect EGT- to GNDA either on J2 "C" connector or just short C28 (replace with 0R).

<img width="588" height="521" alt="Screenshot from 2025-09-26 11-19-41" src="https://github.com/user-attachments/assets/0cf99712-3a90-4c1d-994f-c72283389419" />

## [EXPERIMENTAL] How to make MAX9924 work with low tooth count trigger wheel

In some cases user may need two VR inputs on UAEFI and both trigger wheels are low-tooth count.

In default configuration MAX9924 does not work with low count trigger wheels because of its "adaptive peak threshold" and its watchdog.

<img width="470" height="554" alt="Screenshot from 2025-10-12 16-58-30" src="https://github.com/user-attachments/assets/d868c44c-c477-4ae1-806f-a2882cb111ef" />

On UAEFI MAX9924 is configured in **A2 mode**.

<img width="932" height="215" alt="Screenshot from 2025-10-12 16-59-49" src="https://github.com/user-attachments/assets/65111187-c274-4829-9ff7-c9cb2b85e4f4" />

**B mode** allow use of MAX9924 with low count trigger wheels. But external Bias and Thresholt voltages should be allpied. Both can be sources from UAEFI Discrete VR module.

List of modifications:
1. pin 6: ZERO_EN connect to VCC instead of GND.
2. pin 4: supply 2.5 V instead of GND
3. pin 8: EXT, supply external threshold voltage

Pins 4 and 6 needs to be lifted from PCB to be disconnected from GND. Pin 8 initially is not connected to any circuit.

Use hot air gun to de-solder whole chip. Then twist pins 4 and 6 up so both do not touch PCB. Then solder chip back to PCB

Now use thin wire to connect:
1. pin 6 to pin 10 of the same chip.
2. pin 4 to **Vref** at R769 + C754. See file:///home/work/rusefi/docs/uaefi-d-ibom.html for its locations
3. pin 8 to **thresh_high** at U756 pin 1. See file:///home/work/rusefi/docs/uaefi-d-ibom.html for its locations

![photo_2025-10-12_11-40-24](https://github.com/user-attachments/assets/d103b3f7-429a-4be8-9031-adfdd35b5004)

Now MAX9924 VR input uses same threshold vs RPM settings that is set for Descrete VR input. And it is cabable to work with low tooth count trigger wheels without noise issues.
