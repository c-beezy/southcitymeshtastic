# Observations about Meshtastic hardware ecosystem

In recent weeks I have picked up a collection that is representative of the current offerings for devices that run Meshtastic:

- Heltec v3 (ESP32)
- Heltec T114 (NRF52)
- LILYGO T-Echo (NRF52)
- LILYGO T-Deck (ESP32)
- RAK WisBlock 19007 (NRF52)
- RAK WisBlock Mini 19003 (NRF52)

After evaluating these boards and assembling functional handheld and fixed Meshtastic nodes with them, it is my conclusion that the NRF52 platform is the preferred SOC family to use for all meshtastic nodes due in large part to the vastly increased power requirements of ESP32-based Meshtastic boards.

In the future, the only times I will choose an ESP32 system is if it will be in a fixed location that always has external power like a (desktop or an attic device) that will not be reliant on either solar or battery power to function, or when external considerations specific to the particluar board (like the keyboard on the T-Deck) offer a compelling reason to put up with the bad performance and high power drain of an ESP32 SOC.

Currently the Heltec T114 board is my favorite handheld Meshtastic device and what I will be using for all Meshtastic builds in the future.

## SoC Families


| Feature | ESP32 | NRF52| Winner |
| ------ | ------- | ------ |
| Idle Power (as tested) | .5W (heltec v3) | 0.003W (T114) | NRF52 |
| Max Power  |  |  |  |
| Coremark CPU | 660 | 215 | ESP32 |
| Bluetooth | 4.x | 5.x | NRF52 |
| WiFi | Yes | No | ESP32 |
| Cost | Low | High | ESP32 |

## ESP32

ESP32 boards like the Heltec v3 have a main advantage in that the low cost of the boards make them a popular choice for a first project, but the limitations of the platform rapidly cause frustration later on when integrating the board into a complete user device. The power drain is many times what a NRF52-based board will require, which necessitates larger batteries and results in a bulkier device for handhelds, and also requires a much larger solar panel than a NRF52 device would need to self-power.

In my direct experience, a battery that can power a NRF52 device for several days will fall short of powering an ESP32 device for a full day. They are comparatively extremely power hungry.

Meshtastic does a poor job of utilizing the ESP32's baked-in WiFi functionality, and it should be discounted as an added benefit for most Meshtastic applications unless someone has a specific project requimement to utilize it.

### Heltec v3 

The Heltec v3 is a tiny ESP32 board that is extremely low-cost. Like most others my first Meshtastic experience was buying a pair of these on amazon to play with.  The boards are certainly capable but the battery drain on portable devices makes them chunky and shorter-lived than they should be.  I might re-use a Heltec board as a USB-powered desktop node in the future but these are my least favorite Meshtastic-capable device at the current time. 

### LILYGO T-Deck

The T-Deck is a notable ESP32 standout because it has singular functionality among Meshtastic hosts in that it does not require a paired Bluetooth host or phone running the Meshtastic app to make use of Meshtastic networks. The enhanced performance of the ESP32 makes it a logical choice for this use-case even though the power drain is problematic.

Once the new on-device Meshtastic client becomes better-supported, this device might become my go-to handheld device.

## NRF52

On a hardware level, the NRF52 is a lower spec CPU vs the ESP32 with a concurrently lower power draw.  If the Meshtastic project made better use of WiFi this would be a differentiator, but Meshtastic is laser-focused on using BLE to talk to devices so the WiFi capabilities of the ESP32 are an afterthought at best.

### RAK WisBlock

The WisBlock family of NRF52 boards are a modular family of systems that allows for dozens of hardware capabilities to be easily snapped onto a baseboard via hardware modules with proprietary socketed connectors. This is far easier than soldering to header pins but comes at an increased cost that in some cases is hard to justify. (as an example, their socketed GNSS module costs 3x what other modules do). Wisblock has the distinction of being one of the few boards that doesnt ship by default with a display, it must be ordered for an additional fee. Both Bluetooth and Lora radios have external antenna connectors, and BLE performance is much improved vs other devices with the RAK-supplied full antenna. 

I started out absolutely loving the WisBlock boards and have so far built 2 solar-powered outdoor nodes using them, one with a WisBlock 19007 and one with a WisBlock Mini 19003. While the 19007 has been very straightforward to work with, the 19003 has undergone some changes that enhance usability with the proprietary RAK modules while making it harder to integrate devices via the header pins. Due to this difficulty, I have decided to not ever use a 19003 baseboard again, and will only use the 19007 moving forward. 

### LILYGO T-Echo

The T-Echo with an e-ink display is probably the lowest-power device with a display that has yet been made available for Meshtastic use. For new users this is my default device reccomendation as it comes out of the box ready to go and has good performance and longevity. Having an external antenna is an immediate benefit.

### Heltec T114 

The T114 is something I have only recently started working with but my experience is completely positive at this time. This NRF52 board is relatively cheap, can be purchased either with or without a large and bright color OLED, and is the same tiny size as the Heltec v3 board.

I am planning on building a few outdoor solar nodes using the no-display T114 board, and the large display makes it a good contender for desktop nodes that can be read from farther away than something like the Heltec V3.

Once more printable T114 cases become available, I predict this board will become a popular choice for portable devices.