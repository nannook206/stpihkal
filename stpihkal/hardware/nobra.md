# Nobra

## Introduction

[Nobra](https://www.nobra.de/?lang=en) is a company run by a couple
from Germany that has been selling vibrators since 1999. It offers
both insertable vibrators as well as a male vibrator with two motors
(“Nobra Twincharger”).

The vibrators can be connected to either an analog control box or a
digital control box. In addition to the buttons, the digital control
box can also be controlled via Bluetooth using the official
“NobraControl” application (uses .NET Framework).

## Bluetooth details

The digital control box identifies itself as `Nobra Control` via
Bluetooth 2.0. When paired with a system using the key `1234`, it
exposes two serial ports, COM4 and COM5. However, only COM5 can be
used to control the toy.

## Protocol

When switching on the digital control box, it waits for five seconds
and then switches into manual mode, using the stored setting. This
can either be a steady vibration or an oscillating vibration in a
sinusoidal, sawtooth or rectangular shape.

Upon receiving a command via Bluetooth, the control box will stop
the oscillation and change to the vibration level as indicated by
the command, or keep the vibration constant at whatever is the
current level if the command specifies no vibration level.

A user can press the physical buttons on the control box at any time
to go back to manual control. In addition, they can press a specific
button combination to turn Bluetooth invisible, however the control
box will still accept commands from previously paired devices.

### Command list

A command is a one-byte message. Commands `0x41` to `0x45` (`'A'`
through `'F'`) are systems commands, while `0x61` to `0x70` (`'a'`
through `'p'`) change the vibration level.

Even though some Nobra toys contain two motors, these commands will
set both motors to the same vibration level. The only way to control
the vibration for each motor separately is via the physical dials.

| Byte | Char | Result |
| ------ | ----- | ----------- |
| `0x41` | `'A'` | The control box will return its identifier as five bytes: `NoBra` (`4E 6F 42 72 61`).
| `0x42` | `'B'` | Puts the control box into a “frozen” state: The vibration stays at the current level and any further Bluetooth commands or physical button presses are ignored until the power is turned off and on again. This command might be used to store a new oscillation pattern in the control box.
| `0x43` | `'C'` | Same as `0x42` (`'B'`).
| `0x44` | `'D'` | The control box returns the stored oscillation pattern encoded in 36 bytes, e.g.: ``dpAabcdcbapNOdpRdpFGHIJKLMNO_`dpAphd`` (`64 70 41 61 62 63 64 63 62 61 70 4E 4F 64 70 52 64 70 46 47 48 49 4A 4B 4C 4D 4E 4F 5F 60 64 70 41 70 68 64`)
| `0x45` | `'E'` | Same as `0x44` (`'D'`).
| `0x46` | `'F'` | Reboots the control box. Turns off all vibrations for five seconds before it switches the vibration to the stored setting. After reconnecting via Bluetooth, further commands can be sent to the control box.
| `0x61` | `'a'` | Sets the vibration to the lowest level (1).
| `0x62` | `'b'` | Sets the vibration level to 2.
| `0x63` | `'c'` | Sets the vibration level to 3.
| `0x64` | `'d'` | Sets the vibration level to 4.
| `0x65` | `'e'` | Sets the vibration level to 5.
| `0x66` | `'f'` | Sets the vibration level to 6.
| `0x67` | `'g'` | Sets the vibration level to 7.
| `0x68` | `'h'` | Sets the vibration level to 8.
| `0x69` | `'i'` | Sets the vibration level to 9.
| `0x6A` | `'j'` | Sets the vibration level to 10.
| `0x6B` | `'k'` | Sets the vibration level to 11.
| `0x6C` | `'l'` | Sets the vibration level to 12.
| `0x6D` | `'m'` | Sets the vibration level to 13.
| `0x6E` | `'n'` | Sets the vibration level to 14.
| `0x6F` | `'o'` | Sets the vibration to the highest level (15).
| `0x70` | `'p'` | Turns off the vibration (level 0).

Any bytes missing from this table cause the oscillation from manual
mode to stop at whatever is the current vibration level but do not
have any other effect.

## Related links

* Official website and shop (English): [https://www.nobra.de/?lang=en](https://www.nobra.de/?lang=en)
* Documentation of the digital control box: [https://www.nobra.de/digital-control/?lang=en](https://www.nobra.de/digital-control/?lang=en)
* Documentation of the official companion app for Windows: [https://www.nobra.de/digital-control/nobracontrol-rhythmus-und-soundsteuerung/?lang=en](https://www.nobra.de/digital-control/nobracontrol-rhythmus-und-soundsteuerung/?lang=en)
* US store selling the Nobra Twincharger: [http://www.happystim-usa.com/catalog/i553.html](http://www.happystim-usa.com/catalog/i553.html)
