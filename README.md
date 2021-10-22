# Daftar isi
- <a href="#john-the-ripper">John The Ripper</a>
- <a href="#hydra">Hydra</a>
- <a href="#nmap">Nmap</a>
- <a href="#gobuster">Gobuster</a>
- <a href="#sqlmap">Sqlmap</a>
- <a href="#reverse-shell">Reverse Shell</a>
- <a href="#iptables">IP Tables</a>
- <a href="#forensic">Forensic</a>
- <a href="#reverse-engineering">Reverse</a>
- <a href="#assembly">Assembly</a>
- <a href="#c-programming">C Cheatsheet</a>


<br>

# John The Ripper

#### Bruteforce File
```
john --wordlist=[WORDLIST] [FILE]
```
#### Show Format List
```
john --list=formats
```
#### Bruteforce Hash
```
john --formats=[HASH] [FILE]
```
#### PDF2John Online Tool
```
https://www.onlinehashcrack.com/tools-pdf-hash-extractor.php
```
#### PDF2John Command
```
/usr/share/john/pdf2john.pl [FILE] > [HASH FILE]
```
#### ZIP2John Command
```
zip2john [FILE]
```

<br>

# Hydra

#### Bruteforce Password
```
hydra -V -l [USERNAME] -P [WORDLIST] [IP VICTIM] [PROTOCOL]
```
#### Bruteforce Via HTTP
```
hydra -V -l [USERNAME] -P [WORDLIST] [IP VICTIM] http-[REQUEST METHOD]-form "[PATH]:[REQUEST BODY]:[INCORRECT ALERT]"
```
Example :
```
hydra -V -l admin -P /usr/share/wordlists/rockyou.txt 10.10.10.10 http-get-form "/DVWA/vulnerabilities/brute:username=admin&password=^PASS^:Username and/or password incorrect."
```
<br>

# Nmap

#### Aggresive & Verbose Scan
```
nmap -v -A [IP]  
```

<br>

# Gobuster

#### Directory Enumeration
```
gobuster dir -u [URL] -w [WORDLIST] 
```

<br>

# Sqlmap

#### SQL Injection from File
```
sqlmap -r [FILE LOCATION] --dbs
```

#### SQL Dump
```
sqlmap -r [FILE LOCATION] --dump
```
Example :
```
sqlmap -r Belajar/learn/sqlmap/latihan.txt --dbs
```

<br>

# Reverse Shell

#### Python Spawning Bash
```
python -c 'import pty; pty.spawn("/bin/bash")'
```
#### Export Shell
```
export SHELL=bash
export TERM=xterm-256color
```

<br>

# Iptables

#### Show Iptables with Numbers
```
iptables -L --line-numbers
```
#### Remove All Rules
```
iptables -F
```
#### Delete Spesific Rule
```
iptables -D [CHAIN] [NUMBER]
```
Example :
```
iptables -D INPUT 3
```
#### Save Permanently Iptables
```
sudo /sbin/iptables-save
```
#### Filter Packet from Spesific Port
```
iptables -A [CHAIN] -p [PROTOCOL] --dport [PORT] -j [ACCEPT/DROP]
```
Example :
```
iptables -A INPUT -p tcp --dport 22 -j DROP
```

<br>

# Forensic

#### Tools
| Name      | Extensions       | Command                                          |
|-----------|------------------|--------------------------------------------------|
| Zsteg     | PNG, BMP         | zsteg [FILE]                                     |
| Steghide  | JPG/JPEG, AV, AU | steghide info [FILE] ; steghide extract -sF [FILE] |
| Stegsolve | JPG, PNG, BMP    | ./stegsolve.jar                                  |
| Binwalk   | JPG, PNG, BMP    | binwalk -e [FILE]                                |
| Jsteg     | JPG              | jsteg reveal [IMAGE JPG] [FILE OUTPUT]           |
| Foremost     | *              | foremost           |


<br>

# Reverse Engineering

#### CLI Tools

- strings
- ltrace
- r2 -d
- gdb

#### GUI Tools

- Ghidra (Linux)
- IDA (Windows)

<br>

# Assembly

