# 數位設計基本原理

- [卡諾圖化簡](#1-1)
- [二補數的-1除以2等於多少](#1-2)
- [Flip-Flop、Latch的差異](#1-3)

<h2 id="1-1">卡諾圖化簡</h2>
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

<h2 id="1-2">二補數的-1除以2等於多少</h2>

<br>

<h2 id="1-3">Flip-Flop、Latch的差異</h2>

<br>
