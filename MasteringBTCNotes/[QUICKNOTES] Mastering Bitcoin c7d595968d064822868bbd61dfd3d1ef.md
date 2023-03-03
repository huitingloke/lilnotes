# [QUICKNOTES] Mastering Bitcoin

# 1 Introduction

`doublespend` — ensuring no one else can claim the money belongs to them and not to the actual owner

- 4 things:
    - Bitcoin protocol — decentralized peer-to-peer network
    - Blockchain — public transaction ledger
    - Distributed mining — math/deterministic currency issuing system
    - Transaction script — decentralized transaction verification system
- `Client`
    - `Full client` — stores every transaction, trades directly onto the network, manages the user’s wallets — aka handles the protocol directly
    - `Light client` — stores transactions but still relies on third parties for interactions with the network
    - `Web client` — everything’s done through a third party
- You can QR code your BTC wallet to make it easy for people to pay you LOL
- [https://blockchain.info/address/](https://blockchain.info/address/1Cdid9KFAaatwczBwBttQcwXYCpvK8h7FK)[your bitcoin address]
- On confirmation of a bitcoin transaction
    - Okay, apparently might not need to wait 10 minutes for this… some might just accept small transactions with low risk :P
    
    ![Screenshot 2023-02-24 at 10.05.49 AM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-02-24_at_10.05.49_AM.png)
    

## Questions

- So if everything is verified every 10 minutes, can’t you just game the system and only have 1 person mine? Unless it’s a system that’s supported by trying to get the bitcoins themselves, which encourages competition and is the only reason it works?
    
    Answer: You’d need to collude with literally the whole world, so yes it is competition that drives it
    

# 2 How Bitcoin Works

- Blockchain explorer site: website like a BTC search engine, let’s you track transactions
- QR bitcoin codes will do the equivalent of a PayNow — where it autofills the information of the wallet that the money will go to
- Inputs and outputs and transaction definitions
    
    ![Screenshot 2023-02-24 at 10.19.16 AM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-02-24_at_10.19.16_AM.png)
    
    ![Screenshot 2023-02-24 at 10.19.52 AM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-02-24_at_10.19.52_AM.png)
    
- “Change” — putting many smaller amounts of BTC for it to be returned as one large sum — literally exchanging coins for a note IRL
    - If not enough to conduct transaction, wallets will scrounge around for this change to try and have enough to pay :P
- 1 input to multiple outputs — could be done with BTC e.g. paying multiple employees
- Transactions can occur offline, but you need to be online for it to be updated as one
- `curl` gets the data from a website… kind of
    - It’s a simple HTTP get request :3
- Example
    
    Coffee is 0.15 BTC — Alice has 1 BTC and pays for the coffee — 0.15BTC paid for coffee and 0.845BTC paid to herself as “change” and 0.005 goes to the transaction fee
    
- New blocks with unsure data — must be verified by the process of mining — when verified is easy to check if it’s correct… then TADA it is a real BTC block that is proven in the algorithm
    - Like sudoku solving thing — easy to verify but hard to solve
    - The more blocks that are mined, the more they build on the block before, and the more secure it is — 6 blocks is normally considered irreversible HAHA
- Everything will be carried out in transactions from then on!

## Questions

# 3 The Bitcoin Client

- `git tag` lets you find the version which you are running on
- `git checkout [version]` lets you choose the version you want to run on
- Info
    
    ![Screenshot 2023-02-25 at 10.55.26 AM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-02-25_at_10.55.26_AM.png)
    
- Client stuffs — preface all commands with the terminal command `bitcoin-cli`
    
    `getinfo` : json file of data about your client
    
    `password [newpassword]` : creates new password for your client
    
    `walletpassphrase [yourpassword] [timeuntillockedinseconds]` : unlocks your wallet for a while
    
    `backupwallet [nameofwallet].backup` : saves your wallet into a backup file of your choice
    
    `dumpwallet [nameofwallet].txt` : dumps your wallet into a human readable file
    
    `getnewaddress` : creates a new BTC address for you 
    
    `getreceivedbyaddress [yourwalletaddress] [no.ofconfirmations(just put 0)]` : get BTC retrieved
    
    `listtransactions` : see all transactions from entire wallet
    
    `getaddressesbyaccount ""` : shows all addresses in your wallet
    
    `getbalance` : adds up all transactions with `minconf` confirmations
    
    - will not show balances at all if you the min number of confirmations have not been fulfilled
    - Exploring and decoding transactions
        - `gettransaction [transactionhash]` : shows details of transaction in JSON file
            - Transaction malleability — transaction can technically be modified until its hard coded into the block
        - `getrawtransaction [transactionhash]` : shows the transaction in a bit decoded format
        - `decoderawtransaction [rawtransaction that the aforementioned function returns]` : shows all the details, even more than just `gettransaction`
            
            ![Screenshot 2023-02-25 at 12.02.33 PM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-02-25_at_12.02.33_PM.png)
            
    - Exploring blocks
        - `getblock [blockhash] true` : Will see JSON file with all the details of every transaction in that block
            - Height states the number of block it is in the tower thing
        - `getblockhash [height]` : JSON of block measured by height
        - `getblock [hash]` : same thing as above but using the hash instead
    - Creating, signing and submitting transactions based on unspent outputs
        - Concept
            
            Spending “outputs” of transactions → creates a transaction chan that transfers ownership from address to address
            
        - `listunspent` : shows unspent “outputs”
        - `gettxout [txid]` : returns details about an unspent transaction output
        - Steps
            - `list unspent` : see how much money you have left
                - `gettxout [hash] 0` : view more details about this particular block/transaction
            - `getnewaddress` : self explanatory
            - `createrawtransaction \[{"txid" : "9ca8f969bd3ef5ec2a8685660fdbf7a8bd365524c2e1fc66c309acbae2c14ae3", "vout" : 0}]' \
            '{"1LnfTndy3qzXGN19Jwscj1T8LR3MVe3JDb": 0.025, \
            "1hvzSofGwT8cjb8JU7nBsCSfEVQX5u9CL": 0.0245}'` : honestly I don’t understand the parameters and I’m way too intimidated to find out why, but it seems like you’re parsing a personal JSON which is fortunately not my personal problem
                - The 0.025 is payment, the 0.0245 is paid back to us, and the 0.005 or whatever is left is used as a miner’s reward
            - `decoderawtranasction [hashthatcreatetransactiongives]` : Decodes the transaction mess from earlier
            - `walletpassphrase [password] [timeyouwillleaveitunlockedinseconds]` : so that you can sign stuff with your own key
            - `signrawtransaction [secretkey]` : lets the wallet know you are the owner and to approve the transaction
                - Transactions should now include `scriptSig` , which is a script’s signature
            - `sendrawtransaction [rawheckofsignedtransaction]` : YESSSS FINALLY
            - `gettransaction [txid]` : check your transaction on the servers
        - Alternative wallets
            
            ![Screenshot 2023-02-25 at 12.20.43 PM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-02-25_at_12.20.43_PM.png)
            

# 4 Keys, Addresses, and Wallets

## Keys

- Keys are stored inside local BTC wallet (simple database)
- WIF: Wallet Import Format
    - Standardized method for displaying Bitcoin private keys using the Base58Check encoding scheme
- Two
    - Public key — think of it like the bank account number
        - Public key = private key * elliptic curve number generator
        - Start with 04 (uncompressed) or 03, or 02 (compressed)
            - 03  if the y in the graph is odd, 02 if the y is even to deduce at the end if the answer in the formula is positive or negative
    - Private key — think of it like the PIN
        - Number picked at random — determines public key which determines the address
            
            ![Screenshot 2023-02-26 at 4.14.43 PM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-02-26_at_4.14.43_PM.png)
            
        - Owner controls all the BTC in this wallet
        - Cannot be retrieved once lost
        - `bitcoind dumpprivkey` — shows your private key (truly not recommended friends)
        - Formats
            
            
            | TYPE | PREFIX | DESCRIPTION |
            | --- | --- | --- |
            | Hex | None | 64 Hex digits |
            | WIF | 5 | Base58Check encoding — base-58 with version prefix of 128 and 32-bit checksum |
            | WIF-Compressed | K or L | As above, with added suffix 0x01 before encoding |
- Cryptography — easy to encode and pretty near impossible to decode
- Compressed private key — really is a private key from which compressed public keys should be derived
    - And uncompressed private keys are private keys from which uncompressed public keys should be derived
    - Export formats are either WIF-compressed or WIF, just don’t refer to private key as compressed =]
    - Poot brainfart which essentially explains the public and private key vibe and its compressed forms (research more in the future)
        - Compressed public keys used by default: private keys used to make public key points → compressed→ WIF now adds _01_ to the private key (”Compressed WIF”) and starts with K or L
        
        ![Screenshot 2023-02-26 at 6.27.19 PM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-02-26_at_6.27.19_PM.png)
        

