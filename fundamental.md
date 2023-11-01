# 數位設計基本原理

- [卡諾圖化簡](#卡諾圖化簡)
- [二補數的-1除以2等於多少](#二補數的-1除以2等於多少)
- [Flip-Flop, Latch的差異](#flip-flop-latch的差異)
- [RCA和CLA有甚麼差異及各自的優缺點](#rca和cla有甚麼差異及各自的優缺點)
- [cache的功能](#cache的功能)
- [Direct Memory Access的運作原理](#direct-memory-access的運作原理)
- [Reference](#reference)


## 卡諾圖化簡

卡諾圖通常用於最小化邏輯閘的數量，以節省硬件資源並提高電路的效能。

|  cd\ab  |  00  |  01  |  11  |  10  |
|:-------:|:----:|:----:|:----:|:----:|
| 00      |  1   |  1   |  0   |  1   |
| 01      |  1   |  0   |  0   |  1   |
| 11      |  0   |  1   |  1   |  1   |
| 10      |  1   |  1   |  0   |  0   |

<details>
    <summary>Answer</summary>
    <code>out = (~a & ~d) + (~b & ~c) + (~a & b & c) + (a & c & d)</code>
</details> <br>

|  cd\ab  |  00  |  01  |  11  |  10  |
|:-------:|:----:|:----:|:----:|:----:|
| 00      |  d   |  0   |  1   |  1   |
| 01      |  0   |  0   |  d   |  d   |
| 11      |  0   |  1   |  1   |  1   |
| 10      |  0   |  1   |  1   |  1   |

```d is don't-care```
<details>
    <summary>Answer</summary>
    <code>out = a + (~b & c)</code>
</details> <br>

|  cd\ab  |  00  |  01  |  11  |  10  |
|:-------:|:----:|:----:|:----:|:----:|
| 00      |  0   |  1   |  0   |  1   |
| 01      |  1   |  0   |  1   |  0   |
| 11      |  0   |  1   |  0   |  1   |
| 10      |  1   |  0   |  1   |  0   |

<details>
    <summary>Answer</summary>
    <code>out = ((a ^ b) & ~(c ^ d)) + ((c ^ d) & ~(a ^ b))</code>
</details> <br>

|  cd\ab  |  00  |  01  |  11  |  10  |
|:-------:|:----:|:----:|:----:|:----:|
| 00      |  d   |  0   |  d   |  d   |
| 01      |  0   |  d   |  1   |  0   |
| 11      |  1   |  1   |  d   |  d   |
| 10      |  1   |  1   |  0   |  d   |

```d is don't-care```
<details>
    <summary>Answer</summary>
    <code>out = (c & d) + (c & ~d & ~a) + (~c & d & b) + (~c & ~d & a)</code>
</details> <br>


## 二補數的-1除以2等於多少

$無號數N(N ≠ 0)，基底（base）r，n位整數的r補數:$
$r^n-N$

1. $(012398)_{10}\ 的10’s\ complement = 10^6 − 012398 = 987602$
2. $(1101100)_2\ 的2’s\ complement = 2^7 − 1101100 = 0010100$

> 重要性質：r’s complement = (r – 1)’s complement + 1
> 
> Eq. 2's complement = 1's complement + 1
<br>

Q1: $(0101)_2\ 的\ 2's補數的-1除以\ 2=?$
<details>
    <summary>Answer</summary>
    <pre><code>
        0101的2's補數的 - 1 = 0101的1's補數 = 1010
        1010除以2 = 1010 >>> 1 = 1101 
    </code></pre>
</details> <br>

Q2: $(11010)_2\ 的\ 2's補數的-1除以\ 2=?$
<details>
    <summary>Answer</summary>
    <pre><code>
        11010的2's補數的 - 1 = 11010的1's補數 = 00101
        00101除以2 = 00101 >>> 1 = 00010 
    </code></pre>
</details> <br>


## Flip-Flop, Latch的差異

<details>
    <summary>Answer</summary>
    <p>
        Flip-Flop, Latch 都是記憶單元，最主要差異是觸發的機制，Flip-Flop 是邊緣觸發，Latch 則是準位觸發。雖然 Flip-Flop 的面積比 Latch 大很多，但在設計上通常還是會避免使用到 Latch。因為準位觸發對電路 glitch 的敏感性較高，導致電路的低穩定性；而 Flip-Flop 的邊緣觸發只有在觸發時才會有讀寫的動作，在非觸發階段輸入與輸出無關，電路有較高的穩定性和可靠性。
    </p>
</details> <br>


## RCA和CLA有甚麼差異及各自的優缺點

<details>
    <summary>Answer</summary>
    <p>RCA和CLA在設計和性能方面有明顯區別。RCA是串行加法器，每一位的進位信號必須逐位傳播，因此速度較慢，但結構較簡單且需要較少硬體資源。CLA則是平行運算的加法器，可同時計算進位信號，因此速度較快，但電路較複雜且可能消耗較多功耗。</p>
    <table>
    <thead>
        <tr>
        <th style="width:20%"></th>
        <th style="width:40%">Ripple-Carry Adder (RCA)</th>
        <th style="width:40%">Carry-Lookahead Adder (CLA)</th>
        </tr>
    </thead>
    <tbody>
        <tr>
        <td>運算速度</td>
        <td>較慢，進位信號逐位傳遞</td>
        <td>較快，平行運算進位信號</td>
        </tr>
        <tr>
        <td>延遲</td>
        <td>較高</td>
        <td>較低</td>
        </tr>
        <tr>
        <td>硬體資源需求</td>
        <td>較低</td>
        <td>較高</td>
        </tr>
        <tr>
        <td>優點</td>
        <td>結構規則、電路簡單、面積小</td>
        <td>運算複雜度較低，延遲時間短</td>
        </tr>
        <tr>
        <td>缺點</td>
        <td>高位元運算需等待低位元運算完成，延遲時間較長</td>
        <td>電路複雜度較高、面積大</td>
        </tr>
    </tbody>
    </table>
</details> <br>


## cache的功能



## Direct Memory Access的運作原理



## Reference
- [r補數與(r − 1)補數](http://publish.get.com.tw/bookpre_pdf/U0107A-1.PDF)
- [Flip-Flop和Latch](https://zhuanlan.zhihu.com/p/58613051)
- [flipflop和latch以及register的區別](https://www.twblogs.net/a/5b8ad83b2b71775d1ce97a67)
- [Digital system Class note](https://hackmd.io/@college/HksIhvwtD#128---class-note)
- [進位選擇加法器之設計摘要](http://ir.lib.ncut.edu.tw/bitstream/987654321/2326/2/%E9%80%B2%E4%BD%8D%E9%81%B8%E6%93%87%E5%8A%A0%E6%B3%95%E5%99%A8%E4%B9%8B%E8%A8%AD%E8%A8%88.pdf)
- [加法器的實現及優化](https://www.twblogs.net/a/5d21a78bbd9eee1e5c83bd9b)