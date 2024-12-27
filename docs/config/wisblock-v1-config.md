# Wisblock Node v1 Config

## Step 0: Connect computer to USB-C port of Wisblock

## Step 1: Install current version of Meshtastic

<https://flasher.meshtastic.org> (only works from Chromium browsers) is probably the simplest method but this should eventually include a command-line method as well

Use the USB-C connection (on Linux/Mac it should present as /dev/cu.usbmodemsomething)

Send the most current Stable(beta) release to the device, let it reboot.

## Step 2: Configuration via <htttps://client.meshtastic.org>

0. Connect the web interface to either the Bluetooth or USB-C interface of the node.
1. From the left navbar: click the edit icon at the top of the navbar to edit the node name.
    - Long Name: `Zulu Sierra [number]` (example:  `Zulu Sierra 00`)
    - Short Name: `ZS[number]` (example: `ZS00`)
    - Click Save (Device will reboot, so reconnect to it)
2. From the left navbar: click on `Config` to enter the config options.
3. Device (From center navbar):
    - Role: select `Client` (look [here](https://meshtastic.org/blog/choosing-the-right-device-role/) for why this should almost never be set to `Router` or 'Repeater' unless the note is on a tower.)
    - Rebroadcast Mode: select `All`
    - LED Heartbeat Disabled: move slider to right to enable this, and disable the LED (it saves power)
    - Click the save icon in the top right (device may reboot)
4. Position:
    - Enable Smart Position: Disable
    - GPS Mode: `NOT PRESENT`
    - Fixed Position: Enable
    - Click the save icon in the top right (device may reboot)
5. Power:
    - Enable power saving mode: Enable
    - Click the save icon in the top right (device may reboot)
6. Network:
    - No changes here, make sure WiFi and Ethernet are both Disabled, save if needed.
7. Display:
    - No changes here
8. LoRa:
    - Region: `US`
    - Hop Limit: `3`
    - Frequency Slot: `20`
    - Ignore MQTT: Disable
    - OK to MQTT: Enable
    - Waveform Settings - Use Preset: Enable
    - Modem Preset: `Long Fast`
    - Radio Settings - Transmit Enabled: Enable
    - Transmit Power: `30`
    - Override Duty Cycle: Disable
    - Frequency Offset: `0`
    - Boosted Rx Gain: Enable
    - Override Frequency: `0`
    - Click the save icon in top right (device may reboot)
9. Bluetooth
    - Enabled: Enable
    - Pairing Mode: `Fixed Pin`
    - Pin: [Get the PIN from here](./sensitive-credentials.md)
    - Click Save, device may reboot. If you have BT-paired the device, you will need to Forget the old device from your computer or phone, and re-pair with the new PIN
10. Security (from center navbar)
    - Private Key: Click `Generate` Button
    - Public Key: Record the public key [here](./sensitive-credentials.md).
    - Allow Legacy Admin: Disable
    - Managed: Disabled (for now)
    - Admin Key: [Get the key from here](./sensitive-credentials.md)
    - Enable Debug Log API: Enable
    - Serial Output Enabled: Enable
    - Click Save, device may reboot.
11. Channels
    1. Automatic configuration method:
        - Channels (from left navbar)
        - In the top-right corner of the WebUI, click the "Download" icon
        - On the `Import Channel Set` screen, paste in the config URL. [Get the URL from here](./sensitive-credentials.mdsensitive-credentials.md)
        - Click Apply, device may reboot.
    2. Manual configuration method:
        - Channels (from left navbar)
        - `Ch 0` (from center navbar)
        - Role: `PRIMARY`
        - Pre-Shared Key: [Get the PSK from here](./sensitive-credentials.md)
        - Click the drop-down between the PSK field and the Generate button, set to `256 bit`
        - Name: `ZSNet`
        - Uplink Enabled: Disable
        - Downlink Enabled: Disable
        - Allow Position Requests: Enable
        - Precise Location: Enable
        - Approximate Location: `Within 350 m`
        - Click Submit, device may reboot
        - `Ch 1` (from center navbar)
        - Role: `SECONDARY`
        - Pre-Shared Key: `AQ==`
        - Click the drop-down between the PSK field and the Generate button, set to `8 bit`
        - Name: `ZSNet`
        - Uplink Enabled: Enable
        - Downlink Enabled: Enable
        - Allow Position Requests: Enable
        - Precise Location: Disable
        - Approximate Location: `Within 350 m`
        - Click Submit, device may reboot

At this point the radio is provisioned and ready to deploy.

## Considerations

This configuration is notably lacking a remote administration option. Remote (OTA-via-LoRa) is a required function for this network, but it involves maturity we dont yet have.  We need to get a collection of Meshtastic devices owned by the admins so we can record their public keys and load them as "Admin Keys" on the deployable nodes before this is ready to be added.

We also need to learn how to manage these devices remotely without accidentally bricking them before we go pushing buttons on devices that aren't easily resettable via USB.

I am currently in the process of experimenting with this, and I should have a plan in the next week or so.
