//write 2017/5/19 //前两天给师弟做ISE的仿真，之前用过vivado和quartus II做仿真，没用过ISE，发现ISE和前两者有一定区别，记载下 //代码如下： //顶层文件：

`timescale 1ns / 1ps
module FB383(clk, rst, speaker); 
input clk,rst; 
output speaker;
// first create a 16bit binary counter 
reg [15:0] counter; 
wire speaker;
always @(posedge clk or posedge rst) 
 begin 
  if(rst) 
    counter <= 1'b0; 
  else 
    counter <= counter + 1'b1;
// and use the most significant bit (MSB) of the counter to drive the speaker 
 end
assign speaker = counter[1];
endmodule
//testbench代码 `timescale 1ns / 1ps
module FB383_tb;
reg clk,rst;
wire speaker;

// Instantiate the Unit Under Test (UUT)
FB383 uut (
	.clk(clk),
	.speaker(speaker),
	.rst(rst)
);
// reg reset; initial begin // Initialize Inputs // Wait 100 ns for global reset to finish clk = 0;
forever   #1 clk = ~clk;
end
 
 initial
 begin
 rst = 0;
 #100 rst = 1;
 #50 rst = 0;
 #10000 $stop;
 end
 
 initial
  $monitor($time,,rst,,clk,,,speaker);
// initial
//	$display("speaker = % h hex % d decimal",speaker,speaker);
    
	// Add stimulus here
endmodule


//两点注意的地方： 
//第一，testbench需要加激励信号，clk和rst都需要。如果不写rst，可能由于输出没有初始化过程， //而导致输出信号一直处于高阻抗状态，那么仿真波形就一直是红色的。
//第二，在创建工程的时候代码标准设置，如下图 //  

![image](https://github.com/tigerZhouCN/picture/blob/master/picture/ISE%E5%B7%A5%E7%A8%8BVerilog%E6%A0%87%E5%87%86%E8%AE%BE%E7%BD%AE.png)

//两个标准，vhdl-93和vhdl-200x是两种不同的语言版本，vhdl-200x提供了一些新的关键字定义。 // 一般默认的是VHDL-93，如果仿真波形不对，可以试着换成VHDL-200X，因为我们现在学的Verilog可能和之前的版本有些不同。 //自己参考，随机应变
