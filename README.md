# FSM_for_Sequence_Detector
# EXP NO.6.A. Sequence Detector Using Moore Machine and Mealy Machine

# Aim
To design and simulate a Finite-State-Machine-for-Sequence-Detector-1011 using Verilog HDL, and verify its functionality through a testbench in the Vivado 2023.1 environment.

# Apparatus Required
Vivado 2023.1

# Procedure
1.  Launch Vivado 2023.1 Open Vivado and create a new project.
2.  Design the Verilog Code Write the Verilog code for the RAM,ROM,FIFO Create the Testbench Write a testbench to simulate the memory behavior.
3.  The testbench should apply various and monitor the corresponding output.
4.  Create the Verilog Files Create both the design module and the testbench in the Vivado project. Run Simulation Run the behavioral simulation to verify the output.
5.  Observe the Waveforms Analyze the output waveforms in the simulation window, and verify that the correct read and write operation.
6.  Save and Document Results Capture screenshots of the waveform and save the simulation logs. These will be included in the lab report.

# Code
# Mealy 1011
// Verilog code
// Verilog code
`timescale 1ns / 1ps
//////////////////////////////////////////////////////////////////////////////////
// Company: 
// Engineer: 
// 
// Create Date: 06.08.2026 17:48:00
// Design Name: 
// Module Name: moore
// Project Name: 
// Target Devices: 
// Tool Versions: 
// Description: 
// 
// Dependencies: 
// 
// Revision:
// Revision 0.01 - File Created
// Additional Comments:
// 
//////////////////////////////////////////////////////////////////////////////////


module moore_1011(
    input clk,
    input rst,
    input x,
    output reg y
);

reg [2:0] state;

parameter S0 = 3'b000;
parameter S1 = 3'b001;
parameter S2 = 3'b010;
parameter S3 = 3'b011;
parameter S4 = 3'b100;

always @(posedge clk or posedge rst)
begin
    if(rst)
        state <= S0;
    else
    begin
        case(state)

            S0:
                if(x)
                    state <= S1;
                else
                    state <= S0;

            S1:
                if(x)
                    state <= S1;
                else
                    state <= S2;

            S2:
                if(x)
                    state <= S3;
                else
                    state <= S0;

            S3:
                if(x)
                    state <= S4;
                else
                    state <= S2;

            S4:
                state <= S0;

            default:
                state <= S0;

        endcase
    end
end

always @(*)
begin
    case(state)
        S4: y = 1;
        default: y = 0;
    endcase
end

endmodule

// Test bench
// Test bench
`timescale 1ns / 1ps
//////////////////////////////////////////////////////////////////////////////////
// Company: 
// Engineer: 
// 
// Create Date: 06.08.2026 17:50:20
// Design Name: 
// Module Name: tb_moore
// Project Name: 
// Target Devices: 
// Tool Versions: 
// Description: 
// 
// Dependencies: 
// 
// Revision:
// Revision 0.01 - File Created
// Additional Comments:
// 
//////////////////////////////////////////////////////////////////////////////////




module moore_1011_tb;

reg clk;
reg rst;
reg x;

wire y;

moore_1011 uut(
    .clk(clk),
    .rst(rst),
    .x(x),
    .y(y)
);

always #5 clk = ~clk;

initial
begin
    clk = 0;
    rst = 1;
    x = 0;

    #20;
    rst = 0;

    // Input sequence : 1011
    #10 x = 1;
    #10 x = 0;
    #10 x = 1;
    #10 x = 1;

    #30;

    $finish;
end

endmodule



// output Waveform

<img width="1587" height="892" alt="image" src="https://github.com/user-attachments/assets/db74ab59-5314-444b-a0da-2d3b228d1253" />


# Moore 1011
// write verilog code for ROM using $random
// write verilog code for ROM using $random
module mealy_1011(
    input clk,
    input rst,
    input x,
    output reg y
);

reg [1:0] state;

parameter S0 = 2'b00,
          S1 = 2'b01,
          S2 = 2'b10,
          S3 = 2'b11;

always @(posedge clk or posedge rst)
begin
    if(rst)
    begin
        state <= S0;
        y <= 0;
    end
    else
    begin
        y <= 0;

        case(state)

        S0:
            if(x)
                state <= S1;
            else
                state <= S0;

        S1:
            if(x)
                state <= S1;
            else
                state <= S2;

        S2:
            if(x)
                state <= S3;
            else
                state <= S0;

        S3:
        begin
            if(x)
            begin
                y <= 1;
                state <= S0;
            end
            else
                state <= S0;
        end

        endcase
    end
end

endmodule

// Test bench
`timescale 1ns / 1ps
//////////////////////////////////////////////////////////////////////////////////
// Company: 
// Engineer: 
// 
// Create Date: 06.08.2026 18:03:57
// Design Name: 
// Module Name: tb_mealy
// Project Name: 
// Target Devices: 
// Tool Versions: 
// Description: 
// 
// Dependencies: 
// 
// Revision:
// Revision 0.01 - File Created
// Additional Comments:
// 
//////////////////////////////////////////////////////////////////////////////////





module tb_mealy;

reg clk;
reg rst;
reg x;

wire y;

mealy_1011 uut(
    .clk(clk),
    .rst(rst),
    .x(x),
    .y(y)
);

always #5 clk = ~clk;

initial
begin
    clk = 0;
    rst = 1;
    x = 0;

    #20 rst = 0;

    // Input: 1011
    #10 x = 1;
    #10 x = 0;
    #10 x = 1;
    #10 x = 1;

    #30;
    $finish;
end

endmodule


// output Waveform

<img width="1577" height="887" alt="image" src="https://github.com/user-attachments/assets/a8fa51cf-17e6-4bde-8d42-56795dc589f7" />


# Conclusion 
The Mealy and Moore state machine for sequence 1011 was designed and successfully simulated using Verilog HDL. The testbench verified both the write and read functionalities by simulating the sequence operations and observing the output waveforms.

