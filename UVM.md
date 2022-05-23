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


## UVM Advanced

## UVM reference implementation


