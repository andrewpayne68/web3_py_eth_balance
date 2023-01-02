# Web3 and interacting with the Ethereum Blockchain - ETH Balance

Web3.py enables you to fulfill the second responsibility: developing clients that interact with The Etherem Blockchain. And not necessarily "clients" like user-facing applications (web applications for example), but "clients" that transact with the blockchain by reading information from it, writing new transaction data to it, or executing business logic with smart contracts. Since you're writing python this "client" might be a script that scrapes blockchain data, or a server process that executes a smart contract function for example. Web3.py is collection of libraries that enable you to do these kinds of things: create Ethereum transactions, read and write data from smart contracts, create smart contracts, and so much more!

Web3.py talks to The Ethereum Blockchain with JSON RPC, which stands for "Remote Procedure Call" protocol. Ethereum is a peer-to-peer network of nodes that distributes all its data across each node in the network. In other words, each node on the network gets a copy of all the code and the data on the network. Web3.py allows us to make requests to an individual Ethereum node on behalf of the entire network with JSON RPC. This will allow us to read and write data to the network through a single node. It's kind of like making HTTP requests to a JSON API on a web server.

Dependencies
Let's install developing with Web3.py.

Python
First, you'll want to ensure that you have some version of Python installed. I'm using version 3.6.7 in this series. Next, you'll want to use some kind of environment manager like venv, which ships with Python or pyenv, which you can download here.

You can see if you have Python already installed on your machine by going to your terminal and typing:
```
$ python --version
```
OR:
```
$ python3 --version
```
Make sure you have some version of Python 3 installed before continuuing. If you have multiple Python versions installed, and you're forced to use python3 to access Python version 3, then please use python3 instead of python for all Python specific terminal commands in this series.

Next, you'll want to create a virtual envrionment with venv or pyenv to install Python dependencies.

Web3.py Library
You can install the Web3.py library with pip in your terminal like this:
```
$ pip install web3
```
Infura RPC URL
In order to connect to an Ethereum node with JSON RPC on the Main Net, we need access to an Ethereum node. There are a few ways you could do this. For one, you could run your own Ethereum node with Geth or Parity. But this requires you to download a lot of data from the blockchain and keep it in sync. This is a huge headache if you've ever tried to do this before.

Mostly for convenience, you can use Infura to access an Ethereum node without having to run one yourself. Infura is a service that provides a remote Ethereum node for free. All you need to do is sign up and obtain an API key and the RPC URL for the network you want to connect to.

Once you've signed up, your Infura RPC URL should look like this:

https://mainnet.infura.io/v3/YOUR_INFURA_API_KEY_GOES_HERE
Checking Account Balances
Now that all of your dependencies are installed, you can start developing with Web3.py! First, you should fire up the Python shell in your terminal like this:
```
$ python
```
Now you've got the Pthon shell open! Inside the Pthon shell, you can import Web3.py like this:

from web3 import Web3
Now you have access to a variable where you can create a new Web3 connection! Before we generate a Web3 connection, we must first assign the Infura URL to a variable like this:

infura_url = "https://mainnet.infura.io/v3/YOUR_INFURA_API_KEY_GOES_HERE"
Make sure that you replace YOUR_INFURA_API_KEY with your actual Infura API key that you obtained earlier. Now you can instantiate a Web3 connection like this:
```
web3 = Web3(Web3.HTTPProvider(infura_url))
```
Now you have a live Web3 connection that will allow you to talk to the Ethereum main net! We can ensure that we're connected like this:

print(web3.isConnected())
This will return true if the connection is live. Next we can check the latest block number like this:
```
print(web3.eth.blockNumber)
```
There's the latest block number! Now let's check the account balance for this account: 0x90e63c3d53E0Ea496845b7a03ec7548B70014A91. We can see how much Ether this account holds by checking its balance with web3.eth.getBalance().

First, let's assign the address to a variable:
```
account = "0x90e63c3d53E0Ea496845b7a03ec7548B70014A91"
```
Now, let's check the account balance like this:
```
balance = web3.eth.getBalance("0x90e63c3d53E0Ea496845b7a03ec7548B70014A91")
```
There's the account balance! However, I should note that this account balance is expressed in wei, which is a subdivision of Ether, kind of like a penny. You must convert this to Ether by dividing the value by 10 ** 18.

And that's it! That's the conclusion to the first part of this tutorial. Now you've seen what the Web3.py library is and you can get started using it to check Ethereum account balances. Here is a summary of the code we wrote in this tutorial:
```
from web3 import Web3

infura_url = "https://mainnet.infura.io/v3/YOUR_INFURA_API_KEY_GOES_HERE"
web3 = Web3(Web3.HTTPProvider(infura_url))
print(web3.isConnected())
print(web3.eth.blockNumber)
balance = web3.eth.getBalance("YOUR_ACCOUNT_GOES_HERE")
print(web3.fromWei(balance, "ether"))
```
