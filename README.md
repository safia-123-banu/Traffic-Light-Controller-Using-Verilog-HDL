# Traffic-Light-Controller-Using-Verilog-HDL
Aim
To design and simulate a traffic light controller using Verilog HDL, and verify its functionality through a testbench in the Vivado 2023.1 simulation environment. The objective is to control the traffic lights for a junction with a specific time-based sequence for Red, Yellow, and Green lights.

Apparatus Required
Vivado 2023.1 or equivalent Verilog simulation tool.
Computer system with a suitable operating system.
FPGA board (optional for hardware verification).
Procedure
Launch Vivado 2023.1:

Open Vivado and create a new project.
Design the Traffic Light Controller Verilog Code:

Write the Verilog code for the traffic light controller, using an FSM (Finite State Machine) to transition between Green, Yellow, and Red lights based on timing intervals.
Create the Testbench:

Write a testbench to simulate the traffic light controller. The testbench will check the sequence of light transitions based on time.
Add the Verilog Files:

Add the traffic light controller Verilog code and the testbench file to the project.
Run Simulation:

Run the behavioral simulation in Vivado to verify the correct sequence of the traffic lights.
Observe the Waveforms:

Examine the waveform output to verify that the traffic light transitions through the Green, Yellow, and Red lights in the correct sequence.
Save and Document Results:

Capture screenshots of the waveform and save the simulation logs to include in your report.

Verilog Code for Traffic Light Controller

// traffic_light_controller.v
module TRAFFICLIGHT(
input wire clk,
input wire reset,
output reg [2:0] lights);
parameter Green  = 2'b00;
parameter Yellow = 2'b01;
parameter Red    = 2'b10;
reg [1:0] current_state, next_state;
reg [3:0] counter;
always @(posedge clk or posedge reset)
begin
if (reset) 
begin
current_state <= Green;
counter <= 0;
end 
else
begin
if (counter == 4'd9)
begin
current_state <= next_state;
counter <= 0;
end 
else 
begin
counter <= counter + 1;
end
end
end
always @(*) 
begin
case (current_state)
Green: begin
lights = 3'b001;
next_state = Yellow;
end
Yellow: begin
lights = 3'b010;
next_state = Red;
end
Red: begin
lights = 3'b100;
next_state = Green;
end
default: begin
lights = 3'b000;
next_state = Green;
end
endcase
end
endmodule






![Screenshot 2024-10-05 163058](https://github.com/user-attachments/assets/10336cc9-db6e-4442-aa46-fba7f11b7708)


Testbench for Traffic Light Controller

// traffic_light_controller_tb.v
`timescale 1ns / 1ps

module TESTBENCH_TRAFFIC;
reg clk;
reg reset;
wire [2:0] lights;
TRAFFICLIGHT uut(.clk(clk),.reset(reset),.lights(lights));
always #5 clk = ~clk;
initial
begin
clk=0;
reset=1;
#10 reset = 0;
#100 $stop;
end
initial
begin
$monitor("Time=%0t | Lights (R Y G) = %b", $time, lights);
end
endmodule









![Screenshot 2024-10-05 163058](https://github.com/user-attachments/assets/675b786d-1392-4d04-bfb2-b755f2883718)


Conclusion
In this experiment, a traffic light controller was successfully designed and simulated using Verilog HDL. The design controlled the traffic lights to switch between Green, Yellow, and Red in a cyclic manner based on timing intervals. The testbench verified that the traffic lights followed the correct sequence and timing. The simulation results confirm the correct functionality of the traffic light controller, demonstrating the effectiveness of Verilog HDL in designing FSM-based controllers for real-world applications.
