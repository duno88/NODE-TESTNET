<p align="center">
  <img height="50" height="auto" src="https://user-images.githubusercontent.com/38981255/184088981-3f7376ae-7039-4915-98f5-16c3637ccea3.PNG">
</p>


> [Docs](https://docs.inery.io/docs)

> [Portal](https://testnet.inery.io/)

> [Explorer Inary](https://explorer.inery.io/ "Explorer Inary")

If you haven't registered, please register [here](https://testnet.inery.io/)

# Install Become a Master Node

## Minimum Spec Hardware :
NODE  | CPU     | RAM      | SSD     | OS     |
| ------------- | ------------- | ------------- | -------- | -------- |
| Inery | 4          | 8         | 250  | Ubuntu 20.04 LTS  |


## Update Inery-node 
* If you haven't run node inery before skip to step Download Inery node
* Stop Node
  ```console
  cd $HOME/inery-node/inery.setup/master.node
  ./stop.sh
  ```
  Check 
  ```console
  pidof nodine
  ```
    Execute Stop 
  ```console
  kill -15 <pid>
    ```
    OR
   ```console
  kill -s SIGKILL $(pidof nodine)

  ```

* Delete Folder Inery node
  ```console
  cd $HOME
  rm -rf inery-node
  ```

* Download Inery node
  ```console
   git clone  https://github.com/inery-blockchain/inery-node
  ```

* Goto Folder `inery.setup`
  ```console
   cd inery-node/inery.setup
  ```

* executable `ine.py`
  ```console
  chmod +x ine.py
  ```

* Export path
  ```console
  ./ine.py --export
  ```

* Load path
  ```console
  source $HOME/.bashrc
  ```

* Config Edit
  ```console
  nano tools/config.json
  ```
  Cari `MASTER_ACCOUNT` lalu ubah value seperti berikut
  | Variable | Data |
  |-----------|------------|
  |NAME|Inery Account|
  |PUBLIC_KEY|Public Account|
  |PRIVATE_KEY|Privaet Account|
  |PEER_ADDRESS|127.0.0.1:9010|

 Save <kbd>CTRL</kbd>+<kbd>x</kbd>+<kbd>y</kbd>

* Run node
  ```console
  ./ine.py --master
  ```

* Check log node
  ```console
  tail -f master.node/blockchain/nodine.log
  ```

* If it's syncron run`start.sh`
```console
./master.node/start.sh
```

* Request Faucet in [Dashboard](https://testnet.inery.io/dashboard/)

* Register to produser
  ```console
  cline master bind <AccountName> <PublicKeyAccount> <IP_Node>:9010
  ```
  Delete `<>`

  If Message Error :  `wallet not unlocked` 

  ```console
  cline wallet unlock -n <NameWallet> -p <PasswordWallet>
  ```

* Allow to be producer
  ```console
  cline master approve <AccountName>
  ```

  If Message Error : `unable to find key` required to request a faucet again on the dashboard

* Check if the account has produced a block
  ```console
  cline get account <AccountName>
  ```

Goto [TASK1](https://github.com/an-node/NODE-TESTNET/tree/main/Inery/Task1)

## Troubleshoot

### Error : FileNotFoundError:[Errno] No such file or directory:./blockchain/config/config.ini

Indication :  `libssl 1.1` not installed properly

Solution : 
```
wget http://nz2.archive.ubuntu.com/ubuntu/pool/main/o/openssl/libssl1.1_1.1.1f-1ubuntu2.16_amd64.deb
sudo dpkg -i libssl1.1_1.1.1f-1ubuntu2.16_amd64.deb
```

### Erorr : net_plugin::plugin_startup failed to bind to port 9010

Indication : noding keeps running in the background

Solution : 
```
pidof nodine

kill -15 <pid>
```

Check Again

```
pidof nodine
```

Run Again

## Delete Node
  ```console
  cd $HOME/inery-node/inery.setup/master.node
  ./stop.sh
 pidof nodine
 cd $HOME
 rm -rf inery-node 
 ```
