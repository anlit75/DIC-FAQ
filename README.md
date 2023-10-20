# 數位IC設計面試常見問題

- [數位IC設計面試常見問題](#數位ic設計面試常見問題)
  - [數位設計基本原理](#數位設計基本原理)
  - [時序分析](#時序分析)
  - [電路設計和實現](#電路設計和實現)
  - [Verilog相關](#verilog相關)
  - [IC Design Flow](#ic-design-flow)
  - [CDC (Clock Domain Crossing)](#cdc-clock-domain-crossing)
  - [專業領域](#專業領域)
  - [其他](#其他)

## 數位設計基本原理

- [卡諾圖化簡](fundamental.md/#卡諾圖化簡)
- [二補數的-1除以2等於多少](fundamental.md/#二補數的-1除以2等於多少)
- [Flip-Flop, Latch的差異](fundamental.md/#flip-flop-latch的差異)
- RCA和CLA有甚麼差異及各自的優缺點
- cache的功能
- Direct Memory Access的運作原理

## 時序分析

- setup/hold time 畫圖解釋
- 怎麼修setup/hold time
- timing violation會發生甚麼事
- timing violation怎麼處理
- 從CLK1傳到CLK2為甚麼需要第二級Filp-Flop

## 電路設計和實現

- 用MUX設計and邏輯閘
- 加法器設計
- 4對1多工器
- 除頻器
- input每個cycle都會輸入0或1
- 取絕對值的電路怎麼設計
- 設計電路判斷{10110}後拉1(分別用FSM、非FSM設計，並比較2者缺點)
- 設計deglitch filter, 將cycle1、2的pulse濾除, 並讓cycle3及以上的pulse通過
- 每個cycle都會傳入1 bit訊號, 從LSB開始, 當再任意時刻停止傳送, 如何知道data是否可以被7整除

## Verilog相關

- [always @(posedge clk or negedge rst)中有寫negedge rst跟沒寫的差異](verilog.md/#always-posedge-clk-or-negedge-rst中有寫negedge-rst跟沒寫的差異)
- [case條件沒寫滿會合成什麼電路](verilog.md/#case條件沒寫滿會合成什麼電路)
- [case、if else差別](verilog.md/#caseif-else差別)
- [給code判斷是組合邏輯還是循序邏輯](verilog.md/#給code判斷是組合邏輯還是循序邏輯)
- [combinational、sequential電路差異](verilog.md/#combinationalsequential電路差異)
- [blocking/non blocking差異](verilog.md/#blockingnon-blocking差異)
- 除了用*來實現乘法外還有什麼方式可以實現

## IC Design Flow

- 整條design flow說明
- 合成要怎麼下constraint才能決定adder要用RCA還是CLA
- 合成要下哪些constraint
- 合成要準備哪些檔案
- 合成時怎麼定義technology corner(PVT condition)
- 合成時若pipeline還是無法解決timimg violation還有什麼處理方式
- 合成時下constraint multi-cycle的目的
- False path的目的
- timimg violation時slack是正還負
- 怎麼判斷input/output delay要設多少
- 說明STA在做什麼
- STA和DTA的差異

## CDC (Clock Domain Crossing)

- CDC怎麼處理
- Asynchronous FIFO具體怎麼處理CDC問題
- CDC path上若有combinational電路會有甚麼影響
- multi-bit的CDC訊號怎麼傳播並畫出電路
- multi-bit的CDC訊號傳播有哪些方法
- 如何解決低頻clk傳數據到高頻clk造成高頻clk重覆取資料的問題, 並畫出電路圖

## 專業領域

- low power method
- 給w/r速率計算FIFO depth
- MCU中pipeline的目的
- pipeline的缺點
- GAA和FinFET有什麼差異

## 其他

- 為甚麼想轉做數位IC
- 為什麼不做類比
- 怎麼評估你已經準備好了
