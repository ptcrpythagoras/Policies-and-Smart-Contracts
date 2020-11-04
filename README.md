# Policies-and-Smart-Contracts
Build on pythagoras
pythagoras provides you with the tools, documentation, and support to help you build your applications. 
Develop privacy-preserving applications on the pythagoras.
# Discret Language
---
Discret is pythagoras’s domain-specific language. It defines extra rulesets for assets during transaction validation.
Discret enables users to simply and predictably create custom assets and financial instruments, with terms enforced by the pythagoras network.

# Native Smart Contracts
---
When possible, Pythagoras makes use of stateless smart contracts instead of stateful smart contracts.
Stateful smart contracts are more expressive than stateless contracts, but run the risk of placing a high computational and storage burden on the network validators.
Stateless contracts are a special kind of smart contract that does not have any dynamic state. 
Instead, the smart contract program defines a Boolean function that is run on a bundle of transaction inputs.
If the program returns true then the bundle of transaction inputs are executed atomically and appended to the ledger’s transaction log.
This is similar to policies defined with the Discret language, which are really a special case of stateless smart contracts.
The final transaction bundle also references the smart contract program, which is a content-addressable static data object on the ledger. 
Verifying the transaction bundle requires running the contract program on the bundle and checking the result of the contract program.
Lastly, stateless smart contract functionality can also be achieved using variables and pre-conditions on normal transaction operations. 
For many use cases, placing variables and preconditions on transactions is sufficient to simulate the desired smart contract behavior entirely through native transaction operations. Stateless contracts are much better for scalability and are encouraged when stateful contracts can be avoided.
# Variable addresses and pre-conditions can be defined in transactions.
---
An operation will specify a variable destination address [x], for example “transfer 100 USD from address A to [x]”, and then a list of pre-conditions that the variable [x] must satisfy for the operation to become valid. The pre-conditions may include:

 
Ops: Other operations involving the same address [x]. These operations must be included in the same transaction’s list of operations.
UTXOs: UTXOs that are included as inputs to the transaction. The pre-condition may specify explicitly the addresses and amounts involved in the UTXO, or alternatively specify variable addresses and variable amounts along with policies that must evaluate to true on the variable addresses and variable amounts.
Policy: A policy applies to the variables referenced in the ops or UTXOs. Supported native policies include a credential requirement on address variables in the ops or UTXOs, and arithmetic expressions on transfer amount variables. Evaluating the policy may require auxiliary inputs, such as a credential proof or other privacy-preserving compliance proof. These inputs would be provided in the memo field of the transaction.

 

In pseudocode, an example operation with a variable address [x], variable amount [y], and pre-conditions is:
### Operation A
{“Transfer from addrA to [x] 300 USD token”
pre-conditioned on Op1: “Transfer from [x] to addrA [y] TCEHY tokens”
Policy1: A credential proof that [x] is accredited
Policy2: y >= 1
}

The validator processes transactions with variables and pre-conditions by scanning the list of operations and substituting variables until all the pre-conditions on each transaction are satisfied. For the above example, suppose that a new Operation B was added to the transaction operation list:

### Operation B  
{“Transfer from addrB to [x] 1 TCEHY tokens”
pre-conditioned on
Op1: “Transfer from [x] to addrB [y] USD tokens”
Policy1: y > 275 <proof of addrB accreditation>
}
Then the validator would process this transaction and substitute for the variables. The resolutions executes:
{“Transfer from addrA to addrB 300 USD” “Transfer from addrB to addrA 1 TCEHY”
