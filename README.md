# Babylon Node Deployment
This repository contains Ansible scripts for the installation, updating, and removal of a Babylon node on Linux systems. The playbooks are designed to simplify the process of setting up a Babylon node, managing its services, and ensuring seamless node operations.

## Prerequisites
A Linux system (Ubuntu 22.04 LTS recommended) with Docker installed.
Root access on your machine.
Git and Ansible version 2.15 or newer installed.
Getting Started
Step 1: Installing Dependencies
Update your system's package list and install necessary tools:

```
sudo apt update && sudo apt upgrade -y
sudo apt install ansible git -y
```
##  Step 2: Downloading the Project
Clone this repository to access the Ansible playbook and all necessary files:

```
git clone https://github.com/nodemasterpro/deploy-node-babylon.git
cd deploy-node-babylon
```

## Step 3: Installing Babylon Node
Execute the playbook using the following command, specifying the 'moniker' (node name) as an extra variable:

```
ansible-playbook install_babylon_node.yml -e moniker="your_node_name"
```
Note: Replace "your_node_name" with the unique name you wish to assign to your node.

## Step 4: Viewing Node Logs
To view the logs for the Babylon node:

```
journalctl -u babylon-node -f -o cat
```

## Step 5: Creating a Babylon Wallet
After installing the node, create a Babylon wallet essential for network operations:

```
ansible-playbook create_babylon_wallet.yml
```

## Step 6: Requesting Testnet Funds
After obtaining the wallet address from the playbook execution, visit the Babylon testnet faucet to request funds:

Join the Babylon Discord server and go to the #faucet channel. Type !faucet <wallet_address> to claim test tokens.

## Step 7: Checking Node Synchronization
To ensure your node is fully synchronized with the Babylon blockchain, execute:

```
babylond status | jq
```
Wait for 30 minutes to an hour for the node to synchronize. When the 'catching_up' variable is set to false, your node is synchronized.

## Step 8: Creating the Validator and Linking to the Wallet
Execute the following playbook to create a validator and link it to your wallet:

```
ansible-playbook register-babylon-node.yml
```

During this step, you will be prompted to input the following information:

Moniker: "node_name"
Details: "a sentence of your choice"
Website: "your website"

## Step 9: Viewing Validator State
You can check the status of your validator by executing:

```
babylond query staking validator <wallet_address>
```
Note: Replace "<wallet_address>" with your validator's wallet address provided at the end of the playbook execution.

## Additional Information
Stopping Services
To stop the Babylon node:
```
sudo systemctl stop babylon-node
```

Starting Services
To start the Babylon node:
```
sudo systemctl start babylon-node
```

Removing the Babylon Node
To remove the Babylon node, run the playbook again with the action set to remove:
```
ansible-playbook remove_node_babylon.yml
```
Ensure to back up any important data before removing the node, as this action may delete node data.