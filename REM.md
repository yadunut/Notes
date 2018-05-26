# Chapter 1 - Basic Concepts

<!-- markdownlint-disable MD025 -->

## Convert **Binary** to **Decimal**

binary 1011 = decimal 11

| $2^3$ | $2^2$ | $2^1$ | $2^0$ |
| :---: | :---: | :---: | :---: |
| 1     | 0     | 1     | 1     |

$11 = 2^3 + 2^1 + 2^0$

## Convert **Unsigned Decimal** to **Binary**

| Division | Quotient | Reminder |
| :------: | :------: | :------: |
| 37 / 2   | 18       | 1        |
| 18 / 2   | 9        | 0        |
| 9 / 2    | 4        | 1        |
| 4/2      | 2        | 0        |
| 2/2      | 1        | 0        |
| 1/2      | 0        | 1        |

`decimal 37 = binary 100101`

## Binary Addition

Start with *least* significant bit

| 2^4   | 2^3   | 2^2   | 2^1   | 2^0   |
| :---: | :---: | :---: | :---: | :---: |
| 0     | 1     | 0     | 1     | 0     |
| 0     | 1     | 1     | 0     | 0     |
| 1     | 0     | 1     | 1     | 0     |
$01010 + 01100 = 10110$

## Binary to Hex

**Each** *Hex* digit translates to **4** *binary* digits

| Binary | Decimal | Hexadecimal |       | Binary | Decimal | Hexadecimal |
| :----: | :-----: | :---------: | :---: | :----: | :-----: | :---------: |
| 0000   | 0       | 0           |       | 1000   | 8       | 8           |
| 0001   | 1       | 1           |       | 1001   | 9       | 9           |
| 0010   | 2       | 2           |       | 1010   | 10      | A           |
| 0011   | 3       | 3           |       | 1011   | 11      | B           |
| 0100   | 4       | 4           |       | 1100   | 12      | C           |
| 0101   | 5       | 5           |       | 1101   | 13      | D           |
| 0110   | 6       | 6           |       | 1110   | 14      | E           |
| 0111   | 7       | 7           |       | 1111   | 15      | F           |

## Hex to Decimal

| Division | Quotient | Reminder |
| :------: | :------: | :------: |
| 422 / 16 | 26       | 6        |
| 26 / 16  | 1        | A        |
| 1 / 16   | 0        | 1        |

`decimal 422 = Hex 1A6`

## Signed Integers

**Highest** bit indicates sign. `1 = negative, 0 = positive`

If highest digit of hex > 7, value is negative

## Two's Complement

Negative Numbers stored in two's complement notation

For -1
| Instruction    | Binary   |
| :------------- | :------: |
| Starting Value | 00000001 |
| Reverse Bits   | 11111110 |
| Plus 1         | 11111111 |

`-1 is represented as 11111111 in a 1 byte binary`

## Binary Subtraction

$00001100 - 00000011 = 00001100 + (-00000011)$
| Instruction    | Binary   |
| :------------- | :------: |
| Starting Value | 00000011 |
| Reverse Bits   | 11111100 |
| Plus 1         | 11111101 |

$00001100 +$

$11111101 =$

$00001001$

$00001100 - 00000011 = 00001001$

## Boolean Algebra

### NOT

| X     | Not X |
| :---: | :---: |
| F     | T     |
| T     | F     |

### AND

| X     | Y     | X AND Y |
| :---: | :---: | :---: |
| F     | F     | F     |
| F     | T     | F     |
| T     | F     | F     |
| T     | T     | T     |

### OR

| X     | Y     | X AND Y |
| :---: | :---: | :---: |
| F     | F     | F     |
| F     | T     | T     |
| T     | F     | T     |
| T     | T     | T     |

# Chapter 2 - x86 Processor Architecture