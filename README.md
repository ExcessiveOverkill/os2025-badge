Open Sauce 2025 Badge
=====================

Assembly, parts, usage, user programming, and other information:

* https://opensauce.com/badge-25/
* https://www.digikey.com/en/maker/tutorials/2025/assembling-your-2025-open-sauce-badge


Additional information
----------------------

After flashing `os_2025.hex` to your ATtiny85, the chip's fuses need to be configured for correct operation. Warning:
after setting fuses as described below, you will be unable to re-program your ATtiny or change additional fuses without
the use of high voltage programming!

**Programming with AVRDUDE**

This is assuming you are using a USBASP programmer - unofficial, cheap, but not an Atmel product.

```
avrdude -c usbasp -p t85 -U flash:w:os_2025.hex:i
```

**Fuse setting with AVRDUDE**

The following command sets appropriate fuses:

```
avrdude -c usbasp -p t85 \
    -U lfuse:w:0xE2:m \
    -U hfuse:w:0x5F:m \
    -U efuse:w:0xFF:m \
    -U lock:w:0xFF:m
```

The fuses required are - described as what changes from the defaults:

| Fuse     | Setting | Comment                                       |
|----------|---------|-----------------------------------------------|
| Low      | 0xE2    | Clear CKDIV8 - run cpu at full 8MHzC          |
| High     | 0x5F    | Set RSTDISBL - reconfigure reset pin as GPIO* |
| Extended | 0xFF    | default                                       |
| Lock     | 0xFF    | default                                       |

\* Warning, after setting fuses as described above, you will be unable to re-program your ATtiny or change additional
fuses without the use of high voltage programming!