## Addresses

- Begin with `1` for BTC
- Not the same as a public key
- Uses base58 `123456789ABCDEFGHJKLMNPQRSTUVWXYZabcdefghijkmnopqrstuvwxyz`
    - Base58 checked against Base58Check — comes up with hashsum for each of those equations and if those don’t match, something went wrong
        - Base58Check version prefix and encoded result examples
            
            ![Screenshot 2023-02-26 at 6.08.38 PM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-02-26_at_6.08.38_PM.png)
            
        
        ![Screenshot 2023-02-26 at 6.07.22 PM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-02-26_at_6.07.22_PM.png)
        
        - `checksum = SHA256(SHA256(prefix+data))`
        - Prefix + data + checksum = Check encoding
- Decoding
    - Can use the LIbbitcoin and sx tools library
        - `sx base58check-decode [base58]` — BASE58 to Hexadecimal key
            - Returns key and an integer, which would be WIF prefix number
        - `sx base58check-encode [hex]` — Hexadecimal to BASE58
            - Returns BASE58 string
    - There is more but lazy and it is irrelevant to me right now. When this is relevant, go to page 77.

## Keys and addresses in Python

- Personal comment here…
    
    > Hi me! If you’re reading this, you’re currently scrolling through the book looking at all the juicy Python code. It’s great. It makes sense, it kinda acts like a baby documentation for the way Python is used to decode and encode keys and come up with addresses. However, I don’t see the use of documenting it here further because it’ll just be screenshotting all the pages. If you’re very interested, click [here](https://unglueit-files.s3.amazonaws.com/ebf/05db7df4f31840f0a873d6ea14dcc28d.pdf) to go to the page and read through it yourself on page 81-84 :3 Have fun! It’s kinda cool actually
    > 
- [Hex, WIF, Base58 encoder and decoder in Python](https://github.com/primal100/pybitcointools) for public and private keys and addresses — main page has been deprecated =(
- Python ECDSA library — creates elliptic curve math to explore how BTC is encoded and decode
    
    ```bash
    pip install ecdsa
    ```
    

## Wallets

- Private key containers — key value pair of private to public keys
- Type 0 wallet — randomly generated keys
- Deterministic (seeded) wallets — all keys derived from a common seed
    - Don’t need to backup anything other than the seed since it can all be brought about anyway
    
    ### Hierarchial deterministic wallets
    
    - Can keep deriving children from the children from the children etc… from one parent seed to a master key to all the child keys
    
    ![Screenshot 2023-02-26 at 6.44.38 PM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-02-26_at_6.44.38_PM.png)
    
    ![Screenshot 2023-02-26 at 6.47.47 PM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-02-26_at_6.47.47_PM.png)
    
    - Can be used to make many keys,,, perhaps for an organization? — can keep creating child keys for different members hehe
    - Can keep sequence of public keys without needing the private key to access it — can receive funds without having it be able to derive the private key
    - Created from root seed - 125, 256, or 512 bit random number
    - Use *********************child key derivation********************* (CKD) to derive children from parent keys — one way hash function of parent public/private key, seed (256 bits), and index number (32 bits)
        - Normal child: number between 1 - 2^31-1 to derive
        - Hardened (see below) child: number between 2^31 - 2^32-1 to derive
            - Index displayed starts from 0 with prime symbol — 0’
    - Child keys operate as normal keys, cannot trace its siblings either — guarantees privacy
    - Extended key — used to derive children (like extra to the seed key when deriving children keys)
        - Extended public key — public key and chain code
        - Extended private key — private key and chain code
        - Having easy access to the public key tree network lets there be transparency to someone on the inside with the extended public key, but only the private key owner can actually spend the funds — limits access
    - Hardened derivation: using the parent private key to derive the child key — can’t be retraced if the parent public key is obtained
    - Wallet key identifier (aka path, like you know HTTP path)
        - M/0/3/2 — public key’s 0th child’s 3rd child’s second child
        - m/1/2/3 — private key’s first child’s second child’s third child
    - Proposal to navigating the tree structure
        
        ![Screenshot 2023-02-26 at 7.06.13 PM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-02-26_at_7.06.13_PM.png)
        
        ![Screenshot 2023-02-26 at 7.07.03 PM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-02-26_at_7.07.03_PM.png)
        
- Mnemonic code words — 12-24 words used as a seed that is enough to recreate the wallet and its derived keys

## Advanced keys and addresses

- Encrypted private keys
    - BIP0038 — choosing your own passphrase and merging it with your private key to encode as a BIP0038 encrypted key
    - If it starts with 6P, it’s encrypted and needs to be decoded
        
        ![Screenshot 2023-02-26 at 7.10.19 PM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-02-26_at_7.10.19_PM.png)
        
- Pay to script hash (P2SH) and multi-sig addresses
    - Type of bitcoin transaction that allows the sender to commit to a script, or set of conditions, that must be met in order to spend the funds
    - Created from transaction script that defines who can spend a transaction output
        
        ![Screenshot 2023-02-26 at 7.12.16 PM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-02-26_at_7.12.16_PM.png)
        
    - E.g. multi signature address script — require M signatures from N keys to go through
- Vanity address
    - Creating a BTC address by running through until it matches your requirement e.g. starting with “1Kids”
    - Technically can be secure if you generate an 8 character distinct start, which makes the attacker have to generate 10 places which is very inefficient in order to “match” it at least
- Paper wallets
    - Private keys printed on paper aka “cold storage”
    - Can be stolen… like literally physically stolen LOL
    - Can encoded with BIP0038 and memorize your own passphrase and encode it with that — ultimate POWER!!

# 5 Transactions

- Transactions: encode transfer of value between participants in the BTC system
    - Data structure that encodes a transfer of value from a source of funds (input) to a destination (output)
- The cycle:
    - Origination (creation) → signed → broadcasted on network for validation → verified by mining node → recorded on blockchain
    - Once it is sent to a node, node will verify
        - If it’s properly created and signed, will succeed
        - Otherwise it will send a rejection message to the owner and reject it
    - All nodes verify transactions before propogating it to another 3 to 4 machines until everyone has an updated copy — so only valid transactions will go through :3
- Can be sent over any network because it doesn’t contain any sensitive information — could even be turned into emojis and pasted into a web form or something LOL (changing money into a data structure)
- Locktime: earliest time a transaction can be added to the blockchain
    - If 0 < num < 500,000,000: interpreted as blockheight
    - If num > 500,000,000: interpreted as Unix Epoch timestamp
- Unspent Transaction Output (UTXO): No “balance” of funds, just the chain remembering that scattered everywhere, there are some UTXO funds that a user has access to use but it is not stored WITH the user
    - UTXO, once created, cannot be divisible again
    - If too big, then it will be consumed and create another UTXO
    - **UTXO used: transaction input; UTXO created: transaction output**
    - Exception: ********coinbase******** transaction, aka first transaction in each block placed by the winning miner that creates new bitcoin for the miner (yes, they technically create an output from nothing)
    - Kept in a UTXO pool by verified nodes
    - 2 parts
        - Amt of BTC (in satoshis)
        - Encumbrance (locking script) — specifies conditions that must be met to spend this output — e.g. having the transaction be signed by the person who owns the UTXO and exceeding a certain cost
            - Both locking and unlocking script written in some Forth-like language — when checking, validation script checked alongside locking script to see if conditions are fulfilled
            - IT’S LITERALLY PROGRAMMABLE MONEY
    - Transaction input: pointers to UTXO that also have unlocking scripts to satisfy UTXO usage conditions
        - Sidenote
            
            `from sys import argv` — allows you to take a parameter in your terminal and use it in Python HAHA
            
        - If conditions satisfied → UTXO unlocked → all this information added to the inputs of the transaction
- Transaction structure (image)
    
    ![Screenshot 2023-02-27 at 11.50.11 AM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-02-27_at_11.50.11_AM.png)
    
- Transaction fee
    - Pay money to get your stuff processed — incentivize miners to miner a transaction into the next block + avoid spam
    - Technically it’s not compulsory but it certainly speeds up the process because yours gets dumped at the front if you pay more (I’m sorry, do I hear pay to win?)
    - `Fees = sum(inputs) - sum(outputs)` — my extra change be going to the miner TwT
        - IMPORTANT: If you paying a 1 BTC fee with your 20BTC, you MUST change 19BTC back to yourself or that will be the transaction fee…
    - Calculated based on the size of the transaction, not the value of the coin
- Orphan pool
    - Temporary holding station for child transactions waiting for their parent transactions to be fulfilled first
    - When parents arrive, it will be recursively reconstructed and all mined in the proper order
    - If the max size of the pool is hit, it will evict random transactions until it’s within the size again
- Scripting transaction requirements
    
    ![Screenshot 2023-02-27 at 12.59.21 PM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-02-27_at_12.59.21_PM.png)
    
    - Locking script — specifies requirements to spend output in the future
        - Probably appears as `scriptPubKey`
    - Unlocking script — solve/satisfies conditions placed by locking script
        - Probably appears as `scriptSig`
    - Validation software gets UTXO + its locking script → check unlocking script against it
        - Unlocking script generates some sort of result → copy of that result tested against the locking script → if even one fails, whole thing fails → otherwise it’s considered pass (locking script is already in blockchain so it cannot be amended and unlocked in any other way other than by a valid unlocking script)
    - Language — “Script”
        
        ![Screenshot 2023-02-27 at 1.03.03 PM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-02-27_at_1.03.03_PM.png)
        
        ![Screenshot 2023-02-27 at 1.03.20 PM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-02-27_at_1.03.20_PM.png)
        
        - Very simple non-fancy language meant to run on anything
        - Stack based — uses stacks e.g. push and pop
        - Turing incomplete to ensure no infinite loops can break the process
        - Stateless verification
        - Standardized transactions (as of 2014, I don’t know about now) — Go to page 128 of the book if you’re interested in seeing how everything plays out in more detail
            - Pay to Public key hash (P2PKH) — most common on BTC network
                - Locking script have public key hash — to unlock, you need to present public key and digital signature
                - `<Cafe Signature> <Cafe Public Key> OP_DUP OP_HASH160 \ <Cafe Public Key Hash> OP_EQUAL OP_CHECKSIG`
            - Pay to public key
                - Public key stored in locking script
                - Unlocking script needs signature from private key
                - `<Signature from Private Key A> <Public Key A> OP_CHECKSIG`
            - Multi-signature (up to 15 keys)
                - Need at least N number out of M signatures saying yes to validate
                    - (Check is standard function for what is currently accepted by the network)
                - `OP_0 <Signature B> <Signature C>\ 2 <Public Key A> <Public Key B> <Public Key C> 3 OP_CHECKMULTISIG`
                    - First part gives available signatures
                    - 2 stands for the number of signatures needed
                    - 3 stands for the number of public keys whose signatures you will check for
            - Pay to script hash (P2SH)
                - “pay to a script matching this hash, a script which will be
                presented later when this output is spent”. — they really said “not my problem HELP”
                    - Entire multisign transaction is hashed into SHA256, and that’s passed into this P2SH
                    - If the other side’s encoded script also matches the SHA256, then the unlocking script is executed on its own
                - Script replaced with a cryptographic hash (digital fingerprint) — when trying to spend UTXO, must have the script that matches this hash and the unlocking script
                    
                    ![Screenshot 2023-02-27 at 1.19.29 PM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-02-27_at_1.19.29_PM.png)
                    
                - Burden and complexity shifted to receiver — unloads data less
                - Pay to script hash addresses
                    - Base58Check encoding of 20-byte hash of public key — since P2SH addresses start with 5, when encoded they’ll start with 3
                    - Give address to BTC wallet to make a payment — I think it’s because by right the other guy should have your address if he hashes it anyway and it matches, so there will be no problems retrieving your address but if it’s not there, then we will all collectively scream in agony
                - Benefits (only writing non intuitive ones)
                    - Burden in data storage goes from output (UTXO set) into input (blockchain)
                    - Data storage burden moved to future time when spent
                - Do not put P4SH inside a P2SH redeem script as it’s not recursive
                - If you encode something wrongly, the transaction might be processed but you will be unable to access the BTC inside… p2SH will be accepted even if the redeem script is invalid because ain’t nobody got time to check
            - Data output
                - Storing data that isn’t currency transactions because you like the format and the simplicity
                - No unlocking script because there is no “spend”
                - Some don’t like it because it creates unspendable UTXOs and bloats it
                - Compromise is that the `OP_RETURN` function was made — does store on the blockchain and use up storage, BUT is not stored on the UTXO set so it doesn’t clog that one up
                - One transaction can only have 1 OP_RETURN (for isStandard() checks), but 1 OP_RETURN can be combined in transactions with outputs of other types
                - `OP_RETURN <data>`
                    - Would add a SHA256 code as the parameter and if it matches, returns a boolean like the rest
                - Do not use OP_RETURN in a redeem script because OP_RETURN cannot be redeemed
    - Script validation has changed now! There can be other types other than these 5 if you want as long as it runs in a valid way

## Nerd has questions

- Is it possible for a node to wrongly verify something? And if it does and keeps that copy, since it’s the only one in the blockchain that is wrong, will it eventually sync up to correctly identify something? I’m having trouble conceptualising this in my brain…

# 6 The Bitcoin Network

- Peer to peer — no hierarchy, all nodes connect to each other as equals
- Bitcoin is flat, decentralized P2P
- Bitcoin network: nodes running the bitcoin P2P protocol
    - Protocol: established set of rules that determine how data is transmitted between different devices in the same network
    - Extended Bitcoin network: Overall network of P2P bitcoin protocol, pool mining protocols, Stratum protocols
        - Other protocols yoink from the main protocol and extend to their own, providing additional service but using BTC as a base
        - Stratum protocol: used for mining and lightweight wallets
        - Some companies build products on top of this network (blockchain and network without mining and wallet)
        - Network kinda just is a jumbled amalgamation of different types of nodes all doing their own thing but contributing to the main network with their wallets, some with validation, some with products and services etc
            
            ![Screenshot 2023-02-28 at 10.31.13 AM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-02-28_at_10.31.13_AM.png)
            
- Nodes: can route, validate transactions and blockchain, and maintains connection to peers
    - Some might be ‘full nodes’ — carry copy of blockchain
    - Simplified Payment Verification: some non-full nodes use this to validate transactions (more at bottom)
    - Reference list of nodes (image)
        
        ![Screenshot 2023-02-28 at 10.28.30 AM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-02-28_at_10.28.30_AM.png)
        
        ![Screenshot 2023-02-28 at 10.29.03 AM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-02-28_at_10.29.03_AM.png)
        
- Network discovery: new node booting up and finding other nodes → not geographically constrained and can be any node
    - Gives a series of information to existing node
        
        ![Screenshot 2023-02-28 at 10.32.27 AM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-02-28_at_10.32.27_AM.png)
        
    - If successful, other node responds with `verack` (which I assume stands for version acknowledge) and, if it wants to connect as a node, repeats this process and hopes the original node sends `verack` back
    - Seed nodes — kind of a default choice to discover new nodes
    - Nodes can send their address, then request addresses from nodes it connected to so it gets better connected
    - `getpeerinfo` — Bitcoin Client, let’s you see who you’re connected to HAHA
    - Bootstrapping: only connecting to a few nodes (and in turn they are only also connected to a few) so that connection space isn’t wasted, if the normally connected to nodes don’t respond (within 90 minutes), you can find more nodes to use as default
        - It’s literally like my friendships why am I so sad
- Full (blockchain) nodes
    - Maintain up to date blockchain transactions — can independently verify transactions by relying on network to receive updates then updating its blockchain
    - It’s like 450 GB to run a full node you know what I’ll just install GTA
    - Exchanging inventory
        - Node’s local blockchain with highest height will disseminate, 500 blocks at a time, information to other nodes with smaller ones
        - `getblock` → `inv` entory the blocks to see what you’re missing → catch up to full blockchain
            
            ![Screenshot 2023-02-28 at 10.46.00 AM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-02-28_at_10.46.00_AM.png)
            
- Simplified payment verification (SPV) nodes
    - Lightweight client that doesn’t need to store full blockchain
    - Only download block headers — relies on peers to see partial view of the block when information is necessary
        - Tourist analogy
            
            ![Screenshot 2023-02-28 at 10.48.57 AM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-02-28_at_10.48.57_AM.png)
            
    - Describes blocks by depth instead of height — verifies chains of all blocks and links the ones of interest (Merkle Path)
        - A full blockchain node verifies a transaction by checking the chain of thousands of blocks below it and checks that the UTXO is not spent, whereas an SPV node checks how deep the block is buried by a handful of blocks above it
    - `getheaders` used to get the infomation needed, `getdata` used if more specific information is required
    - Bloom filters
        - Filter transactions less specifically (including the one you need) without fully revealing which one the SPV is interested in (probabilistic search filter)
            - Instead of “are there any places here called 23 Church Street” it becomes “Do any of the streets here end with R-C-H”?
            - Positive matches are more “probably, yes”, but negative matches are “definitely, no”
                
                ![Screenshot 2023-02-28 at 11.21.46 AM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-02-28_at_11.21.46_AM.png)
                
        - Added to avoid profiling on SPV nodes
        - Has a strength level — specific bloom filters give you more accurate results at expense of privacy, and vice versa
        - How the world works (just understand can already)
            
            ![Screenshot 2023-02-28 at 11.18.47 AM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-02-28_at_11.18.47_AM.png)
            
        - SPV sends `filterload` message (aka the bloom) → anything that matches the bloom filter is sent to SPV
            - If using the Merkle tree to find (aka `merkleblock`), only matching Merkle patterns will be returned when filtering using Bloom
            - `filteradd` — adding filters; `filterclear` — clear filters (since you can’t individually remove filters)
- Transaction pools
    - Unconfirmed transactions list
    - Orphan pool: transactions that need a parent transaction to be completed first but it’s not here, so child transactions are sent here to wait instead of being discarded — once parent arrives, the chain is recursively constructed starting from parent to child
    - Stored on local memory
    - Pools start empty then are populated by different messages from the nodes
        - Some also have UTXO pool (and this one is persistent storage) — only confirmed outputs
- Alert messages
    - Bitcoin devs can send a message to all nodes — rarely used, obviously
    - `alert` — ID, expiration, relayUntil, MinVer MaxVer (the versions which it is applicable to), subVer (client software it applies until), Priority (alert priority level)
    - Signed by public key (private key held by a few developers)
    - Alert received → verify → send on if it’s legit

## Questions from a curious child (me)

# 7 The Blockchain

- Back-linked list of blocks and transactions — all blocks layered on top of the first one
- Genesis block — first block ever created
    - Created within the client itself, so all nodes inherently know the Genesis block
    - `$ bitcoind getblock 000000000019d6689c085ae165831e934ff763ae46a2a6c172b3f1b60a8ce26f`
    - Has a secret message as well for people to know this is the first block :3
- Every block’s ID is identified by hash and previous block
    - If the previous block changes, the entire hash of all subsequent block changes, so you can ensure there is immutability
- Every block can technically have more than one child — a “fork” — but eventually will be resolved
- Blocks
    - Contain metadata (header) and transactions — in metadata, there is stuff like previous block hash, merkle root, nonce (proof of work algorithm counter) etc
        
        ![Screenshot 2023-03-01 at 12.14.10 PM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-03-01_at_12.14.10_PM.png)
        
    - Linking blocks
        - When new blocks are found, validated by node and used to extend the chain
        - Finds `previousblockhash` , uses it as part of the formula (along with the nonce) to hash the new block (starting with like 0000000 HAHA)
- Block hash
    - Identifies a block from hashing the block header
    - Not stored: calculated on the spot
    - Block height can also be determined but might not necessarily be unique (because there might be forks) — is just calculated dynamically
- Merkle trees (binary hash trees)
    
    ![Screenshot 2023-03-01 at 12.26.59 PM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-03-01_at_12.26.59_PM.png)
    
    - Contain cryptographic hashes (opposite tree: root at the top and leaves at the bottom)
    - Formed by recursively hashing blocks until you reach the main block using double SHA256
        - Hashes stored in the tree, those added together are hashed, then the newly hashed one is hashed with another newly hashed one etc etc until you reach the root
        - `H(smallA) = SHA256(SHA256(Transaction A))` — and then do the same for B
        - Then you hash those 2 resulting hashes with another double SHA256 to get another hash
        - Repeat
    - Saves a lot of space because it only hashes the block headers, which aren’t as big as the entire block → final result is also really small and just a check to see if they are the same so YAYYYYY it’s efficient and SPV nodes use it to verify blocks too~
    - Check if data in tree: `2*log(small2)(N)` calculations, thus it is efficient hehe
    - If there is an odd number, the latest smallest hash will be duplicated and added to itself
        
        ![Screenshot 2023-03-01 at 12.27.11 PM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-03-01_at_12.27.11_PM.png)
        
    - No matter what, the tree will be summarized into 32 bytes at the end
    - Merkle path/authentication path
        - Produces a path from the bottom using the new hash to verify the transaction — if it matches the 32 bytes at the beginning then you know the block you are checking is valid

# 8 Mining and Consensus

- Mining: validating and clearing transactions → new bitcoin added to money supply
- Miners: provide processing power to BTC network → opportunity to be rewarded BTC and transaction fees from all transactions in the block
    - Solve difficult math problem based on cryptographic hash algorithm
    - Validate new transactions and add to global blockchain

## BTC economics and currency creation

- Every block contains newly minted BTC
- Deflationary money
    - Appreciating in value due to mismatch in supply and demand that drives up the value → more purchasing power over time
    - Some people think is bad → deflating money over time leads to people hoarding money, which reduces supply even more etc etc, but others say it’s different because BTC value up is caused by constrained supply and not collapse in demand
- Mining rewards will diminish every 4 years — by the time I’m dead, all income would be generated from transaction fees and none from actually mining the block (talk about a slow burn)
    
    ![Screenshot 2023-03-02 at 10.47.15 AM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-03-02_at_10.47.15_AM.png)
    

## De-centralized consensus

- Ensuring everything is the same without a central figure of authority maintaining order and consistency
- Emergent consensus: consensus is an emergent artefact of asynchronous interaction of thousands of independent nodes all following simple rules
    - Consensus is not a status, it’s an evolving state

### Independent verification of transactions

- Every node will verify transactions to ensure they are valid → kinda builds them all in the same order
- There are a lot, but are all summed up under `AcceptToMemoryPool`, `CheckTransaction`, and `CheckInputs` under the BTC reference client

### Mining nodes

- Technically, if a node “receives” a block, it lost the mining competition and has to just fill in the block as new data
- Other than that, this describes the process of using a mining rig (which is a full node in this case) to try and mine for BTC, in the process also confirming the validity of the block that some other machine has mined

### Aggregating transactions into blocks

- Validated transactions get added to the transaction pool → becomes a candidate block → some confirmed block received from some other computer and goes into this man’s node → node aggregates the transactions in the pool, sees what’s inside the block that’s inside the pool, and removes those which have been added to the latest block (and for the other transactions, they have to wait until they themselves are added to a block) → new candidate block created

### Transaction age, fees, priority

- Prioritized transactions: ones with oldest UTXO (allows for old high value UTXO to be prioritized over newer, smaller ones)
    - Can be sent without fees if there is enough space in the block
    - `Priority = Sum (Value of input * Input Age) / Transaction Size`
    - High priority: 57,600,000 or more (which is like, 1 BTC, one day, transaction 250 bytes total size)
- Mining nodes will fill first 50 KB of the transaction with high priority requests, then the rest with highest transaction fees to lowest ones
    - Some miners might include feeless transactions if there’s space left, some might skip over it
- Eventually, transactions that are unprocessed will be old enough to be processed for free LOL (unless something happens to the memory pool if there is a wipe and then suddenly everyone forgets your 42 day old transaction)

### Generation transaction

- First transaction added to a block
- Essentially a miner paying himself the BTC for making the block + transaction fees
- 1 input: coinbase → creates BTC from nothing
- Coinbase rewards and fees
    - `Total fees = sum(inputs) - sum(outputs)` (these are transaction fees)
    - Calculate BTC reward based on block height (accounting for the halving rewrads)
    - Final formula: BTC formula + total fees = your earned money for mining

### Structure

- First 2 fields are ***not*** set to UTXO transactions
- Everything is just set to some pseudo default value

![Screenshot 2023-03-02 at 11.27.29 AM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-03-02_at_11.27.29_AM.png)

### Coinbase data

- Generation transactions have no unlocking script → replaced by coinbase data (arbitrary)
    - Right now miners fill it with extra nonce values and strings identifying the mining pool
- First few bytes of coinbase no longer arbitrary — V2 blocks must have block height index set as “push” operation in the beginning of the field
- Example `03443b0403858402062f503253482f`
    - `03` would indicate something needs to be pushed
    - `0x443b04` block height encoded in little endian format → reverse it to get `0x043b44` — 277,316 in decimal
    - `03858402062` extra nonce
    - `2f503253482f` (ACSII encoded “/P2SH/”) aka Pay to script hash to indicate support for BIP0016 (google it if you don’t know because I also don’t know)

## Block header

![Screenshot 2023-03-02 at 11.42.39 AM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-03-02_at_11.42.39_AM.png)

- `0x02000000` → encoded number 2 (stands for the version)
- `0000000000000002a7bbd25a417c0374cc55261021e8a9ca74442b01284f0569` → previous block hash
- Add merkle root (the encoded one, you know) `c91c008c26e50763e9f548bb8b2fc323735f73577effbc55502c51eb4cc7cf2e`
- Epoch timestamp `1388185914`
- Mantissa exponent encoding of the difficulty target
    - First part is a hexadecimal `0x19`
    - Next is coefficient `0x03a30c`
- Nonce is initialized to 0 (for the miner to solve and encode the funny block in)
    - You win when you find a hash that is less than the difficulty

## Mining the block

- Hashing the block header, changing one parameter, until hash matches a specific target → unpredictable so you need to randomly modify the input until you reach the output

### Proof of work algorithm

- Hash algorithm: arbitrary length data → fixed-length deterministic result (unpredictable model)
    
    ![Screenshot 2023-03-02 at 11.56.33 AM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-03-02_at_11.56.33_AM.png)
    
- SHA256 — output is always 256 characters long, regardless of the input
    - One way cryptographic function
- So miners solve the `nonce` → varying the output of a cryptographic function until it produces the result that is valid in the context of the block
    - It’s a number apparently…
- E.g. if you wanna find something less than `0x1000000...` then the result would start with `0x0100` or whatever
- The smaller the target, the more computations you would need

```python
import hashlib

x = 1
while x: 
    output = hashlib.sha256(str(x).encode()).hexdigest()
    output = str(output)
    print(f"FALSE: {output}, {x}")
    if output[:9] == "000000000":
        print(f"TRUE: {output}, {x}")
        break
    x += 1

# my code please be nice it just runs through nubmers and doesnt account for like hex HAHA help lah
```

### Difficulty representation

- Bits — `0x1903a30c` (where `0x19` is the hexadecimal digits for the coefficient and `0x03a30c` is the coefficient)
- Formula
    - `target = coefficient * 2^(8 * (exponent - 3))`
        
        ![Screenshot 2023-03-02 at 12.30.34 PM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-03-02_at_12.30.34_PM.png)
        
    - Example’s hexadecimal (image above) — `0x0000000000000003A30C00000000000000000000000000000000000000000000`
    - Miner would find a solution once every 60 days on average with 1Terahash per second… you’re kidding

### Difficult targeting and retargeting

- Adjusted by equilibrium of generating BTC → keep it to generating a block every 10 minutes (depending on how many miners there are)
- Every 2016 blocks, all nodes retarget Proof Of Work difficulty → time took to calculate last 2016 blocks and compares to expected time of 20160 minutes
    - If too fast, difficulty increases, if too slow, it go down
    - Less than a factor of 4 per cycle to avoid crazy fluctuations
- Target difficulty does not depend on transaction volume or value

### Successfully mining the block

- Solution found thanks to nonce increment spams → block sent to all other nodes → receive, validate and propogate → everyone adds to own copy of the blockchain → everyone starts computing the next block

## Validating a new block

- Independently validated by every node in the network
    - Checked against long list of criteria
        
        ![Screenshot 2023-03-02 at 12.39.44 PM.png](%5BQUICKNOTES%5D%20Mastering%20Bitcoin%20c7d595968d064822868bbd61dfd3d1ef/Screenshot_2023-03-02_at_12.39.44_PM.png)
        
- Incentive for honest mining → if it is wrong, then miners would have lost the cost of electricity to power the rigs

## Assembling and selecting chain of blocks

- Once block is chosen, attempts are made to assemble a chain and add it to the blockchain
- Nodes have 3 sets of blocks (disregard invalid ones which are just rejected)
    - Main blockchain — chain with most cumulative difficulty associated with it (might have sibling blocks which are not part of the main chain but are nevertheless valid)
        - Most blocks will take a look at the brand new block, look for the parent hash of the previous block, and just link it to this one
    - Secondary chain — extending off a new block that is not in the main chain that doesn’t fit the main chain
        - If difficulty is harder here is harder than the main chain, then the secondary chain becomes the main chain → if node is miner, it extends this new chain
    - Orphan pool — normally occurs when block that is received in the wrong order has to wait for its parent (still is a legit block)
- Extending chain represents a vote to achieve consensus → everyone is happy if we all just choose the harder block (longest cumulative difficulty chain)

### Blockchain forks

- Fork: temporary inconsistencies between versions of the blockchain → resolved by reconvergence
    - 2 candidate blocks competing to form the longset blockchain → occurs when 2 miners solved Proof Of Work close to each other’s time → broadcast their own solutions → propagate block → if nodes receive blocks, puts one on the main and another on a secondary → then the block chosen as the Hunger Games winner is the one with the “harder” difficulty
    - Any miners that work with the non-chosen chain are suddenly shifted back to the main chain and abandon the non-chosen one (orphans it) → everyone goes back to main chain
- Normally resolved within 1 block

## Mining and hashing race

- Basically → better tech → more mining power → increased difficulty → barrier to entry keeps going up OOF
- At this point it’s about optimizing space for all the chips instead of optimizing the chips themselves

### Extra nonce solution

- Basically, miners exhausted all possible outputs way too fast so they had to make the difficulty harder, e.g. moving block timestamp into many places to exhaust more possibilities → more nonce values → harder to solve

### Mining pools

- Pooling your computer power and then sharing the reward among thousands of other people (as a consumer) → daily returns reduce risk but also less money so sad
- Coordinate 100s of thousands of miners over specialized pool mining protocols → connect to server → leave it running, then reap rewards
    - Pool server collects a % and then splits the rest between the miners who helped (proportionally to how much they contributed)
- Get miners to find lower value hashes even as they all find the one big higher value hash to make it fair and prove their contributions to the pool instead of faking it
- Managed pools
    - Pool operator: manages pools
    - Manages the main node
    - Candidate block header that’s compiled in the main node sent to the miners → mines using block template with lowered difficulty → sends successful results back to earn shares
    - Pool operator could cheat
    - If there is DDos attack, everyone cannot mine
- P2Pool
    - Peer-to-peer mining pool without a central operator
    - Implements sharechain: like a blockchain but different → collab and mine in this decentralised pool → 1 share block every 30 seconds → when one of the miners strikes goal, share block is checked for contributions and then the winnings are distributed evenly
    - Users need to support a full node to use this
    - Susceptible to 51% attack

## Consensus attack

- Does not affect: security and privacy of keys and signing, cannot steal Bitcoins, spend Bitcoins without signatures, redirect bitcoins, change transaction records… can just cause DDos attacks and denial of service disruptions
- 51% attack
    - Group of miners over the majority collude to attack BTC (doesn’t actually need to be 51%, just the hefty majority in a particular chain)
    - Attacker can double spend transaction by invalidating transaction by altering the records through this 51% attack
    - Example
        - Buy $100,000 painting → collude with friend with large mining servers to launch a fork and get that to be the majority in the transaction, so yours is chosen → change your transaction’s UTXO spending to paying yourself so money doesn’t go to painting’s seller → mine another block to make your chain longer and be given precedence
        - To avoid, wait at least 6 blocks+ escrow multisignature account
    - Centralization has been occurring with mining rigs → might only take 1 pool operator to screw everyone over

# 9 Alternative chains, Currencies, and Applications

- Alt coins: currency that uses the same technology but hosted on a completely different network
- Protocol layers (e.g. meta coins, meta chains, blockchain apps) → use blockchain as app platform/extend BTC by adding protocol layers
- Alt chains: Using the blockchain concept but not to implement currency
    - Implementing consensus ledger as platform for contracts, name register, and other apps
    - E.g. Ethereum

### Meta-coin platforms

- Meta coins and meta chains are software layers implemented over BTC → currency inside currency/platform or protocol overlay inside BTC system
- Coloured coins — essentially a currency with its own special trade meaning layered atop another currency
    - Meta protocol that overlays information on small amounts of BTC — adds a layer with a special meaning (using its metadata)
    - Can be bought/sold/divided/undivided and if needed to be, uncoloured
    - Convert specific, small amount of BTC to a traded cert that represents the ownership of another asset
    - Managed by specialized wallets
    - E.g. Mastercoin, Counterparty (coin to purchase financial assets)
- Alt coins
    - Might be derived from BTC i.e. yoinking BTC source code/made “from scratch” like relying on BTC model
    - E.g. Litecoin
    - Difference from BTC
        - Different monetary policy
        - Different proof-of-work/consensus mechanisms
        - Specific features e.g. strong anonimity
    - Evaluating alt coins
        - Conceptual metrics: significant innovation? Succinctly different from BTC? Difference enough to compel users to switch from BTC? Address interesting/niche market? Attract enough miners to be secured against consensus attacks?
        - Financial metrics: Total market capitalization? Estimated users? Accepted by merchants? Number of consistent transactions? Daily value of transactions?
        - Money generation would differ for alt coins as compared to BTC e.g. Litecoin will have 84 million coins by 2140
- Consensus innovation
    - Scrypt introduced as alternative for POW → mining more CPU friendly and less susceptible to centralization
    - Proof of stake: owners stake a currency as interest bearing collateral → can earn investment return in the form of new currency/transaction fees
        - E.g. Peercoin, Ethereum, Myriad, Blackcoin, Vericoin, NXT (go research NXT it looks very promising because it has name registry, decentralized asset exchange, decentralized and integrated messaging, and stake delegation)
- Dual purpose mining innovation
    - Solving useful problem + producing proof of work to secure the network
    - Addresses the concern of “wasteful” mining
    - Risk: adding external use to the currency can also risk having extraneous variables influence the supply and demand curve
    - E.g. Primecoin, Curecoin, Gridcoin (allows users to share their computing power for academic computing)
- Anonimity focussed alt coins
    - BTC is actually quite easy to connect profiles to people to see their spending habits → these alt coins try to prevent that
    - E.g. Zerocoin/zerocash, CryptoNote, Bytecoin, Monero, Darkcoin

### Non-currency alt chains

- Alternative implementations of blockchain design pattern that are not used as currency
    - Used to allocate something else, e.g. resource or contract
- Namecoin (NMC)
    - Used to register names and information about a person
    - Stats are same as BTC e.g. block generation time is 10 minutes
    - Must format all this in a preset manner
    - Must update all your information approximately once every 250 days (which can be done with `name_firstupdate`)
- BitMessage
    - Decentralized messaging system → serverless encrypted system
    - If messages are not persistent and are deleted after 2 days — if not delivered to destination node in time, they are lost
    - Strongly authenticated (cannot be spoofed) and pseudonymous (only see address)
- Ethereum (YAYYYY)
    - Turing complete contract processing and execution platform based on a blockchain ledger
    - Ethereum contracts are like little scripts that can execute vending machine instructions

### Future of currencies

- TLDR: Lots of things will be decentralized, BTC isn’t the best but has opened up many doors for more exciting executions → lower cost of organization and coordination on large scale systems → lower concentration of power, corruption, and regulatory capture

# 10 Bitcoin Security

### Security principles

- Responsbility and control on the end user → since it is on Proof Of Work and not access control, no need to encrypt stuff
- BTC transactions are extremely set —  only authorized to give a certain amount of money to a certain person and cannot be forged or modified, and doesn’t reveal any private information
- Secure development
    - Don’t take control/keys away from users and don’t take transactions off the blockchain - e.g. doing all the transactions on a centralized system and then syncing it to the blockchain every few days or so
- The root of trust
    - Trusted core used as the foundation for security of overall application/system → place the root of trust in a simple system that is not likely to break (the more layers you add on, the easier it is to get bugs that are likely to break the system)
        - Traditional security architecture
    - Blockchain genesis block is the root of trust and everything is built up from there → since it is immutable and decentralized, it is very trustworthy
        - Take care not to put too much trust into the infrastructure built on top of BTC, trust BTC itself because that is trustless, if that makes sense
    - Fun fact: some early BTC wallets were centralised… and then everything went up in smoke when security breaches happened

### User security best practices

- Lots of incentives to hack BTC — if you do, can just digitally transfer assets that have intrinsic value already (but here are ways that we shall try and counter them)
- Physical BTC storage
    - Paper wallet — printing your address and key onto a sheet of paper
    - Cold storage — keys generated offline and stored on paper/digital media or a USB stick
- Hardware wallets: foolproof level of security to non expert users
- Balancing risk (loss v theft): To prevent theft, owners of 7000 BTC made complicated series of backups and lost the encryption keys
- Diversifying risk: spread money around many wallets
- Multi-sig and governance: require more than 1 signature to make a payment/redundancy (one person generates a few keys that they can sign with for a transaction so you don’t end up having one compromised then cry)
- Survivability: share details with trusted lawyer/family member so they can access it when you’re gone (can use multi sig and leave one with family, one with lawyer)