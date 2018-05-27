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
  - [Integer Contstants](#integer-contstants)
  - [Instruction](#instruction)
    - [Label](#label)
    - [Memonic and Operands](#memonic-and-operands)
    - [Comments](#comments)
    - [Instruction Format Example](#instruction-format-example)
  - [Defining Data](#defining-data)
    - [Data Types](#data-types)
    - [Data Definition Statement](#data-definition-statement)
    - [Defining BYTE and SBYTE](#defining-byte-and-sbyte)
    - [Defining Byte Arrays](#defining-byte-arrays)
    - [DUP operator](#dup-operator)
    - [Little Endian order](#little-endian-order)
    - [Declaring uninitialized data](#declaring-uninitialized-data)
  - [Symbolic Constants](#symbolic-constants)
    - [Equals Sign](#equals-sign)
    - [Calculate Size of Arrays and strings](#calculate-size-of-arrays-and-strings)
      - [Byte Array](#byte-array)
      - [Word Array](#word-array)
      - [DWORD Array](#dword-array)
    - [EQU Directive](#equ-directive)
    - [TEXTEQU Directive](#textequ-directive)
- [Chapter 4 - Data Transfer, Addressing and Arithmetic](#chapter-4---data-transfer--addressing-and-arithmetic)

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

| Register | Use                                                      |
| :------: | :------------------------------------------------------- |
| EIP      | Instruction Pointer                                      |
| EFLAGS   | Status and Control Flag<br>Each Flag is a single **bit** |

# Chapter 3 - Fundamentals

## Integer Contstants

| Type  | Letter | Example |
| :---: | :----: | :-----: |
| Hex   | h      | 6Ah     |
| Dec   | d      | 88d     |
| Dec   | 88     |
| Bin   | b      | 001010b |

## Instruction

Instruction Contains

- Label (Optional)
- Memonic (Required)
- Operand (Dependent on Memonic)
- Comment (Optional)

### Label

- Acts as placemarkers
  - Marks offset of code
- Follows identifier rules
- Data Label
  - Must be Unique
  - Example - `MyArray` (No colon after)
- Code Label
  - Target of Jump and Loop instruction
  - Example - `L1:`

### Memonic and Operands

- Instruction Memonics
  - Memory Aid
  - Examples - `MOV, ADD, SUB, MUL, INC, DEC`
- Operand
  - Constant
  - Constant Expression
  - Register
  - Memory (data label)

*Constants and constant expressions are often called **Immediate Values***

### Comments

- Explain programs purpose
- Single Line comments begin with `;`
- Multiline comments begin with COMMENT and a chosen character and ends with the chosen character

### Instruction Format Example

| Example     | Command                                                                       |
| :---------- | :---------------------------------------------------------------------------- |
| No Operand  | `stc  ;set carry flag`                                                        |
| One Operand | `inc eax ;increment register`<br>`inc myByte ; increment memory`              |
| Two Operand | `add eax, ecx  ;register, register`<br>`sub myByte, 25 ;memory, constant`<br> |

## Defining Data

### Data Types

| Unsigned | Signed | Definition                |
| :------- | :----- | :------------------------ |
| BYTE     | SBYTE  | 8 bit (un)signed integer  |
| WORD     | SWORD  | 16 bit (un)signed integer |
| DWORD    | SDWORD | 32 bit (un)signed integer |
| QWORD    |        | 64 bit unsigned integer   |
| TBYTE    |        | 80 bit integer            |
| REAL4    |        | 4-byte IEEE short real    |
| REAL8    |        | 8-byte IEEE short real    |
| REAL10   |        | 10-byte IEEE short real   |

### Data Definition Statement

- Sets aside storage in memory for a variable
- Optionally assign a name(label) to the data
- Syntax
  - `Name Type Initializer`
  - `value1 BYTE 10`

### Defining BYTE and SBYTE

| Code                | Definition             |
| :------------------ | :--------------------- |
| `value1 BYTE 'A'`   | character constant     |
| `value2 BYTE 0`     | smallest unsigned byte |
| `value3 BYTE 255`   | largest unsigned byte  |
| `value4 SBYTE -128` | largest signed byte    |
| `value5 SBYTE +127` | largest signed byte    |
| `value6 BYTE ?`     | uninitialized byte     |

### Defining Byte Arrays

```asm
list1 BYTE 10, 20, 30, 40
list2 BYTE 00100010b, ?, 'a', 14h
list3 BYTE 50, 60, 70, 80
      BYTE 90, 100, 110, 120
str1  BYTE "This is a string", 0
str2  BYTE 'A', 'E', 'I', 'O', 'U'
str3  BYTE 'The 0 at the end is a null termination'.
           'This is a multi line string'
str4 BYTE '0Dh is carriage return, 0Ah is line feed', 0Dh, 0Ah,
          'This causes it to go to new line'
```

### DUP operator

Use DUP to allocate space for array or string

syntax: `count DUP`

```asm
var1 BYTE 20 DUP(0) ;20 bytes, all equal to 0
var2 BYTE 20 DUP(?) ;20 bytes, all uninitialized
var3 BYTE 4 DUP("Hi");8 bytes, "HiHiHiHi"
```

### Little Endian order

All data types larger than a byte store data in little endian order.
*Least Significant Byte* Occurs at the first memory address

val1 DWORD = 12345678h
| Memory Address | Data |
| :------------- | :--- |
| 0000           | 78   |
| 0001           | 56   |
| 0002           | 34   |
| 0003           | 12   |

### Declaring uninitialized data

- Use the `.data?` directive to declare uninitialized data segment
- Within the segment, declare variables with "?" initializer
  - Example - `smallArray DWORD 10 DUP(?)`

## Symbolic Constants

### Equals Sign

- `name = expression`
  - expression is a 32 bit integer
  - may be redefined
  - name is called `symbolic constant`
- good programming style to use symbols

```asm
COUNT = 500
...
mov ax, COUNT
```

### Calculate Size of Arrays and strings

- Current location counter - $
  - subtract from address of array
  - difference is no of bytes

#### Byte Array

```asm
list BYTE 10, 20, 30, 40
listSize = ($ - list)      ; 4
```

#### Word Array

```asm
list WORD 1000h, 2000h, 3000h, 4000h
listSize = ($ - list)/2      ; 4
```

#### DWORD Array

```asm
list DWORD 1000h, 2000h, 3000h, 4000h
listSize = ($ - list)/4      ; 4
```

### EQU Directive

Define symbol as integer or text expression. **Cannot Be redefined**

Will act as if 

```asm
PI EQU <3.1416>
pressKey EQU <"Press any key to continue", 0>
.data
prompt BYTE pressKey
```

### TEXTEQU Directive

Define symbol as integer or text expression. **Can Be redefined**

Called Text Macro

```asm
continueMessage TEXTEQU <"Do You wish to continue (Y/N)?", 0>
rowSize = 5
.data
prompt1 BYTE continueMessage
count TEXTEQU %(rowSize * 2) ;Evaluaets this expression and sets count to 10
setupAL TEXTEQU <mov, al, count>

.code
setupAL ;generates mov al, 10
```

# Chapter 4 - Data Transfer, Addressing and Arithmetic