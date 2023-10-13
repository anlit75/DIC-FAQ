# 數位設計基本原理

- [數位設計基本原理](#數位設計基本原理)
  - [卡諾圖化簡](#卡諾圖化簡)
  - [二補數的-1除以2等於多少](#二補數的-1除以2等於多少)
  - [Flip-Flop, Latch的差異](#flip-flop-latch的差異)

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
$$r^n-N$$

1. $(012398)_{10}\ 的10’s\ complement = 10^6 − 012398 = 987602$
2. $(1101100)_2\ 的2’s\ complement = 2^7 − 1101100 = 0010100$

> 重要性質：$r’s\ complement = (r – 1)’s\ complement + 1$
> 
> Eq. $2's\ complement = 1's\ complement + 1$
<br>

Q1: $(0101)_2\ 的2's補數的-1除以2=?$
<details>
    <summary>Answer</summary>
    <pre><code>
        0101的2's補數的 - 1 = 0101的1's補數 = 1010
        1010除以2 = 1010 >>> 1 = 1101 
    </code></pre>
</details> <br>

Q2: $(11010)_2\ 的2's補數的-1除以2=?$
<details>
    <summary>Answer</summary>
    <pre><code>
        11010的2's補數的 - 1 = 11010的1's補數 = 00101
        00101除以2 = 00101 >>> 1 = 00010 
    </code></pre>
</details> <br>

## Flip-Flop, Latch的差異

<br>
