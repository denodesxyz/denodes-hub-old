---
description: 'Dymension: Roller Setup Guide'
---

# Roller Setup Guide

<figure><img src="../.gitbook/assets/Sub Roller.png" alt=""><figcaption></figcaption></figure>

Welcome to our guide on setting up your node and participating in the Dymension protocol testnet. Follow these step-by-step instructions to get started.

### Hardware Requirements <a href="#hardware-requirements" id="hardware-requirements"></a>

We recommend the following minimum hardware requirements for running the Avail Node:

* Machine: **16 GB+ RAM,** **Dual Core, 100 GB+ SSD**
* Network: **At least 100mbps network bandwidth**
* OS: **Linux AMD64, Linux ARM64, Mac AMD64, Mac ARM64**

### Install Roller

1. Run the following command:

```bash
curl -L https://dymensionxyz.github.io/roller/install.sh | bash
```

2. Verify Roller version:

```bash
roller version
```

{% code title="Should output:" %}
```
💈 Roller version v0.1.16-beta
💈 Build time: 2023-10-04T13:38:07+0000"
💈 Git commit: 57994323bdaea039b4ce7449b9f026f0059ba925
```
{% endcode %}

### Initialize RollApp

Initializing the configuration files of the RollApp will create the necessary information to start a new RollApp. This will create a folder `~/.roller` in the root directory of your computer with important files such as the `Genesis` file.

```bash
roller config init --interactive
```

* Select your network → **Froopyland (default)**
* Select your execution environment → **EVM RollApp (default)**
* Enter your RollApp ID → The rollapp ID, should contain only alphabetical characters. **Example**: **denodes**
* Specify your RollApp denom → Name of the native token of the RollApp in English letters. **Example**: **BTC, PEPE, DYM**
* Set the genesis token supply → Initial token supply in the RollApp **1,000,000,000 (default)**
* Choose your data layer → **Celestia: Arabica testnet**, **Avail: Dymension dedicated devnet**

### Address funding <a href="#address-funding" id="address-funding"></a>

After initializing the RollApp, addresses to fund should be returned to you:

{% code fullWidth="false" %}
```
🔑 Addresses:

Sequencer <network> | Address used to publish state updates to the Dymension Hub
Relayer   <network> | Address that handles the relaying of IBC packets
DA        <network> | Address used to publish data on-chain to the DA network
```
{% endcode %}

You can get these addresses at any time by executing the command:

```
roller keys list
```

The first two addresses need to be fund through the [froopyland-faucet](https://discord.com/channels/956961633165529098/1143231362468434022) channel in the Dymension discord:

```
$request <dym-address>
```

For Celestia and Avail network tokens you may use the [celestia-faucet](https://discord.com/channels/956961633165529098/1128048548999610451) or [avail-faucet](https://discord.com/channels/956961633165529098/1144240033650458685) respectively:

```
$request <celestia-address>
```

```
/deposit <avail-address>

```

### Registering the RollApp

Registering the RollApp adds a namespace in the Dymension Hub to account for the newly initalized RollApp.

Instead of managing a multi-sig smart contract, a developer only needs to register the RollApp with a simple command. Registering the RollApp to the Dymension Hub allows a Sequencer to publish state updates on-chain and furthermore facilitates bridging between ecosystems.

The following command utilizes the addresses generated in the [previous step](https://docs.dymension.xyz/build/quick-start/roller-quick/initialize) :

```bash
roller tx register
```

Should return:

```
💈 Rollapp '<rollapp-id>' has been successfully registered on the hub.
```

### Running the RollApp

There are two ways to run RollApp. In the first case it is enough to execute the command:

```
roller run
```

During the `Run` process a RollApp with an IBC connection to the Dymension Hub is started. A status table will appear with information about the RollApp and IBC relayer. Developers should see an output with useful information such as this:

<figure><img src="../.gitbook/assets/Screenshot 2023-10-09 at 4.53.41 PM.png" alt=""><figcaption></figcaption></figure>

If you close the terminal, the process execution will be stopped. Therefore, it is recommended to use the following method. It only works on Linux with systemd.

Creating service files:

```bash
roller services load
```

Enable services:

{% code title="Celestia" %}
```bash
sudo systemctl enable da-light-client sequencer relayer
```
{% endcode %}

{% code title="Avail" %}
```bash
sudo systemctl enable sequencer relayer
```
{% endcode %}

Start the services:

{% code title="Celestia" %}
```bash
sudo systemctl start da-light-client sequencer relayer
```
{% endcode %}

{% code title="Avail" %}
```bash
sudo systemctl start sequencer relayer
```
{% endcode %}

Next, check the status of running services

{% code title="Celestia" %}
```bash
sudo systemctl status da-light-client sequencer relayer
```
{% endcode %}

{% code title="Avail" %}
```bash
sudo systemctl status sequencer relayer
```
{% endcode %}

The status of all services should be **active (running)**.

### Monitor

### IBC Transfer

### Export keys

### Portal Listing











***

_Powered by_ [_deNodes_](https://twitter.com/deNodes\_)