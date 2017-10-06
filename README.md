# simple-blockchain
My implementation of a blockchain in C++ I created for fun :)
Follows some Bitcoin design choices including using SHA-256 to hash headers and blocks, merkle trees, and mining WoS. 
- Uses C++14 and OpenSSL library

### Peer-to-Peer coming soon!

Includes a Command line interface that allows you to view blockchains at different indices and add new blocks. You 
can do that 20 times until it automatically quits -> can change that. You can control-c to quit too. 

And unfortunately, everything is stored in memory and is deleted on quit.

## BlockChain Class
#### Private Variables: 
- blockchain(vector<unique_ptr<Block> >): vector of smart pointers to Block objects

Genesis Block is created during intialization.
Every time you want to add a block to the blockchain, you will need to provide it: 

`int index, string prevHash, string hash, string nonce, vector<string> &merkle`
- index: index of the block
- prevHash: hash of the previous block
- nonce: self-explantory
- merkle: vector holding in the data of the block

It will then check whether you have the correct hash(it rehashes it), if you have "00" in front, and whether your index is correct.

Note: this is the only way to add to the blockchain.


## Mining
(I made it very simple because I didn't want to spend much processing power) - use findHash() to get hash and nonce

first two characters of the hash must be 0
- e.g. `003d9dc40cad6b414d45555e4b83045cfde74bcee6b09fb42536ca2500087fd9` works 


## Block 
Hash header: index + prevHash + merkleRoot(data) + nonce

#### Private Variables:
- index
- Data: vector of strings
- previousHash
- blockHash
- nonce

For a block to be immutable, its properties are private and there are only methods that return them but not update them. 

## Common Functions
#### getMerkleRoot(const vector<string> &merkle)
  - gets merkle root based on elements of a vector
#### findHash(int index, string prevHash, vector<string> &merkle)
  - "Mining" part 
  - finds hash and returns a std::pair of the hash found and nonce used to find it 




tk2@illinois.edu
