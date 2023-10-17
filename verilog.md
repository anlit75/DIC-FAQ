# Verilog相關

- [Verilog相關](#verilog相關)
    - [always @(posedge clk or negedge rst)中有寫negedge rst跟沒寫的差異](#always-posedge-clk-or-negedge-rst中有寫negedge-rst跟沒寫的差異)
    - [case條件沒寫滿會合成什麼電路](#case條件沒寫滿會合成什麼電路)
    - [case、if else差別](#caseif-else差別)
    - [給code判斷是組合邏輯還是循序邏輯](#給code判斷是組合邏輯還是循序邏輯)
    - [combinational、sequential電路差異](#combinationalsequential電路差異)
    - [blocking/non blocking差異](#blockingnon-blocking差異)

## always @(posedge clk or negedge rst)中有寫negedge rst跟沒寫的差異


## case條件沒寫滿會合成什麼電路

```verilog
module case_x(
    input a,
    input b, 
    input c,
    input [1:0] sel, 
    output reg out
    );
    
    always @(*) begin
        case (sel)
            2'd0: out = a;
            2'd1: out = b;
            2'd2: out = c;
        endcase
    end
endmodule
```
<details>
    <summary>Answer</summary>
    <p>當條件沒有寫完整且出現沒有定義的條件時，輸出訊號會默認保持原樣，因此合成電路時會產生額外的記憶單元 Latch 及其控制訊號。</p>
    <img src="./img/case_x.png">
    <a href="#caseif-else差別">case條件寫完整的電路</a>
</details> <br>

## case、if else差別

```verilog
module if_complete(
    input a,
    input b, 
    input c,
    input [1:0] sel, 
    output reg out
    );
    
    always @(*) begin
        if (sel == 0) out = a;
        else if (sel == 1) out = b;
        else out = c;
    end
endmodule


module case_complete(
    input a,
    input b, 
    input c,
    input [1:0] sel, 
    output reg out
    );
    
    always @(*) begin
        case (sel)
            2'd0: out = a;
            2'd1: out = b;
            2'd2: out = c;
            default: out = 0;
        endcase
    end
endmodule
```
<details>
    <summary>Answer</summary>
    <p>case、if else 的差別在於 if else 具有階層性，條件寫得越上面的具有越高的優先權，因此會生成多個2對1多工器串接在一起；case 則不具有階層性，會直接生成一個多對1多工器。</p>
    <h3>if else: </h3>
    <img src="./img/if_complete.png">
    <h3>case: </h3>
    <img id="case_complete" src="./img/case_complete.png">
</details> <br>

## 給code判斷是組合邏輯還是循序邏輯


## combinational、sequential電路差異


## blocking/non blocking差異

