###Smart Contract in Bitcoin (Public-Permissionless Blockchain)

###Smart Contract in Ethereum (Public Blockchain)
~~~~
contract HelloWorld {
    uint public balance;
    function HelloWorld(){
        balance = 1000;
    }
    function deposit(uint _value) returns(uint _newValue){
        balance += _value;
        return balance;
    }
}
~~~~

###Smart Contract in Hyperledger (Public-Permissioned Blockchain)
In hyperledger the code for smart contract is called chaincode. Confidentiality for chaincodes and state is provided through symmetric-key encryption of transactions and states with a blockchain-specific key that is available to all peers with an enrollment certificate for the blockchain. Extending the encryption mechanisms towards more fine-grained confidentiality for transactions and state entries is planned for a future version.

####Architecture
The validating peers run a BFT consensus protocol for executing a replicated state
machine that accepts three types of transactions as operations:

* Deploy transaction: Takes a chaincode (representing a smart contract) written in Go as a parameter; the
chaincode is installed on the peers and ready to be invoked.
* Invoke transaction: Invokes a transaction of a particular chaincode that has been installed earlier through
a deploy transaction; the arguments are specific to the type of transaction; the chaincode executes the
transaction, may read and write entries in its state accordingly, and indicates whether it succeeded or
failed.
* Query transaction: Returns an entry of the state directly from reading the peer’s persistent state; this
may not ensure linearizability

Validation of transactions occurs through the replicated execution of the chaincode and given the fault assumption underlying BFT consensus, i.e., that among the n validating peers at most  $f < n/3$  may “lie” and behave arbitrarily, but all others execute the chaincode correctly. When executed on top of PBFT consensus, it is important that chaincode transactions are deterministic, otherwise the state of the peers might diverge. A modular solution to filter out non-deterministic transactions that are demonstrably diverging is available and has been implemented in the SIEVE protocol.

