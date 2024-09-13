Dual Port RAM Using Verilog
Overview
This project implements a Dual Port RAM using Verilog HDL. Dual-port RAM allows two independent memory access operations (read/write) simultaneously on different or the same addresses. The design supports two separate ports (A and B) with independent addresses, data inputs, and control signals. The module is accompanied by a testbench that simulates various read and write operations to verify the functionality of the design.

File Structure
dual_port_ram.v: Verilog module defining the dual-port RAM functionality.
dual_port_ram_tb.v: Testbench to simulate and verify the dual-port RAM design.
dump.vcd: Value Change Dump (VCD) file generated during the simulation.
Functionality
Dual-Port RAM Design (dual_port_ram.v):
Data width: 8 bits per port.

Address width: 6 bits per port, supporting 64 addresses (0 to 63).

Ports:

Port A and Port B have independent data, address, write-enable, and output signals.
The memory is defined as an 8x64 bit RAM (reg [7:0] ram[63:0]).

For write operations, data is written to the memory at the given address if the write-enable signal (we_a or we_b) is high during the positive edge of the clock.
For read operations, data is read from the memory at the given address when the write-enable signal is low.
Testbench (dual_port_ram_tb.v):
The testbench performs several operations to test the design:

Write operation on Port A and Port B.
Read operation from both ports.
Simultaneous read and write operations on different addresses.
Signal Descriptions:
Inputs:
data_a, data_b: 8-bit input data for Port A and Port B.
addr_a, addr_b: 6-bit addresses for Port A and Port B.
we_a, we_b: Write enable signals for Port A and Port B (1 for write, 0 for read).
clk: Clock signal to synchronize the operations.
Outputs:
q_a, q_b: 8-bit output data for Port A and Port B, driven during read operations.
How to Run
Simulation
Ensure you have a Verilog simulator such as ModelSim, Icarus Verilog, or any equivalent tool.
Compile the Verilog files:
bash
Copy code
iverilog -o dual_port_ram_tb dual_port_ram_tb.v dual_port_ram.v
Run the simulation:
bash
Copy code
vvp dual_port_ram_tb
View the waveform using a VCD viewer (e.g., GTKWave):
bash
Copy code
gtkwave dump.vcd
Expected Output
The testbench will simulate the following operations:

Write data 0x33 to address 0x01 on Port A and 0x44 to address 0x02 on Port B.
Write data 0x55 to address 0x03 on Port A, and then read data from address 0x01 on Port B (expected output 0x33).
Read data from address 0x02 on Port A (expected output 0x44).
Write data 0x77 to address 0x02 on Port B.
Output Waveforms
You can view the simulation waveforms to verify:

Correct read and write operations on Port A and Port B.
Independent functionality of the two ports.
Key Points
The design allows simultaneous access to two memory locations through two ports.
The testbench provides scenarios to test the dual-port functionality.
The code is synthesizable for FPGA implementation, allowing the dual-port RAM to be mapped to FPGA-specific memory blocks.
Future Enhancements
Parameterization: Modify the design to make the data and address widths configurable using Verilog parameters.
Write conflict handling: Add logic to handle cases where both ports attempt to write to the same address.
Author
Ankita Soni
