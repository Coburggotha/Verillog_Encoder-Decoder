# Verillog_Encoder-Decoder
Verillog_Encoder&amp;Decoder

● Encoder

```
/*Encoder Module*/

module encoder (iIN, oOUT);
  input [9:0] iIN;
  output [3:0] oOUT;
  
  reg [3:0] out;
  
always @(iIN) begin
  case(iIN)
    // 98 7654 3210 <-- KEY PAD NUMBER
    10'b00_0000_0001 : out = 4'b0000;
    10'b00_0000_0010 : out = 4'b0001;
    10'b00_0000_0100 : out = 4'b0010;
    10'b00_0000_1000 : out = 4'b0011;
    10'b00_0001_0000 : out = 4'b0100;
    10'b00_0010_0000 : out = 4'b0101;
    10'b00_0100_0000 : out = 4'b0110;
    10'b00_1000_0000 : out = 4'b0111;
    10'b01_0000_0000 : out = 4'b1000;
    10'b10_0000_0000 : out = 4'b1001;
    default : out = 4'b1111;
    
  endcase
end
assign oOUT = out;

endmodule

```
## Code Capture
<img width="812" height="660" alt="스크린샷 2025-09-17 160024" src="https://github.com/user-attachments/assets/762f95fa-f76a-4649-ae37-8a0bebd80698" />





- Test Bench

```

`timescale 1ns/10ps

module tb_encoder;
  reg [9:0] iIN;
  wire [3:0] oOUT;
  
  encoder U0 (
  .iIN (iIN),
  .oOUT (oOUT));
  
  initial begin
    iIN = 10'b00_0000_0001; #100;
    iIN = 10'b00_0000_0010; #100;
    iIN = 10'b00_0000_0100; #100;
    iIN = 10'b00_0000_1000; #100;
    iIN = 10'b00_0001_0000; #100;
    iIN = 10'b00_0010_0000; #100;
    iIN = 10'b00_0100_0000; #100;
    iIN = 10'b00_1000_0000; #100;
    iIN = 10'b01_0000_0000; #100;
    iIN = 10'b10_0000_0000; #100;

end


endmodule

```







● Decoder

- Case 문

```

/* 2-to-10 Decoder Module*/

module decoder (iIN, oOUT);
  input [3:0] iIN;
  output [9:0] oOUT;
  
  reg [9:0] out;
  
  always @(iIN) begin
    case (iIN)
    0 : out = 10'b00_0000_0001; 
    1 : out = 10'b00_0000_0010;
    2 : out = 10'b00_0000_0100; 
    3 : out = 10'b00_0000_1000; 
    4 : out = 10'b00_0001_0000; 
    5 : out = 10'b00_0010_0000; 
    6 : out = 10'b00_0100_0000; 
    7 : out = 10'b00_1000_0000;
    8 : out = 10'b01_0000_0000;
    9 : out = 10'b10_0000_0000; 
    default : out = 10'b11_1111_1111;

endcase
end

assign oOUT = out;

endmodule

```




-Test Bench

```

`timescale 1ns/10ps
module tb_decoder;
  reg[3:0] iIN;
  wire [9:0] oOUT;
  integer i;
  
  decoder U0(
  .iIN (iIN),
  .oOUT (oOUT));
  
  initial begin
    iIN = 0;
    for (i=0; i<= 10; i= i+1)
    #100 iIN = iIN + 1;
  end
  
endmodule

```











● VIVADO  Encoder



코드는 동일, xdc 포트는 아래와 같이 수정




Schematic




Basys 보드 동작 확인 이상 無 > VIVADO Simulation 설정 ILA 





- 코드에 clk 추가, probe 코드 추가. 

- module encoder 에도 clk 추가 하고 input 도 추가해야한다..






0000000010 = 0001




0000000100 = 0010




● VIVADO  Dencoder

코드는 동일, xdc 포트는 아래와 같이 수정





Basys 보드 동작 확인 이상 無 > VIVADO Simulation 설정 ILA 







- 코드에 clk 추가, probe 코드 추가. 

- module encoder 에도 clk 추가 하고 input 도 추가해야한다




0000 = 0000000001




0010 = 0000000100


