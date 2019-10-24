# Cosmos
Step by Step Setup Cosmos and Nginx using AWS

# 1) Create 2 servers using t2.micro instance type
![Nginx Web Server](https://github.com/fisher-woon/Cosmos/blob/master/AWS_Nginx_server.png)
![Cosmos Application Server](https://github.com/fisher-woon/Cosmos/blob/master/AWS_Cosmos_server.PNG)

After created the servers, configure inbound rules to allow SSH and open Firewall
![Nginx Inbound rules](https://github.com/fisher-woon/Cosmos/blob/master/AWS_Nginx_inbound_rules.PNG)
![Cosmos Inbound rules](https://github.com/fisher-woon/Cosmos/blob/master/AWS_Cosmos_inbound_rules.PNG)

In Elastic IPs navigation, allocate 2 new address and assign to Server Nginx and Cosmos
![Elastic IPs](https://github.com/fisher-woon/Cosmos/blob/master/AWS_Elastic_IPs.PNG)

# 2) Configure Cosmos Application Server
SSH to server via Putty with your key pair.

Create a new script "$ sudo vi gaia_install.sh" and copy script from https://gist.github.com/kwunyeung/bfc3a6c9f8e5ad2566f12e69419c64e6

Create a new script "$ sudo vi gaia_update.sh" and copy script from https://gist.github.com/kwunyeung/802965472b526513f12793eeaef5abd2

Execute both scripts

Download genesis.json "$ sudo wget https://raw.githubusercontent.com/cosmos/testnets/master/gaia-13k/genesis.json -o $HOME/genesis.json"

Move the file "$ sudo mv $HOME/genesis.json /opt/gaiad/config/genesis.json" and change ownership "$ sudo chown gaiad:gaiad genesis.json"

Edit file "$ sudo vi /opt/gaiad/config/config.toml"
![config.toml](https://github.com/fisher-woon/Cosmos/blob/master/edit_config_toml.PNG)

Save the changes and start the service.

![start service](https://github.com/fisher-woon/Cosmos/blob/master/start_service.PNG)

![check status](https://github.com/fisher-woon/Cosmos/blob/master/check_status.PNG)

To start a REST server \
$ gaiacli rest-server --chain-id=test \
	--laddr=tcp://0.0.0.0:1317 \
	--node tcp://0.0.0.0:26657 \
	--trust-node=false
  
 # 3) Configure Nginx Web Server
 install Nginx Web Server \
 ![install nginx](https://github.com/fisher-woon/Cosmos/blob/master/install_nginx.PNG)
 
 Setup proxy redirect API calling connection to Cosmos server. \
 Edit configuration file "$ sudo vi /etc/nginx/sites-enabled/default"
 ![setup proxy](https://github.com/fisher-woon/Cosmos/blob/master/nginx_setup_proxy.PNG)
 
 Test syntax error and start nginx service.
 ![start service](https://github.com/fisher-woon/Cosmos/blob/master/start_nginx_server.PNG)
 
 # 4) Test API Calling using Nginx Server Public IP
 http://3.132.153.217/node_info \
 ![api result](https://github.com/fisher-woon/Cosmos/blob/master/api_result.PNG)
 
 
