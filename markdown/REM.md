<!-- markdownlint-disable MD025 MD033 MD024-->

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
  - [Data Transfer Instructions](#data-transfer-instructions)
    - [Operand Types](#operand-types)
    - [Direct Memory Operands](#direct-memory-operands)
    - [MOV instruction](#mov-instruction)
    - [Zero Extension](#zero-extension)
    - [Sign Extension](#sign-extension)
    - [XCHG Instruction](#xchg-instruction)
    - [Direct-Offset Operands](#direct-offset-operands)
    - [Challenge - Program that makes a array of 1,2,3 to 3,1,2](#challenge---program-that-makes-a-array-of-1-2-3-to-3-1-2)
  - [Addition and Subtraction](#addition-and-subtraction)
    - [INC and DEC Instructions](#inc-and-dec-instructions)
    - [ADD and SUB operations](#add-and-sub-operations)
    - [NEG (negate) operation](#neg-negate-operation)
  - [Flags affected by arithmetic](#flags-affected-by-arithmetic)
    - [Zero Flag (ZF)](#zero-flag-zf)
    - [Sign Flag (SF)](#sign-flag-sf)
    - [Hardware viewpoint on signed and unsigned](#hardware-viewpoint-on-signed-and-unsigned)
    - [Carry Flag (CF)](#carry-flag-cf)
      - [Too Big](#too-big)
      - [Too Small](#too-small)
    - [SF,ZF,CF Demo](#sf-zf-cf-demo)
    - [Overflow Flag (OF)](#overflow-flag-of)
  - [Data-related addressing](#data-related-addressing)
    - [OFFSET Operator](#offset-operator)
    - [PTR Operator](#ptr-operator)
    - [TYPE Operator](#type-operator)
    - [LENGTHOF Operator](#lengthof-operator)
    - [SIZEOF Operator](#sizeof-operator)
    - [Spanning Multiple lines](#spanning-multiple-lines)
    - [LABEL Directive](#label-directive)
  - [Indirect Addressing](#indirect-addressing)
    - [Indirect Operands](#indirect-operands)
    - [Array Sum Example](#array-sum-example)
    - [Indexed Operands](#indexed-operands)
  - [JMP and LOOP instructions](#jmp-and-loop-instructions)
    - [JMP instruction](#jmp-instruction)
    - [LOOP instruction](#loop-instruction)
    - [LOOP Example](#loop-example)
    - [Nested Loop](#nested-loop)
    - [Summing integer array](#summing-integer-array)
    - [Copying a string](#copying-a-string)
- [Chapter 5 - Procedure](#chapter-5---procedure)
  - [Stack operations](#stack-operations)
    - [Runtime stack](#runtime-stack)
    - [PUSH Operation](#push-operation)
    - [POP Operation](#pop-operation)
    - [Using PUSH and POP](#using-push-and-pop)
    - [Example - Nested Loops](#example---nested-loops)
    - [Related Instructions](#related-instructions)
  - [Defining and using Procedures](#defining-and-using-procedures)
    - [Creating Procedures](#creating-procedures)
    - [Documenting Procedues](#documenting-procedues)
    - [Example](#example)
    - [CALL and RET instructions](#call-and-ret-instructions)
    - [CALL-RET Example](#call-ret-example)
    - [Local and Global Labels](#local-and-global-labels)
    - [Procedure Parameters](#procedure-parameters)
- [Conditional Processing](#conditional-processing)
  - [Boolean and Comparison Instructions](#boolean-and-comparison-instructions)
    - [Status Flags Review](#status-flags-review)
    - [AND instruction](#and-instruction)
    - [OR Instruction](#or-instruction)
    - [XOR Instruction](#xor-instruction)
    - [NOT Instruction](#not-instruction)
    - [Applications](#applications)
    - [Test](#test)
    - [CMP Instruction](#cmp-instruction)
      - [Destination == Source](#destination-source)
      - [Destination < Source](#destination-source)
      - [Destination > Source](#destination-source)
    - [Comparison with signed integers](#comparison-with-signed-integers)
      - [Destination > Source](#destination-source)
      - [Destination < Source](#destination-source)
  - [Conditional Jumps](#conditional-jumps)
    - [Jump Based on Specific Flags](#jump-based-on-specific-flags)
    - [Jump based on Equality](#jump-based-on-equality)
    - [Jump based on Unsigned Comparisons](#jump-based-on-unsigned-comparisons)
    - [Jump based on Signed comparisons](#jump-based-on-signed-comparisons)
    - [Applications](#applications)
    - [Encrypting a string](#encrypting-a-string)
  - [Conditional Loop instructions](#conditional-loop-instructions)
    - [LOOPZ and LOOPE](#loopz-and-loope)
    - [LOOPNZ and LOOPNE](#loopnz-and-loopne)
  - [Conditional Control flow Drectives](#conditional-control-flow-drectives)
    - [Runtime Expressions](#runtime-expressions)
    - [Relational and Logical Operators](#relational-and-logical-operators)
    - [MASM generated code](#masm-generated-code)
    - [.REPEAT directive](#repeat-directive)
    - [.WHILE directive](#while-directive)

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

If highest digit of **hex > 7**, value is **negative**

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

Can store a **DWORD**

| 32 Bit General | Purpose Registers |
| :------------: | :---------------: |
| EAX            | EBP               |
| EBX            | ESP               |
| ECX            | ESI               |
| EDX            | EDI               |

Can store a **WORD**

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
|   |   |           - AX
|   |               - AL
    |   |           - AH
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

| Unsigned | Signed | Definition                | Unsigned Range | Signed Range            |
| :------- | :----- | :------------------------ | :------------: | :---------------------- |
| BYTE     | SBYTE  | 8 bit (un)signed integer  | 0 to 255       | -128 to 127             |
| WORD     | SWORD  | 16 bit (un)signed integer | 0 to $2^{16}$  | -$2^{15}$ to $2^{15}-1$ |
| DWORD    | SDWORD | 32 bit (un)signed integer | 0 to $2^{32}$  | -$2^{31}$ to $2^{31}-1$ |
| QWORD    |        | 64 bit unsigned integer   | 0 to $2^{64}$  | -$2^{63}$ to $2^{63}-1$ |
| TBYTE    |        | 80 bit integer            | 0 to $2^{80}   |
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

```x86asm
list1 BYTE 10, 20, 30, 40
list2 BYTE 00100010b, ?, 'a', 14h
list3 BYTE 50, 60, 70, 80
      BYTE 90, 100, 110, 120
str1  BYTE "This is a string", 0
str2  BYTE 'A', 'E', 'I', 'O', 'U'
str3  BYTE 'The 0 at the end is a null termination' .
           'This is a multi line string'
str4 BYTE '0Dh is carriage return, 0Ah is line feed', 0Dh, 0Ah,
          'This causes it to go to new line'
```

### DUP operator

Use DUP to allocate space for array or string

syntax: `count DUP`

```x86asm
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

```x86asm
COUNT = 500
...
mov ax, COUNT
```

### Calculate Size of Arrays and strings

- Current location counter - $
  - subtract from address of array
  - difference is no of bytes

#### Byte Array

```x86asm
list BYTE 10, 20, 30, 40
listSize = ($ - list)      ; 4
```

#### Word Array

```x86asm
list WORD 1000h, 2000h, 3000h, 4000h
listSize = ($ - list)/2      ; 4
```

#### DWORD Array

```x86asm
list DWORD 1000h, 2000h, 3000h, 4000h
listSize = ($ - list)/4      ; 4
```

### EQU Directive

Define symbol as integer or text expression. **Cannot Be redefined**

Will act as if

```x86asm
PI EQU <3.1416>
pressKey EQU <"Press any key to continue", 0>
.data
prompt BYTE pressKey
```

### TEXTEQU Directive

Define symbol as integer or text expression. **Can Be redefined**

Called Text Macro

```x86asm
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

## Data Transfer Instructions

### Operand Types

- Immediate - constant integer
  - value encoded within instruction
- register - name of register
  - register name is converted to a number and encoded within instruction
- Memory - Reference to location in memory
  - Memory address is encoded within the instruction, or register holds address of memory location

### Direct Memory Operands

- Direct memory operand is a named reference to storage in memory
- Named reference (label) is automatically dereferenced by the assembler
- `[var]` is similar to `*var` in c.

```x86asm
.data
var1 BYTE 10h   ;var1 points to the memory location of the array
.code
mov al,var1
mov al,[var1]   ;Alternate notation
```

### MOV instruction

- Move from source to destination.
  - Syntax - `MOV destionation,source`
- No more than 1 memory operand allowed
- **CS**, **EIP**, **IP** cannot be the destination
- No immediate to segment mmoves

TODO: Find out whether endianness affects this

```x86asm
.data
count BYTE 100
wVal  WORD 2
.code
mov bl,count      ;bl = 100
mov ax,wVal       ;ax = 2
mov count,al      ;count = ?

mov al,wVal       ;error since wVal bigger than al
mov ax,count      ;error ?Type mismatch?
mov eax,count     ;error ?Type mismatch?
```

More Errors

```x86asm
.data
bval  BYTE  100
bVal2 BYTE  ?
wVal  WORD  2
dVal  DWORD 5
.code
mov ds,45       ;move to DS not permitted
mov esi,wVal    ;size mismatch, esi is 32 bits, wVal is 16 bits
mov eip,dVal    ;eip cannot be destination
mov 25,bVal     ;immediate value cannot be register
mov bVal2,bVal  ;memory to memory move not permitted
```

### Zero Extension

When you copy a *smaller* value to a larger destination, the **MOVZX** instruction fills the upper half of destination with *Zeros*

Destination **MUST** be a register

```x86asm
mov bl,10001111b    ;8 bits
movzx ax,bl         ;ax = 0000 0000 1000 1111, upper half filled with 0s
```

### Sign Extension

The **MOVSX** instruction fills the upper half of the destination with a copy of the souce operand's sign bit

Destination **MUST** be a register

```x86asm
mov bl,10001111b    ;8 bits
movsx ax,bl         ;ax = 1111 1111 1000 1111, upper half filled with sign bit
```

### XCHG Instruction

**XCHG** exchanges the values of 2 operands. At least 1 operand must be register. No Immediate Operands permitted.

```x86asm
.data
var1 WORD 1000h
var2 WORD 2000h
.code
xchg ax,bx      ;exchange 16-bit regs
xchg ah,al      ;exchange 8-bit regs
xchg var1,bx    ;exchange mem,reg
xchg var1,var2  ;error: 2 memory operands
```

### Direct-Offset Operands

constant offset is added to data label to produce an effective address. The address is dereferenced to get value inside its memory location.

Byte example

```x86asm
.data
arrayB BYTE 10h, 20h, 30h, 40h
.code
mov al,arrayB+1   ;AL = 20h
mov al,[arrayB+1] ;Alternate notation.
```

Word/DWord Example

```x86asm
.data
arrayW WORD   1000h,2000h,3000h,4000h
arrayD DWORD  1,2,3,4
.code
mov ax,[arrayW+2]   ;ax = 2000h
mov ax,[arrayW+4]   ;ax = 3000h
mov eax,[arrayD+4]  ;eax = 2
```

### Challenge - Program that makes a array of 1,2,3 to 3,1,2

```x86asm
.data
arrayD DWORD 1,2,3
.code
mov  eax,[arrayD]     ;eax = 1
xchg eax,[arrayD+4]   ;eax = 2, arrayD = 1,1,3
xchg eax,[arrayD+8]   ;eax = 3, arrayD = 1,1,2
mov [arrayD],eax      ;arrayD = 3,1,2
```

## Addition and Subtraction

### INC and DEC Instructions

- `inc destination`
  - Logic <-- Destination + 1
- `dec destination`
  - Logic <-- Destination - 1

```x86asm
.data
myWord  WORD  1000h
.code
inc myWord    ;myWord = 1001h
mov ax,00ffh
inc ax        ;ax = 0100h
```

### ADD and SUB operations

- `add destionation source`
  - Logic <-- destionation + source
- `sub destionation source`
  - Logic <-- destionation - source
- **Same rules as the `mov` instruction**

```x86asm
.data
var1 DWORD 10000h
var2 DWORD 20000h
.code
mov eax, var1   ;eax = 10000h
add eax,var2    ;eax = 30000h
```

### NEG (negate) operation

Reverses the sign of an operand. Can be register or memory

```x86asm
.data
valB BYTE -1
valW WORD +32767
.code
mov al,valB     ;al = -1
neg al          ;al = 1
```

## Flags affected by arithmetic

- ALU has status flags that reflect outcome of arithmetic and bitwise operations based on content of destination operand
  - Zero Flag - When destination = 0
  - Sign Flag - Destination is negative
  - Carry Flag - when unsigned value out of range
  - Overflow Flag - when signed value out of range
- `mov` instruction never affects the flags

### Zero Flag (ZF)

occurs when result of operation produces zero in destination

```x86asm
mov cx,1
sub cx,1        ;cx = 0, ZF = 1
mov ax,0FFFFh
inc ax          ; ax = 0; ZF = 1
inc ax          ; ax = 1; ZF = 0
```

### Sign Flag (SF)

set when destination operand is negative. Flag is cleared when destination is positive

```x86asm
mov cx,0      ;cx = 0
dec cx        ;cx = -1, SF = 1
add cx,2      ;cx = 1, SF = 0
```

*Signed flag is **Destionations** highest bit*

```x86asm
mov al,0        ;al = 0
sub al,1        ;al = 1111 1111b, SF = 1
add al,2        ;al = 0000 0001b, SF = 0
```

### Hardware viewpoint on signed and unsigned

CPU operations work exactly the same on unsigned and signed operations. *It doesnt care whether the value is signed or unsigned*. It just sets the appropriate sign flags.

### Carry Flag (CF)

set when results of operation generates unsigned value that is out of range

#### Too Big

```x86asm
mov al,0FFh
inc al          ;AL = 0, CF = 1
```

#### Too Small

```x86asm
mov al,0
dec al      ;AL = FF, CF = 1
```

### SF,ZF,CF Demo

```x86asm
mov ax,00FFh      ; ax = 00FFh, SF = 0, ZF = 0, CF = 0
add ax,1
sub ax,1
add al,1
mov bh,6Ch
add bh,95h

mov al,2
sub al,3
```

### Overflow Flag (OF)

set when signed result of operation is invalid / out of range

```x86asm
mov al,127    ;al = 127, OF = 0
inc al        ;al = -128, OF = 1, Harder to read.
```

```x86asm
mov al,7Fh    ;al = 7Fh = 127, OF = 0
inc al        ;al = 80h = 128, OF = 1
```

2nd one is easier to check whether negative cause If highest digit of hex > 7, value is negative

- Overflow flags are only set when
  - 2 positive operands are added and their sum is negative
  - 2 negative operands are added and their sum is positive

```x86asm
mov al,80h      ;al = 80h, OF = 0
add al,92h      ;al = 3, OF = 1  ;overflow cause al is only 8 bits and result is 9 bits
```

## Data-related addressing

### OFFSET Operator

returns distance in bytes, of a label from beginning of its enclosing statements

```x86asm
;Assume data segment begins at 0040 4000h
.data
bVal  BYTE  ?
wVal  WORD  ?
dVal  DWORD ?
dVal2 DWORD ?
.code
mov esi,OFFSET bVal     ;esi = 0040 4000h
mov esi,OFFSET wVal     ;esi = 0040 4001h
mov esi,OFFSET dVal     ;esi = 0040 4003h
mov esi,OFFSET dVal2     ;esi = 0040 4007h
```

Value returned by OFFSET is a pointer

```c
char array[1000];
char *p = array;
```

```x86asm
.data
array BYTE 1000 DUP(?)
.code
mov esi, OFFSET array
```

### PTR Operator

overrides the default type of label(variable). allows you to access part of the variable

```x86asm
.data
myDouble DWORD 12345678h
.code
mov ax,myDouble           ;error cause myDouble 32 bits, ax 16 bits
mov ax,WORD PTR myDouble  ;ax = 5678h cause little endian
mov WORD PTR myDouble,1234h ;saves 1234h, myDouble = 12341234h (TODO: PLS CHECK)
```

```x86asm
.data
myDouble DWORD 12345678h
mov al,BYTE PTR myDouble        ;al = 78h
mov al,BYTE PTR [myDouble+1]    ;al = 56h
mov al,BYTE PTR [myDouble+2]    ;al = 34h
mov ax,WORD PTR myDouble        ;ax = 5678h
mov ax,WORD PTR [myDouble+2]    ;ax = 1234h
```

PTR can be used to combine elements of smaller data type and move them to larger operand

```x86asm
.data
myBytes BYTE 12h,34h,56h,78h
.code
mov ax,WORD PTR [myBytes]     ;ax = 3412h
mov ax,WORD PTR [myBytes+2]   ;ax = 7856h
mov eax,DWORD PTR myBytes     ;eax = 78563412h
```

### TYPE Operator

returns size, in bytes, of a single element of a data declaration

```x86asm
.data
var1 BYTE   ?
var2 WORD   ?
var3 DWORD  ?
var4 QWORD  ?

.code
mov eax, TYPE var1    ;eax = 1
mov eax, TYPE var2    ;eax = 2
mov eax, TYPE var3    ;eax = 4
mov eax, TYPE var4    ;eax = 8
```

### LENGTHOF Operator

counts no of elements in a single data declaration

```x86asm
.data
                                  ;LENGTHOF
byte1     BYTE  10,20,30          ;3
array1    WORD  30 DUP(?),0,0     ;30 + 2 = 32
array2    WORD  5 DUP(3 DUP(?))   ;3 * 5 = 15
array3    DWORD 1,2,3,4           ;4
digitstr  BYTE  "12345678",0      ;9

.code
mov eax,LENGTHOF array1           ;32

```

### SIZEOF Operator

equals to lengthof * type

```x86asm
.data
                                  ;SIZEOF
byte1     BYTE  10,20,30          ;3
array1    WORD  30 DUP(?),0,0     ;30 + 2 = 32 * 2 = 64
array2    WORD  5 DUP(3 DUP(?))   ;3 * 5 = 15 * 2 = 30
array3    DWORD 1,2,3,4           ;4 * 4 = 16
digitstr  BYTE  "12345678",0      ;9

.code
mov eax,LENGTHOF array1           ;32 * 4 = 64
```

### Spanning Multiple lines

- data declaration can span multiple lines if each line ends with comma

```x86asm
.data
array WORD  10,20,
            30,40,
            50,60
.code
eax,LENGTHOF array    ;eax = 6
eax,SIZEOF array      ;eax = 12
```

### LABEL Directive

TODO: ASK HOW THIS WORKS

## Indirect Addressing

### Indirect Operands

Indirect operand holds the address of a variable, usually an address or string. It can be dereferenced.

```x86asm
.data
val1 BYTE 10h,20h,30h
.code
mov esi,OFFSET val1   ;stores the address of val1
mov al,[esi]          ;al = 10h, dereferences ESI and gets the value out

inc esi
mov al,[esi]          ;al = 20h, dereferences ESI and gets the value out

inc esi
mov al,[esi]          ;al = 30h, dereferences ESI and gets the value out
```

Use `PTR` to clarify the size attribute of memory operand

TODO: ASK ABOUT THIS

```x86asm
.data
myCount WORD 0

.code
mov esi,OFFSET myCount    ;stores the address of myCount
inc [esi]                 ;error since inc doesn't know the type of the value underneath
inc WORD PTR [esi]        ;ok as inc now knows the value underneath
```

### Array Sum Example

indirect operands are optimal for traversing arrays.

**Note:** *Register in brackets must be incremented by a value that matches array type*

```x86asm
.data
arrayW  WORD  1000h,2000h,3000h
.code
mov esi, OFFSET arrayW        ;esi stores address of arrayW
mov ax,[esi]                  ;ax stores 1000h
add esi,TYPE arrayW           ;esi now has the address of the next element of arrayW
add ax,[esi]                  ;ax = 3000h
add esi,TYPE arrayW           ;esi now has the address of the next element of arrayW
add ax,[esi]                  ;ax = 6000h
```

### Indexed Operands

index operands add a constant to a register to generate an effective address. There are 2 notation forms

```x86asm
[label + reg]
label[reg]
```

```x86asm
.data
arrayW  WORD  1000h,2000h,3000h
.code
mov esi,0
mov ax,[arrayW + esi]     ;ax = 1000h
add esi,2
mov ax,array[esi]         ;ax = 4000h
```

## JMP and LOOP instructions

### JMP instruction

- JMP is an unconditional jump to a label that is usually within the same procedure.
  - Syntax - `JMP target`
  - Logic - EIP <-- Target

```x86asm
top:
  .
  .
  jmp top
```

### LOOP instruction

- Loop creates a counting loop
  - Syntax - `LOOP target`
  - Logic
    - ECX <-- ECX -1
    - if ECX !=0, jump to target
  - Implementation
    - assembler calculates distance(in bytes) between the offset of the following instruction and offset of target label. It is called relative offset.
    - Relative offset added to EIP.

### LOOP Example

The following loop calculates 1+2+3+4+5

```x86asm
mov eax,0     ;set value of accumulator to 0
mov ecx,5     ;set value of counter to 5

L1:
add eax,ecx   ;add ecx into eax
loop L1       ;goes back to L1 after subtracting 1 from ecx
;adds 5+4+3+2+1
```

### Nested Loop

If you need to create loop within a loop, you must save the outer loop's counter's ECX value.

In the following loop, outer loop executes 100 times, inner loop 20 times

```x86asm
.data
count DWORD ?     ;stores the counter for outer loop
.code
mov ecx,100       ;set the value for the outer loop
L1:
  mov count,ecx   ;store value of the ecx for outer loop in count
  mov ecx,20      ;set the inner loop counter
L2:
  .
  .
  loop L2         ;Loops L2 20 times
mov ecx,count     ;restores the outer loop counter. only runs after L2 has loopedk
loop L1           ;repeat the outer loop
```

### Summing integer array

```x86asm
.data
intArray WORD 100h,200h,300h,400
.code
                            ;edi is the destination register
mov edi,OFFSET intArray     ;stores the pointer to the start of intArray
mov ecx,LENGTHOF intArray   ;stores the no. of elements in intArray in the counter
mov ax,0                    ;the accumulator
L1:
  add ax,[edi]              ;adds the value at the address of edi
  add edi,TYPE intArray     ;incremenst edi by 2 cause WORD
  loop L1                   ;Goes back to L1 and loops until ecx = 0
```

### Copying a string

Copy's string from source to target

```x86asm
.data
source BYTE "This is the source string",0
target BYTE SIZEOF source DUP(0)

.code
mov esi,0               ;set the index register to 0
mov ecx,SIZEOF source   ;sets the counter to the size of source
L1:
mov al,source[esi]      ;get the char from source
mov ecx[esi],al         ;store it in the target
inc esi                 ;go to next character.
                        ;No need to use add esi,TYPE source` as strings are stored in bytes
loop L1

```

# Chapter 5 - Procedure

## Stack operations

### Runtime stack

- Is a stack
  - Last in First Out (LIFO)
- Managed by CPU using 2 registers
  - Stack Segment(**SS**)
  - Stack Pointer(**ESP**)



### PUSH Operation

- 32-bit push operation decrements the `stack pointer` **by 4** and copies a value into the location pointed by the `stack pointer`
- The stack grows downwards. The area below ESP is always available (unless stack has overflowed)

|           | Before |      |      |           | After |      |
| :-------- | :----- | :--- | :--- | :-------- | :---- | :--- |
| Address   | Value  | ESP  |      | Address   | Value | ESP  |
| 0000 1000 | 6      | <--  |      | 0000 1000 | 6     |      |
|           |        |      |      | 0000 0FFC | 9     | <--  |

### POP Operation

- Copies value at `stack[ESP]` into register or variable
- adds *n* to ESP, where n is either 2 or 4
  - value of *n* depends on the attribute of the operand receiving the data

|           | Before |      |      |           | After |      |
| :-------- | :----- | :--- | :--- | :-------- | :---- | :--- |
| Address   | Value  | ESP  |      | Address   | Value | ESP  |
| 0000 1000 | 6      |      |      | 0000 1000 | 6     | <--  |
| 0000 0FFC | 9      | <--  |      |           |       |      |

### Using PUSH and POP

Save and restore registers when they contain important values.

***Push** and **Pop** instructions occur in opposite order*

```x86asm
;push the registers into the stack
push esi
push ecx
push ebx

;display some stuff
mov esi,OFFSET dWordVal
mov ecx,LENGTHOF dWordVal
mov ebx,TYPE dWordVal
call dumpmem

;restore the registers
pop ebx
pop ecx
pop esi
```

### Example - Nested Loops

When creating nested loop, push the outer loop counter to the stack before entering the inner loop

```x86asm
mov ecx,100         ;set the outer loop counter to 100
L1:                 ;begin the outer loop
push ecx            ;store the loop counter
mov ecx,20          ;set the inner loop counter
L2:
.
.

loop L2             ;repeat the inner loop
pop ecx             ;restore the value of the outer loop
```

### Related Instructions

- PUSHFD and POPFD
  - push and pop EFLAGS register
- PUSHAD pushes the 32bit general purpose registers onto the stack

## Defining and using Procedures

### Creating Procedures

- Large problems can be divide to smaller tasks to make them more manageable
- ASM equivalent of functions in other languages

```x86asm
;Creates a procedure called sample
sample PROC
.
.
.
ret
sample ENDP
```

### Documenting Procedues

- A description of all tasks accomplished by the procedure
- `Receives` - A list of input parameters; state their usage and requirements
- `Returns` - A description of values returned by the procedur
- `Requires` - Optional list of requirements called *preconditions* that must be satisfied before procedure is called
- *If Procedure is called without preconditions satisfied, it will probably not produce expected output*

### Example

```x86asm
;-------------------------------------------------------------------------------
SumOf PROC
;Calculates and returns the sum of 3 32 bit integers
;Receives:  EAX, EBX, ECX , the 3 integers to be added. May be signed or unsigned
;Returns:   EAX = sum, and status flags (Carry, Overflow, etc) are changed
;Requires:  Nothing
;-------------------------------------------------------------------------------
  add  eax,ebx
  add eax,ecx
  ret
SumOf ENDP
```

### CALL and RET instructions

- Call instruction calls a procedure
  - pushes offset of next index onto the stack
  - copies address of procedure into the `EIP`(Instruction Pointer)
- The RET instruction returns from a procedure
  - pops top of stack into EIP

### CALL-RET Example

```x86asm
main PROC
  00000020 call MySub
  ;0000 0025 is the offset of the instruction immediately after the call instruction. This is added to the stack
  ; EIP is set to 0000 0040
  00000025 mov eax,ebx
  .
  .
main ENDP

MySub PROC
  00000040 mov eax,edx
  .
  .
  ret
  ;the stack is popped and EIP is now set to 0000 0025
MySub ENDP
```

### Local and Global Labels

local label is only visible to statements inside the same procedure. A global variable is visible everywhere

```x86asm
main PROC
  jmp L2      ;error since L2 is a local label
  L1::        ;Global Label
  exit
main ENDP

sub2 PROC
  L2:         ;local label
  jmp L1      ;ok since L1 is global label
  ret
sub2 PROC
```

### Procedure Parameters

- A good procedure might be usable in many different programs
- Parameters help make procedures flexible because parameter values can change at runtime

```x86asm
;This procedure calculates the sum of an array
;This program references 2 variables - myArray and theSum
ArraySum  PROC
  mov esi,0                 ;array index      (ESI is the index register)
  mov eax,0                 ;set the sum to 0 (EAX is the accumulator)
  mov ecx,LENGTHOF myArray  ;set no of elements

  L1:
  add eax,myArray[esi]      ;add the value of myArray into the accumulator
  add esi,TYPE myArray      ;increments the esi value to point to the next element
  loop L1

  mov theSum, eax           ;stores the sum
  ret
Arraysum ENDP
```

# Conditional Processing

## Boolean and Comparison Instructions

### Status Flags Review

- `Zero` flag is set when the result of an operation equals 0
- `Carry` flag is set when result is too large for the destination operand
- `Sign` flag is set if the destination operand is negative, and clear if destination is negative
- `Overflow` flag is set when an instruction generates invalid sign result

### AND instruction

- Perform a Boolean AND operation between each pair of matching bits in two operands
- Syntax
  - AND destination,source

| X     | Y     | X AND Y |
| :---: | :---: | :-----: |
| 0     | 0     | 0       |
| 0     | 1     | 0       |
| 1     | 0     | 0       |
| 1     | 1     | 1       |

### OR Instruction

- Perform a Boolean OR operation between each pair of matching bits in two operands
- Syntax
  - OR destination,source

| X     | Y     | X OR Y |
| :---: | :---: | :----: |
| 0     | 0     | 0      |
| 0     | 1     | 1      |
| 1     | 0     | 1      |
| 1     | 1     | 1      |

### XOR Instruction

- Perform a Boolean E**x**clusive-OR operation between each pair of matching bits in two operands
- Syntax
  - XOR destination,source

| X     | Y     | X XOR Y |
| :---: | :---: | :-----: |
| 0     | 0     | 0       |
| 0     | 1     | 1       |
| 1     | 0     | 1       |
| 1     | 1     | 0       |

Useful way to toggle(invert) the bits in an operand

### NOT Instruction

- Perform a Boolean NOT operation on a single destination operand
- Syntax
  - NOT destination,source

| X     | NOT X |
| :---: | :---: |
| 0     | 1     |
| 1     | 0     |

### Applications

```x86asm
;convert character in AL to upper case
;use and instruction to clear bit 5
mov al,'a'
AND al,11011111b        ;use AND to clear bit 6
```

```x86asm
;convert binary decimal byte into its equivalent ascii decimal digit
;use or instruction to set bits 4 and 5
mov al,6
or al,00110000b        ;use or to clear bit 6
```

### Test

- Performs a non-destructive AND Operation between each pair of matching bits in two operands
- No Operands are modified, but `Zero` flag is modified

```x86asm
;This program jumps to label if either bit 0 or bit 1 in al is set
test al,00000011b     ;AND al,0000 0011b
jnz ValueFound        ;JNZ will be taught later on(Conditional Jumps) jnz = jump not zero
```

### CMP Instruction

- Compares destination operand to the source operand
  - Non destructive subtraction of source from destionation (destination operand is not changed)
- Syntax: `cmp destionation,source`

#### Destination == Source

**Zero flag** is *set*

```x86asm
mov al,5
cmp al,5          ;zero flag *set*
```

#### Destination < Source

**Carry flag** is *set*

```x86asm
mov al,4
cmp al,5          ;carry flag *set*
```

#### Destination > Source

**Zero and Carry flag** is *clear*

```x86asm
mov al,6
cmp al,5          ;ZF = 0, CF = 0
```

### Comparison with signed integers

#### Destination > Source

```x86asm
mov al,5
cmp al,-2         ;Sign flag == Overflow flag
```

#### Destination < Source

```x86asm
mov al,-1
cmp al,5         ;Sign flag != Overflow flag
```

## Conditional Jumps

J**cond** - A conditional jump instruction branches to a label when specific register or flag condition are met

### Jump Based on Specific Flags

| Memonic | Description             | Flags  |
| :------ | :---------------------- | :----: |
| JZ      | Jump if Zero            | ZF = 1 |
| JNZ     | Jump if Not Zero        | ZF = 0 |
| JC      | Jump if Carry           | CF = 1 |
| JNC     | Jump if Not Carry       | CF = 0 |
| JO      | Jump if Overflow        | OF = 1 |
| JNO     | Jump if Not Overflow    | OF = 0 |
| JS      | Jump if Signed          | SF = 1 |
| JNS     | Jump if Not Signed      | SF = 0 |
| JP      | Jump if Parity(even)    | PF = 1 |
| JNP     | Jump if Not Parity(odd) | PF = 0 |

### Jump based on Equality

| Memonic | Description                           |
| :------ | :------------------------------------ |
| JE      | Jump if Equal (leftOp = rightOp)      |
| JNE     | Jump if Not Equal (leftOp != rightOp) |
| JCXZ    | Jump if CX = 0                        |
| JCXZ    | Jump if ECX = 0                       |

### Jump based on Unsigned Comparisons

| Memonic | Description                               |
| :------ | :---------------------------------------- |
| JA      | Jump if above(if leftOp > rightOp)        |
| JNBE    | Jump if not below or equal(Same as JA)    |
| JAE     | Jump if above or equal(leftOp >= rightOp) |
| JNB     | Jump if not below (Same as JAE)           |
| JB      | Jump if below(leftOp < rightOp)           |
| JNAE    | Jump if not above or equal(Same as JB)    |
| JBE     | Jump if below or equal(leftOp <= rightOp) |
| JNA     | Jump if not above(Same as JBE)            |

### Jump based on Signed comparisons

| Memonic | Description                                 |
| :------ | :------------------------------------------ |
| JG      | Jump if greater(if leftOp > rightOp)        |
| JNLE    | Jump if not less or equal(Same as JA)       |
| JGE     | Jump if greater or equal(leftOp >= rightOp) |
| JNL     | Jump if not less (Same as JAE)              |
| JL      | Jump if less(leftOp < rightOp)              |
| JNGE    | Jump if not greater or equal(Same as JB)    |
| JLE     | Jump if less or equal(leftOp <= rightOp)    |
| JNG     | Jump if not greater(Same as JBE)            |

### Applications

```x86asm
;Jump to label if unsigned EAX is greater than EBX
cmp eax,ebx
ja larger
```

```x86asm
;Jump to label if signed EAX is greater than EBX
cmp eax,ebx
jg greater
```

```x86asm
;Jump to label if unsigned EAX is lesser than or equal to EBX
cmp eax,ebx
jbe L1
```

```x86asm
;Jump to label if signed EAX is lesser than or equal to EBX
cmp eax,ebx
jg greater
```

```x86asm
;Compare unsigned AX and BX, and copy the larger to variable named large
mov large,ax       ;large = ax
cmp ax,bx          ;compare ax,bx
jnb L1             ;jump to L1 if ax is not below bx (ax > bx)
mov large,bx       ;move large = bx if bx is greater than ax
L1:
```

```x86asm
;Compare signed AX and BX, and copy the smaller to variable named small
mov small,ax     ;small = =ax
cmp ax,bx        ;compare ax and bx
jng L1           ;jump to L1 if ax is not greater than bx (ax <= bx)
mov large,bx
L1:
```

### Encrypting a string

```x86asm
;The following loop uses  the XOR instruction to transform 
;every character in a string to a new value 

KEY = 239
BUFMAX = 128

.data
buffer  BYTE  BUFMAX+1 DUP(0)
bufSize DWORD BUFMAX

.code
mov ecx,bufSize           ;loop counter to buffer size
mov esi,0                 ;set index register to 0

L1:
  xor buffer[esi],KEY     ;translate a byte of data with key
  inc esi                 ;esi now points to next byte
  loop L1
```

## Conditional Loop instructions

### LOOPZ and LOOPE

- Synax
  - LOOPE destination
  - LOOPZ destination
- LOOPZ(loop if *zero*)   instruction works just like the loop instruction except it has 1 more condition. Zero flag must be set
- LOOPE(loop if *equal*)  instruction is equivalent to LOOPZ (cmp sets Zero flag when both values are equal)
- Logic:
  - ECX <-- ECX - 1
  - If ECX > 0 and ZF = 1, jump to destination
- Useful for scanning an array for the first element that does not match a given value

### LOOPNZ and LOOPNE

- Syntax
  - LOOPNZ destination
  - LOOPNE destination
- Logic:
  - ECX <-- ECX - 1
  - If ECX > 0 and ZF = 0, jump to destination
- Useful when scanning an array for the first element that matches a given value

## Conditional Control flow Drectives

Creating **IF** statements

### Runtime Expressions

`.IF`, `.ELSE`, `.ELSEIF`, and `.ENDIF` can be used to evaluate runtime expressions and create block-structured IF statements

```x86asm
.IF eax > ebx
  mov edx,1
.ELSE
  move edx,2
.ENDIF
```

```x86asm
.IF eax > ebx && eax > ecx
  mov edx,1
.ELSE
  move edx,2
.ENDIF
```

MASM generates hidden code for you, consisting of code labels, CMP and conditional jumps

### Relational and Logical Operators

| Operator             | Description                                       |
| :------------------- | :------------------------------------------------ |
| expr1 == expr2       | true when 1 equal 2                               |
| expr1 != expr2       | true when 1 not equal 2                           |
| expr1 > or < expr2   | true when 1 greater / lesser than than 2          |
| expr1 >= or <= expr2 | true when 1 greater / lesser than than or equal 2 |
| !expr1               | true when expr1 equals false                      |
| expr1 && expr2       | logical AND on 1 and 2                            |
| expr1 \|\| expr2     | logical OR between 1 and 2                        |
| expr1 & expr2        | bitwise AND between 1 and 2                       |
| CARRY?               | true if carry flag set                            |
| OVERFLOW?            | true if overflow flag set                         |
| PARITY?              | true if parity flag set                           |
| SIGN?                | true if sign flag set                             |
| ZERO?                | true if zero flag set                             |

### MASM generated code

- when *unsigned* values are compared, MASM automatically generates unsigned jump (.IF register > val(where val is unsigned (WORD))
- when *signed* values are compared, MASM automatically generates a signed jump (.IF register > val(where val is signed (SWORD))

### .REPEAT directive

Execute the loop body before testing the loop condition associated with the `.UNTIL` directive

```x86asm
;display integers from 1-10:
mov eax,0
.REPEAT
  inc eax
  call WriteDec
  call Crlf
.UNTIL eax == 10
```

### .WHILE directive

Tests the loop condition before executing the loop body. The `ENDW` directive marks the end of the loop

```x86asm
;display integers from 1-10:
mov eax,0
.WHILE eax < 10
  inc eax
  call WriteDec
  call Crlf
.ENDW
```