#### Register
| Name | Notes                                                                                                           |    Type   | 64-bit  long | 32-bit int | 16-bit short | 8-bit char |
|:----:|-----------------------------------------------------------------------------------------------------------------|:---------:|:------------:|:----------:|:------------:|:----------:|
| rax  | Values are returned from functions in this register.                                                            | scratch   | rax          | eax        | ax           | ah and al  |
| rcx  | Typical register.  Some instructions also use it as a counter.                                                  | scratch   | rcx          | ecx        | cx           | ch and cl  |
| rdx  | Scratch register.                                                                                               | scratch   | rdx          | edx        | dx           | dh and dl  |
| rbx  | Preserved register: don't use it without saving it!                                                             | preserved | rbx          | ebx        | bx           | bh and bl  |
| rsp  | The stack pointer. Point to the top of the stack                                                                | preserved | rsp          | esp        | sp           | spl        |
| rsi  | Scratch register used to pass function argument #2 in 64-bit Linux.    In 64-bit Windows, a preserved register. | scratch   | rsi          | esi        | si           | sil        |
| rdi  | Scratch register and function argument #1 in 64-bit Linux.   In 64-bit Windows, a preserved register.           | scratch   | rdi          | edi        | di           | dil        |

#### Memory Access
| C/C++ datatype 	| Bits 	| Bytes 	| Register 	| Access memory 	| Allocate memory 	|
|----------------	|------	|-------	|----------	|---------------	|-----------------	|
| char           	| 8    	| 1     	| al       	| BYTE [ptr]    	| db              	|
| short          	| 16   	| 2     	| ax       	| WORD [ptr]    	| dw              	|
| int            	| 32   	| 4     	| eax      	| DWORD [ptr]   	| dd              	|
| long           	| 63   	| 8     	| rax      	| QWORD [ptr]   	| dq              	|

#### Instructions (basically identical to 32-bit x86)
| Mnemonic     	| Purpose                                                                                                                                                                            	| Examples                                                                                                          	|
|--------------	|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|-------------------------------------------------------------------------------------------------------------------	|
| mov dest,src 	| Move data between registers, load immediate data into registers, move data between registers and memory.                                                                           	| mov rax 4,; Load constant into rax mov rdx,rax ; Copy rax into rdx mov rdx,[123] ; Copy rdx to memory address 123 	|
| push src     	| Insert a value onto the stack.Useful for passing arguments, saving registers, etc.                                                                                                 	| push rbp                                                                                                          	|
| pop dest     	| Remove topmost from the stack. Equivalent to "mov dest, [rsp]; add 8,rsp"                                                                                                          	| pop rbp                                                                                                           	|
| cmp a,b      	| Compare two values. Sets flags that are used by the conditional jumps (below).                                                                                                     	| cmp rax,10                                                                                                        	|
| jmp label    	| Goto the instruction label. Skips anything else in the way                                                                                                                         	| jmp post_mem mov [0],rax ; Write to NULL! post_mem: ; OK here...                                                  	|
| add dest,src 	| dest=dest+src                                                                                                                                                                      	| add rax,rdx ;   Add rbx to rax                                                                                    	|
| jl  label    	| Goto label if previous comparison came out as less-than. OPther Conditionals avaible are:  jle (<=), je (==),   jge (>=), jg (>),   jne(!=), jb (<),  jbe (<=), ja (>),  jae (>=). 	| jl loop_start; Jump if rax<10                                                        |

<br>

# C Programming

#### Decompile
```c
gcc -g [file] -o [output]
```

#### Placeholder
|Placeholder   |Describe   |
|---|---|
|%d   |Integer   |
|%c   |Char   |
|%s   |String   |
|%O   |Octal   |
|%p   |An adress (pointer)   |
|%x   |Hexdecimal   |
|%f   |Floats   |
|%x   |Hexdecimal   |


####  Standard Library String Functions
|Library Function   |Describe   |
|---|---|
|strlen   |Finds length of a string   |
|strlwr   |Converts a string to lowercase   |
|strupr   |Converts a string to uppercase   |
|strcat   |Appends one string at the end of another   |
|strncat   |Appends first n characters of a string at the end of another  |
|strcpy   |Copies a string into another   |
|strncpy   |Copies first n characters of one string into another   |
|strcmp   |Compares two strings   |
|strncmp   |Compares first n characters of two strings   |
|strcmpi   |Compares two strings without regard to case ("i" denotesthat this function ignores case)   |
|stricmp   |Compares two strings without regard to case (identical to strcmpi)   |
|strnicmp   |Compares first n characters of two strings without regard to case   |
|strdup   |Duplicates a string   |
|strchr   |Finds first occurrence ofa given character in a string   |
|strrchr   |Finds last occurrence ofa given character in a string   |
|strstr   |Finds first occurrence of a given string in another string   |
|strset   |Sets all characters ofstring to a given character   |
|strnset   |Sets first n characters ofa string to a given character   |
|strrev   |Reverses string   |


