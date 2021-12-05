## How to Run ZBank Test Chain and Make a Test Transaction


Download [MyCrypto App](https://app.mycrypto.com/download-desktop-app) on your local machine 

1. Download geth-and-tools zip and extract into a new directory for this project
-   >[Windows 64 bit](https://gethstore.blob.core.windows.net/builds/geth-alltools-windows-amd64-1.9.7-a718daa6.zip)
-   >[Mac](https://gethstore.blob.core.windows.net/builds/geth-alltools-darwin-amd64-1.9.7-a718daa6.tar.gz)
    

2. Using the CLI, access the directory where you extracted the geth-and-tools zip and create accounts for two nodes for the network with a separate datadir for each using geth (remember to save the passwords and public and private keys)

-   >` ./geth --datadir node1 account new `

-   >` ./geth --datadir node2 account new`

3. Generate genesis block
    1. Run puppeth 
    >- `./puppeth`
    2. Name your network 
    >- `zbank_test_chain`
    3. Select option to configure new genesis block
    4. Choose proof-of-authority consensus algorithm
    5. Paste both account addresses from the first step one at a time into the list of accounts to seal.
    6. Paste them again in the list of accounts to pre-fund. There are no block rewards in PoA, so you'll need to pre-fund.
    7. You can choose `no` for pre-funding the pre-compiled accounts (0x1 .. 0xff) with wei. This keeps the genesis cleaner.
    8. Complete the rest of the prompts, and when you are back at the main menu, choose the "Manage existing genesis" option.
    9. Export genesis configurations. This will fail to create two of the files, but you only need `zbank_test_chain.json`.
    10. You can delete the `zbank_test_chain-harmony.json` file.

4. Initialize each node with the new `zbank_test_chain.json` with `geth`.

-   >`./geth --datadir node1 init zbank_test_chain.json`

-   >`./geth --datadir node2 init zbank_test_chain.json`

- ![Puppeth Config](./Screenshots/puppeth_config.png)
    
5. Run the first node, unlock the account, enable mining, and the RPC flag. Only one node needs RPC enabled.

-   >`./geth --datadir node1 --unlock "SEALER_ONE_ADDRESS" --mine --rpc --allow-insecure-unlock`

6. In a separate CLI window, set a different peer port for the second node and use the first node's `enode` address as the `bootnode` flag.

-   >`./geth --datadir node2 --unlock "SEALER_TWO_ADDRESS" --mine --port 30304 --bootnodes "enode://SEALER_ONE_ENODE_ADDRESS@127.0.0.1:30303" --ipcdisable --allow-insecure-unlock`

7. Use the MyCrypto GUI wallet to connect to the node with the exposed RPC port.

8. You will need to use a custom network, and include the chain ID, and use ETH as the currency.

10. Import the keystore file from the `node1/keystore` directory into MyCrypto. This will import the private key.

- ![Keystore Import](./Screenshots/keystore_import_mycrypto.png)

11. Send a transaction from the `node1` account to the `node2` account









