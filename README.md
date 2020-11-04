# Policies-and-Smart-Contracts
Build on pythagoras
pythagoras provides you with the tools, documentation, and support to help you build your applications. 
Develop privacy-preserving applications on the pythagoras.
# Discret Language
Discret is pythagoras’s domain-specific language. It defines extra rulesets for assets during transaction validation.
Discret enables users to simply and predictably create custom assets and financial instruments, with terms enforced by the pythagoras network.

# Native Smart Contracts
When possible, Pythagoras makes use of stateless smart contracts instead of stateful smart contracts.
Stateful smart contracts are more expressive than stateless contracts, but run the risk of placing a high computational and storage burden on the network validators.
Stateless contracts are a special kind of smart contract that does not have any dynamic state. 
Instead, the smart contract program defines a Boolean function that is run on a bundle of transaction inputs.
If the program returns true then the bundle of transaction inputs are executed atomically and appended to the ledger’s transaction log.
This is similar to policies defined with the Discret language, which are really a special case of stateless smart contracts.
The final transaction bundle also references the smart contract program, which is a content-addressable static data object on the ledger. 
Verifying the transaction bundle requires running the contract program on the bundle and checking the result of the contract program.
Lastly, stateless smart contract functionality can also be achieved using variables and pre-conditions on normal transaction operations. 
For many use cases, placing variables and preconditions on transactions is sufficient to simulate the desired smart contract behavior entirely through native transaction operations. 
Stateless contracts are much better for scalability and are encouraged when stateful contracts can be avoided.
