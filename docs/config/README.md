# Configuration of nodes

For the initial configuration guidance, I've decided to stick with the web UI for Meshtastic, which is simply <https://client.meshtastic.org>.  This is simple and easy enough for everyone to gain a good understanding of how a node gets configured, without requiring a lot of front-end dependencies. It suffers only from:

- Needing working internet access to get the config interface to come up
- Needs a Chromium-based (Chrome/Chromium/Edge/etc) browser to connect to the USB port or Bluetooth via the browser

Config instructions for the v1 node (WisBlock-based) [are here](./wisblock-v1-config.md).

The Python environment has about the average level of PITA dependencies to set up but has the advantage over the WebUI of not requiring working Internet access to load the configuration interface.

Python CLI configuration instructions for a new node [are here](./cli-config.md).

