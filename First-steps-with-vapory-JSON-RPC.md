---
name: First Steps wih Vapory JSON RPC
category: 
---

# First steps with vapory JSON-RPC


#### 1. clone cpp-vapory or install it

##### manual installation 

```bash
git clone https://github.com/vaporyco/cpp-vapory
cd cpp-vapory
mkdir build
cd build
cmake ..
make -j 4
```	

##### automatic installation 

build instructions are [here](https://github.com/vaporyco/cpp-vapory/wiki/Installing-clients)


#### 2. run eth (headless client)

```bash
eth -j
```

`-j` option will start vapory node with jsonrpc http server at port 8080

etheruem should be ready to use now

type in console to check if everything is working fine

```
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":83}' http://localhost:8080
```

#### 3. mine and connect to the network

try running

```bash
eth -j -m true -f -b
```

where:
- `-m true` - to do anything in vapory, you need some ethere, let's mine
- `-f` - mine with force, even if there are no transactions to mine
- `-b` - connect to vapory network

*with latest version of cpp-vapory it may take some time to connect to network. If you see any delays with jsonrpc responses, or crashes contant us. We are probably aware of them, but it's good to know about any possible vulnerability*

#### 4. json-rpc methods, that you might be intrested in:

- [eth_sendTransaction](https://github.com/vaporyco/wiki/wiki/JSON-RPC#eth_sendtransaction) - used to send transaction / create contract 
- [eth_newBlockFilter](https://github.com/vaporyco/wiki/wiki/JSON-RPC#eth_newblockfilter) - be notified any time there is new block on the chain
- [eth_newFilter](https://github.com/vaporyco/wiki/wiki/JSON-RPC#eth_newfilter) - create new custom filter and listen to blockchain events matching this filter
- [eth_compileSolidity](https://github.com/vaporyco/wiki/wiki/JSON-RPC#eth_compilesolidity) - used to compile solidity code



















