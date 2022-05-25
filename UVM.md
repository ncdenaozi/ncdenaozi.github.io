# UVM and Design Verification Method

Following content mainly derived from Verification Academy's UVM cookbook and Coverage Cookbook.

## UVM basic concept
### UVM compoenenet
![image](https://user-images.githubusercontent.com/52019188/169725830-8f2963bc-aebd-45cf-878d-09a5b47b37f2.png)
 - Each UVM testbench is interface specific.
 - uvm_sequence_item/transaction is a uvm_object that contains the data to implement the protocol and communicate with the DUT.
 - one agent per DUT connection.
 - agent may reuse sequencer to generate different transactions.
 - UVM environment encapsulate agent and other analysis components. It can be configured by configuration object.
 - UVM test may build upon these components at a higher view with parameters.
 - UVM top module drives the whole testbench in a run_test() task.

### UVM compoenenet hierarchy
![image](https://user-images.githubusercontent.com/52019188/169726303-30376e28-28d4-4e17-b527-9f07e1ffd6d6.png)
![image](https://user-images.githubusercontent.com/52019188/169726556-c836ce32-1ddb-4a9b-8102-92c78bae1530.png)

### UVM Factory
The purpose of the UVM factory is to enable an object of one type to be substituted with an object of a derived type without changing the testbench structure or even the testbench code.

Following steps need to be taken.
- Registration
- Default constructor
- Component and Object Creation

### UVM Phase
![image](https://user-images.githubusercontent.com/52019188/169726888-2cc29e2d-64cb-4937-81cc-83f58db46898.png)

### UVM Driver
The UVM driver is responsible for communicating at the transaction level with the sequence via TLM (producer-comsumer relationship) communication with the sequencer and converting between the sequence_item on the transaction side and pin-level activity in communicating with the DUT via a virtual interface.

### UVM Monitor
A Monitor communicates with DUT signals through a virtual interface, and contains code that recognizes protocol patterns in the signal activity. Once a protocol pattern is recognized, a Monitor builds an abstract transaction model representing that activity, and broadcasts the transaction to any interested components. Monitor is alike Driver but always remain passive modules.

### UVM Agent
![image](https://user-images.githubusercontent.com/52019188/170361762-9390a955-30e9-4702-a7fc-7bab144878f9.png)

- "BFM" stands for "Bus Functional Model", meaning strictly the driving and response to the DUT's interface, it has also taken in the loose sense connotations of verification. With the advent of newer technologies including assertions and UVM, that term "BFM" is a little passe and is replaced with terms that are more descriptives. And you are correct, these terms include drivers (the strict definition of a BFM), sequence items or transactions (e.g., READ, WRITE, IDLE, .. ) sequence (the flow of transactions, e.g., a READ, followed by 2 IDLEs, followed by a WRITE, and then a WRITE, etc...), monitors (keep track of what is going on), scoreboards (to do the checking of what is expected against what is happening), assertions (SVA provides a concise notation to specify requirements and properties of the design and does on the fly verification in simulation, and can be used in formal verification), tests (the selected set of environments to use for a simulation (drivers, sequences, parameters, etc).

## UVM Advanced

## UVM reference implementation


