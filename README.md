# Daftar isi
- <a href="#john-the-ripper">John The Ripper</a>
- <a href="#hydra">Hydra</a>
- <a href="#nmap">Nmap</a>
- <a href="#gobuster">Gobuster</a>
- <a href="#sqlmap">Sqlmap</a>
- <a href="#reverse">Reverse</a>
- <a href="#reverse-shell">Reverse Shell</a>

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

#### SQL DUMP
```
sqlmap -r [FILE LOCATION] --dump
```
Example :
```
sqlmap -r Belajar/learn/sqlmap/latihan.txt --dbs
```

<br>

# Reverse

#### CLI Tools

- strings
- ltrace
- r2 -d
- gdb

#### GUI Tools

- Ghidra (Linux)
- IDA (Windows)


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