#### List of Memory Bugs
| Bug | Description |
| --- | --- |
| Buffer_Overflow | Writing past the bounds of a buffer.  For example, writing to a buffer without an null byte (\x00) appended at the end, therefore the program doesn't know when to stop writing user input to memory. |
| Dangling_Pointers | When a pointer is pointing to an area of memeory that has already been freed.  Also known as, [Use-After-Free](http://phrack.org/issues/57/9.html). |
| Off-By-One_Error | Found in loops that append data to a buffer.  Not checking the last iteration of the loop can overwrite the least signifcant byte on the function's base pointer. |
| Race_Condition | When threads are in use.  If two or more threads can access shared data and try to change it at the same time.  |
| Format_String_Attack | If a function like printf() is used to print input from a user and a format string is not specified. |
| Integer_Overflow | Integers have a maximum value in memory.  A signed int can only go as high as 2,147,483,647 for example.  Math that goes beyond that limit can overflow the integer, resuting in unexpected behavior. |
| Weak_Encryption | Using weak Pseudo-random seeds, for example using time() to provide a cryptographical seed for encryption or rand() function.. |


#### Programming Concepts
| Subject | Description |
| --- | --- |
| Arrays | Arrays and buffers are the same thing.  They point to [adjacent](https://www.merriam-webster.com/dictionary/adjacent) data streams located in memory and end with a NULL byte. (\x00). |
| Pointers | Pointers have [types](https://www.learnjavaonline.org/en/Variables_and_Types), just like variables.  Pointers are used to store a location of data in memory. |
| Strings | Strings are pointers to character arrays.  Strings point to the beginning of an array/buffer in memory to be read by a function like scanf(). |
| Typecasting | C/C++ is a Strongly Typed Language.  You need to use Typecasting to change the type of a variable or pointer.  Despite how the type was originally defined. |
| Vectors | Vectors are similar to arrays expect that they are used to store Object References instead of values with primative data types. |
| File Descriptors | A number that is used to refernece an open file. |
| Streams | The interface we use for reading and writing data to files, sockets, stdout, etc. |
| Structs (C)  | Structs in C are variables that contain multiple other variables. |
| Classes | Class is short for _Classify._ A class is a blueprint for creating objects during runtime. Objects are dynamic and only spawn during runtime. Classes and Object Oriented Programming _(OOP)_ were added in C++. |
|Structs(C++) | Structs in C++ are the same as Classes except they are by default set to Public. |


#### Primitive Data Types
| Subject | Description | Byte Size |
| --- | --- | --- |
| Signed_Int | Stores a whole number. Numbers in C are defaultly signed. Meaning, they can be either positive or negative numbers. 32-bit signed integers max out at 2,147,483,647. | 4 |
| Unsigned_Int | Stores a whole number. Numbers that are unsigned can only be positive.  This means there is no [Twos Compliment](https://www.youtube.com/watch?v=lKTsv6iVxV4) and the least significant bit is not reserved. 32-bit unsigned integers max out at 4,294,967,295. | 4 |
|Long | Store a whole number.  A long is double the memory size of an int, 8-bytes in 32-bit machines.  Used when an Int isn't big enough to store a value. | 8 |
| Short | Store a whole number.  A short is half the size of an Int. 2-Bytes in 32-bit machines or simply 16-Bits in size. | 2 |
| Float | Stores numbers with decimal points.  4-Bytes in size on 32-Bit machines.  Used for values with 6 to 7 decimals. | 4 |
| Double | Stores numbers with decimal points. 8-Bytes in size on 32-Bit machines.  Used for values with up to 15 decimals. | 8 |
| Char | 2 Bytes in size.  Chars are used to contain letters such as ASCII values. Strings are considered char arrays. | 2 |
| Boolean | Either a True or False.  1-Bit in size. | 1-bit |


#### Endianness
| Subject | Description |
| --- | --- |
| Big Endian| Bytes in there normal order. _"Most significant byte first"_  0x12345678 = \x12\x34\x56\x78 |
| Little Endian | Bytes in there reverse order. _"Least significant byte first"_  0x12345678 = \x78\x56\x34\x12 |

<br>
