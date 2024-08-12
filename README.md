# Storage-Node-Deployment-Guide
This guide provides detailed steps for deploying the 0G System's Storage Node, which consists of multiple components with specific functionalities.

### **Prerequisites**

- **Storage Node**
- **Storage Node CLI**

### **Introduction**
The 0G Storage Node interacts with on-chain contracts for blob root confirmation and PoRA mining. For official deployed contract addresses, please visit the relevant official documentation page.

### **Hardware Requirements**
|Key|Value|
|:--|:----|
|**Memory:**|16 GB RAM|
|**CPU**|4 cores|
|**Disk:**|500GB to 1TB NVMe SSD|
|**Bandwidth:**|500 MBps for both Download and Upload|

### **Deployment Steps**

#### **1. Install Dependencies**

- **For Linux:**
    ```bash
    sudo apt-get update
    sudo apt-get install clang cmake build-essential
    ```

- **For Mac:**
    ```bash
    brew install llvm cmake
    ```

#### **2. Install Rust**
   ```bash
   curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
   ```

#### **3. Install Go**

- **For Linux:**
    ```bash
    # Download the Go installer
    wget https://go.dev/dl/go1.22.0.linux-amd64.tar.gz

    # Extract the archive
    sudo rm -rf /usr/local/go && sudo tar -C /usr/local -xzf go1.22.0.linux-amd64.tar.gz

    # Add Go to your PATH
    export PATH=$PATH:/usr/local/go/bin
    ```

- **For Mac:**
    ```bash
    brew install go
    ```
   Alternatively, download the Go installer from the official [Go download page](https://go.dev/dl/). Open the package file and follow the prompts to install.

#### **4. Download the Source Code**
   ```bash
   git clone -b v0.4.0 https://github.com/0glabs/0g-storage-node.git
   ```

#### **5. Build the Source Code**
   ```bash
   cd 0g-storage-node
   git submodule update --init

   # Build in release mode
   cargo build --release
   ```

#### **6. Configure the Node**

Edit the `run/config.toml` file if necessary:
- **enr address**: Set your instance's public IP to support peer discovery.
- **peer nodes**: Modify the provided node IPs if needed.
- **flow contract address**: Set the address.
- **mine contract address**: Set the address.
- **blockchain RPC endpoint**: Specify the RPC endpoint.
- **log sync start block number**: Specify the starting block number.
- **miner key**: Enter your private key for PoRA mining.
- **db_max_num_chunks**: Set the maximum number of chunk entries to store.

#### **7. Run the Storage Service**

Use the following commands to start the service:

```bash
cd run

# Consider using tmux to run the node in the background
../target/release/zgs_node --config config-testnet.toml --miner-key <your_private_key> --blockchain-rpc-endpoint <blockchain_rpc> --db-max-num-chunks <max_chunk_num>
```

### **You’re All Set!**

Follow the steps above, and your 0G Storage Node should be up and running successfully.

--- 

This version preserves the functionality while streamlining the instructions and improving readability.
