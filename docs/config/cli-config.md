# Configuring and provisioning a node with the [Meshtastic CLI](https://meshtastic.org/docs/software/python/cli/)

## Introduction

The Meshtastic Python-based CLI offers a faster way to provision a new Meshtastic device that does not require a dozen reboots and a Chrome-based browser with internet access.

This guide will, for now, focus on initial provisioning of a new device that is USB-connected, but will eventually incorporate other aspects of the CLI for maintenance and configuration using Bluetooth and LoRa OTA commands.

## Installing the Python CLI

Follow the instructions [here](https://meshtastic.org/docs/software/python/cli/installation/). (I skipped the serial drivers, the built-in macOS USB serial drivers met my needs.)

## One-shotting the device with YAML

If you use a YAML template, you can easily send a whole configuration to the device with one command using

`meshtastic --config <configfile.yaml>`

and it will ingest all the settings before doing a reboot.

There is a sanitized version of the file [here](./cli-config.md).

### Completing the YAML File and flashing it

0. Rename the file `zs[XX]config.yaml` where [xx] is the numeric designation of your node.
1. Replace anything that has been [REDACTED] with data from [here](./sensitive-credentials.md). As of the time of writing this will be the `channel_url`, `fixedPin`, and `adminKey` fields.
2. replace the [XX] in the `owner` and `owner short` fields with the numeric designation of your node. (e.g., `Zulu Siera 07` and `ZS07`, etc).
3. Save the file.
4. Run `meshtastic --config zs[XX]config.yaml` to send the configuration to the node and reboot it.

### Testing the new configuration

1. connect to the node with a Meshtastic client
2. Verify that a message sent to the LongFast channel from a different client shows up, and vice versa.
3. Verify that a message sent to the ZSNet channel from a different client shows up, and vice versa.

### Backing up the new node config

Run `meshtastic --export-config > zs[XX]-full-backup.yaml` to dump the full configuration. Keep this file [safe and secure](./sensitive-credentials.md) as you will need it in the future in case you need to factory default the node and reconfigure it from scratch

**Make sure to send the device's `privateKey` and `publicKey` to the other ZSNet admins so they can be recorded, and are not lost.**
