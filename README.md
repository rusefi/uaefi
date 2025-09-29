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

## HOWTO EGT chip

This board has a placeholder for MAX31855 (or MAX6675) termocouple-to-digital chip. **This chip is not populated by default!**

<img width="1061" height="553" alt="Screenshot from 2025-09-26 11-15-15" src="https://github.com/user-attachments/assets/5a5db5be-c184-4fea-9b31-ffddb2f7b5a9" />

D8 is **optional** ESD protection and also is not populated by default. You need to solder U4 only, D8 is optional. All passive components are already populated.

**MAX31855** works without addtional modification.

For **MAX6675** connect EGT- to GNDA either on J2 "C" connector or just short C28 (replace with 0R).

<img width="588" height="521" alt="Screenshot from 2025-09-26 11-19-41" src="https://github.com/user-attachments/assets/0cf99712-3a90-4c1d-994f-c72283389419" />
