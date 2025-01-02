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

## SoC Family

## ESP32

ESP32 boards like the Heltec v3 have a main advantage in that the low cost of the boards make them a popular choice for a first project, but the limitations of the platform rapidly cause frustration later on when integrating the board into a complete user device. The power drain is many times what a NRF52-based board will require, which necessitates larger batteries and results in a bulkier device for handhelds, and also requires a much larger solar panel than a NRF52 device would need to self-power.

In my direct experience, a battery that can power a NRF52 device for several days will fall short of powering an ESP32 device for a full day. They are comparatively extremely power hungry.

Meshtastic does a poor job of utilizing the ESP32's baked-in WiFi functionality, and it should be discounted as an added benefit for most Meshtastic applications unless someone has a specific project requimement to utilize it.

The T-Deck is a notable ESP32 standout because it has singular functionality among Meshtastic hosts in that it does not require a paired Bluetooth host or phone running the Meshtastic app to make use of Meshtastic networks. For now, the on-device client remains a killer feature that has definite value, but it is crippled by the size of the battery that must be integrated with the T-Deck to get it through a day, and a multi-day battery for a T-deck is something in the 5000-mAh range and makes the finished device into something the size of a cell phone from 30 years ago. Its wifi offers no compelling benefit and should, like the wifi in the Heltec v3, not be a concern unless a specific project requires it.

Hopefully LILYGO will release a NRF52-based T-Deck in the future.

