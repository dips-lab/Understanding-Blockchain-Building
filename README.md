
# Blockchain Building Blocks

### Ethereum network setup steps

1) Go to https://geth.ethereum.org/downloads/ and download the latest version of Geth & Tools.
![image](screenshots/geth.png)

2) Unpack the downloaded zipped folder and copy the contents of the folder to a desired working folder.
![image](screenshots/geth_folder.png)


3) Open terminal and browse to the working folder with the geth & tools.

4) Create accounts for two nodes for the network with a separate datadir for each.

```bash
./geth account new --datadir node1
./geth account new --datadir node2
```
![image](screenshots/node_keys.png)

5) Run puppeth, name the network puppernet(I used Dipsnet as puppernet was already setup for another wallet), and select the option to configure a new genesis block. Follow the same steps as below.

![image](screenshots/puppeth_config_1of2.png)


![image](screenshots/puppeth_config_2of2.png)

- Chain/Network Id is set to 333 (I had another network set to ID 888) 
- Block time is set to the default 15 seconds. 
- Block time explained: https://medium.facilelogin.com/the-mystery-behind-block-time-63351e35603a

6) With the genesis block creation completed, we will now initialize the nodes with the genesis' json file. 

    Using geth, initialize each node with the new dipsnet.json.

```bash
./geth init dipsnet.json --datadir node1
./geth init dipsnet.json --datadir node2
```

7) Now the nodes can be used to begin mining blocks.

    Run the nodes in separate terminal windows with the commands:
    
- Node 1:

```bash
./geth --datadir node1 --unlock “754dD9e178Eb6b93baDDDaD48ca45155566940a2” --mine --rpc --allow-insecure-unlock
```

- Node 2 in a separate terminal window:
    

```bash
./geth --datadir node2 --port 30304 --bootnodes "enode://2d4e714479e858c3ff9f5f9ebe0cf7996bde3e13645a045b57dd279a172424b76d53c999aacb31b443462c71e4e5c397e3095f781089426496489d7cb4a37432@192.168.8.54:30303"
```

- The --rpc flag enables us to talk to our second node, which will allow us to use MyCrypto or Metamask to transact on our chain.


- Since the first node's sync port already took up 30303, we need to change this one to 30304 using --port.


- The --bootnodes flag allows you to pass the network info needed to find other nodes in the blockchain. This will allow us to connect both of our nodes.

- In Microsoft Windows, we need to add the flag --ipcdisable due to the way Windows spawns new IPC/Unix sockets doesn't allow for having multiple sockets running from geth at once. Since we are only using RCP we can safely disable the IPC sockets.

![image](screenshots/both_nodes.png)

8) MyCrypto connection setup to local network. Network was previously setup before taking the screenshot, please ignore the displayed warning messages.

![image](screenshots/mycrypto_network.png)


9) End Result:

![image](screenshots/eth_transaction.png)