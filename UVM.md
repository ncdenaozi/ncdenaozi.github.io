# UVM and Design Verification Method

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


## UVM Advanced

## UVM reference implementation


