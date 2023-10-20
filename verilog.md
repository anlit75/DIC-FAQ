# Verilog相關

- [Verilog相關](#verilog相關)
    - [always @(posedge clk or negedge rst)中有寫negedge rst跟沒寫的差異](#always-posedge-clk-or-negedge-rst中有寫negedge-rst跟沒寫的差異)
    - [case條件沒寫滿會合成什麼電路](#case條件沒寫滿會合成什麼電路)
    - [case、if else差別](#caseif-else差別)
    - [給code判斷是組合邏輯還是循序邏輯](#給code判斷是組合邏輯還是循序邏輯)
    - [combinational、sequential電路差異](#combinationalsequential電路差異)
    - [blocking/non blocking差異](#blockingnon-blocking差異)

## always @(posedge clk or negedge rst)中有寫negedge rst跟沒寫的差異

<details>
    <summary>Answer</summary>
    <p>沒寫在 sensitivity list 會是 Synchronous Reset，有寫則是 Asynchronous Reset。</p>
    <p>Synchronous Reset 在電路合成時會合成沒有復位接腳的FF，並且FF的輸入訊號會跟 Reset 訊號 AND 在一起。Asynchronous Reset 則是直接合成出帶有復位接腳的FF。</p>
</details> <br>

```verilog
always @(posedge clk) begin
    if (!rst_n) out <= 0;
    else out <= in;
end
```
<details>
    <summary>Schematic</summary>
    <img src="./img/synch_rst.jpg">
</details> <br>

```verilog
always @(posedge clk or negedge rst_n) begin
    if (!rst_n) out <= 0;
    else out <= in;
end
```
<details>
    <summary>Schematic</summary>
    <img src="./img/asynch_rst.jpg">
</details> <br>

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

```verilog
// blocking
 always @(posedge clk) begin
    b = a;
    c = b;
end

// non-blocking
always @(posedge clk) begin
    b <= a;
    c <= b;
end
```
<details>
    <summary>Answer</summary>
    <p></p>
    <h3>blocking: </h3>
    <img src="./img/blocking.png">
    <img src="./img/blocking_wave.png">
    <h3>non-blocking: </h3>
    <img src="./img/nonblocking.png">
    <img src="./img/nonblocking_wave.png">
</details> <br>

## Refence
- [Synchronous & Asynchronous Reset](https://hackmd.io/@jesse1282/B1tgS0q62)
- [多種時序邏輯always語句的綜合結果與分析](https://zhuanlan.zhihu.com/p/167305718)
- [Reset信號如何同步？](https://zhuanlan.zhihu.com/p/533949746)