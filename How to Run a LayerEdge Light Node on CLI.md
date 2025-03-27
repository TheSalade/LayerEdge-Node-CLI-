# LayerEdge Node CLI Setup Guide

This is a step-by-step tutorial to set up and run a LayerEdge light node using the command line. Whether you're a beginner or an experienced user, this guide will help you get your node up and running on a VPS.

  ![image](https://github.com/user-attachments/assets/11bdeea0-99de-48bc-b84f-2c29aa313b6d)

---


## Step 1: Setting Up Your VPS

You can choose CLOUP VPS 2 on Contabo : https://www.tkqlhce.com/click-101114590-13484397

![image](https://github.com/user-attachments/assets/a18d3037-3969-49c1-a546-cd8ad9cb5091)

Choose **Ubuntu 22.04** as your operating system during setup.

![image](https://github.com/user-attachments/assets/ede1b20f-fec9-42df-90ef-462d5dcf187b)


---

## Step 2: Connect to Your VPS

- Open your terminal and connect to your VPS using SSH:
   ```bash
   ssh root@<IP_OF_YOUR_VPS>

## Step 3: Setup your LayerEdge node
Go to https://dashboard.layeredge.io/ and register your wallet

![image](https://github.com/user-attachments/assets/001d6c58-646f-4351-9879-58806ae838b4)

- Update your system

 ```
    sudo apt update && sudo apt upgrade -y
 ```
- Install screen
```
   sudo apt install screen
```
- Create a new screen session
```
screen -S layeredge
```
- Install Go
```
curl -OL https://go.dev/dl/go1.21.0.linux-amd64.tar.gz
sudo rm -rf /usr/local/go
sudo tar -C /usr/local -xzf go1.21.0.linux-amd64.tar.gz
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.bashrc
source ~/.bashrc
```
- Check Go version
```
go version
```
- Install Rust
```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source $HOME/.cargo/env
```
- Check Rust Version
```
rustc --version
```
- Install Risc0 Toolchain
```
curl -L https://risczero.com/install | bash && rzup install
echo 'export PATH=$PATH:/root/.risc0/bin' >> ~/.bashrc
source ~/.bashrc
```
- Clone the Light Node Repository
```
git clone https://github.com/Layer-Edge/light-node.git
cd light-node
```
- Open .env file
```
nano .env
```
- Modify .env file with this content, make sure to modify PRIVATE_KEY
```
GRPC_URL=grpc.testnet.layeredge.io:9090
CONTRACT_ADDR=cosmos1ufs3tlq4umljk0qfe8k5ya0x6hpavn897u2cnf9k0en9jr7qarqqt56709
ZK_PROVER_URL=http://127.0.0.1:3001
# Alternatively:
ZK_PROVER_URL=https://layeredge.mintair.xyz/
API_REQUEST_TIMEOUT=100
POINTS_API=https://light-node.layeredge.io
PRIVATE_KEY='cli-node-private-key'
```
- Save the file with CTRL+X write Y press Enter

- Start the merkle service
```
cd risc0-merkle-service
cargo build && cargo run
```
- When you see Starting server on port 3001…

=> Leave the screen with CTRL+A+D

- Create another screen session
```
screen -S layeredge2
```
- Build and Run the LayerEdge Light Node
```
cd light-node
go build
./light-node
```
- Leave the screen with CTRL+A+D

Go to https://dashboard.layeredge.io/ and check if you’re node is running

![image](https://github.com/user-attachments/assets/aa00215a-cc55-4f72-8aaa-3f3dbdc31a0a)



Thank’s for reading
If you need help you can join Discord : https://discord.com/invite/szXyZSgSYg
Twitter : https://x.com/TRTtheSalad
Disclaimer : Not a financial Advice an education tutorial do your own research

