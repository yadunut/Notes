<!-- markdownlint-disable MD025 MD033-->

# Reverse Engineering Malware

- [Reverse Engineering Malware](#reverse-engineering-malware)
- [Chapter 1 - Basic Concepts](#chapter-1---basic-concepts)
  - [Convert **Binary** to **Decimal**](#convert-binary-to-decimal)
  - [Convert **Unsigned Decimal** to **Binary**](#convert-unsigned-decimal-to-binary)
  - [Binary Addition](#binary-addition)
  - [Binary to Hex](#binary-to-hex)
  - [Hex to Decimal](#hex-to-decimal)
  - [Signed Integers](#signed-integers)
  - [Two's Complement](#twos-complement)
  - [Binary Subtraction](#binary-subtraction)
  - [Boolean Algebra](#boolean-algebra)
    - [NOT](#not)
    - [AND](#and)
    - [OR](#or)
- [Chapter 2 - x86 Processor Architecture](#chapter-2---x86-processor-architecture)
  - [General Purpose Registers](#general-purpose-registers)
  - [Accessing Parts of a register](#accessing-parts-of-a-register)
  - [Specialized Register Uses](#specialized-register-uses)
    - [General Purpose](#general-purpose)
    - [Segment](#segment)
    - [Special](#special)
- [Chapter 3 - Fundamentals](#chapter-3---fundamentals)

# Chapter 1 - Basic Concepts

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
| :---: | :---: | :-----: |
| F     | F     | F       |
| F     | T     | F       |
| T     | F     | F       |
| T     | T     | T       |

### OR

| X     | Y     | X AND Y |
| :---: | :---: | :-----: |
| F     | F     | F       |
| F     | T     | T       |
| T     | F     | T       |
| T     | T     | T       |

# Chapter 2 - x86 Processor Architecture

## General Purpose Registers

Storage Locations inside CPU, optimized for speed.

| 32 Bit General | Purpose Registers |
| :------------: | :---------------: |
| EAX            | EBP               |
| EBX            | ESP               |
| ECX            | ESI               |
| EDX            | EDI               |

| 16 Bit Segment | Registers |
| :------------: | :-------: |
| CS             | FS        |
| DS             | GS        |
| ES             | SS        |

|Special Registers|
|:---:|
|EFLAGS|
|EIP|

## Accessing Parts of a register

Use 8 bit, 16 bit or 32 bit name

Each `|   |` space represents 8 bits

```demo
|   |   |   |   |   - EAX
        |   |   |   - AX
        |   |       - AL
            |   |   - AX
```

***The 16 and 8 Bit registers are accessing the values in the EAX***

The E in EAX stands for `extended`, extending the range of the 16 bit registers to 32 bits

EAX, EBX, ECX, EDX have both 16 bit and 8 bit names

EBP, ESP, ESI, EDI only have 16 bit names

## Specialized Register Uses

### General Purpose

| Register | Use                                 |
| :------: | :---------------------------------- |
| E**A**X  | **A**ccumulator                     |
| E**C**X  | Loop **C**ounter                    |
| E**SP**  | **S**tack Pointer                   |
| ES**I**  | Index Register                      |
| ED**I**  | Index Register                      |
| EB**P**  | **B**ase **P**ointer(Frame Pointer) |

### Segment

| Register | Use                    |
| :------: | :--------------------- |
| CS       | **C**ode **S**egment   |
| DS       | **D**ata **S**egment   |
| SS       | **S**tack **S**egment  |
| ES       | Additional **S**egment |
| FS       | Additional **S**egment |
| GS       | Additional **S**egment |

### Special

| Register | Use                                                  |
| :------: | :--------------------------------------------------- |
| EIP      | Instruction Pointer                                  |
| EFLAGS   | Status and Control Flag<br>Each Flag is a single **bit** |

# Chapter 3 - Fundamentals