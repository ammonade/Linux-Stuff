# 🐧 Linux CTF + Hacking Cheat Sheet

> A personal reference of essential Linux commands, OverTheWire solutions, and hacker tools.  
> Built with blood, sweat, and `grep`.

---

## 📁 Basic File & Directory Navigation

```bash
ls -la           # List all files (including hidden) in long format
cd dir/          # Change to a directory
pwd              # Show current directory path
mkdir name       # Create a new directory
touch file.txt   # Create an empty file
rm file.txt      # Delete a file
mv file1 file2   # Move or rename a file
cp file1 file2   # Copy a file
```
## 🔍 File Discovery & Analysis
```bash
file filename                    # Show file type (text, binary, etc.)
du -h                            # Disk usage (human-readable)
du -b file.txt                   # Exact file size in bytes
find . -name ".*"                # Find all hidden files
find . -type f -size 1033c       # Find file of exact size (e.g., 1033 bytes)
find . -type f -exec file {} \; | grep "ASCII"   # Find readable text files
```


## 📖 Reading & Searching Files
```bash
cat file.txt                     # Read a file
cat ./-filename                  # Read a file with a dash prefix
strings filename                 # Extract readable strings from a binary
cat file.txt | grep "keyword"   # Search for a keyword in a file
grep "keyword" file.txt         # Search without using pipe
strings file | grep "KEYWORD"   # Search strings from a binary for keywords
```

## 🚦 Output Redirection & Noise Control
```bash
> file.txt            # Redirect stdout (overwrite file)
2> error.log          # Redirect stderr
&> out.log            # Redirect both stdout and stderr
2>/dev/null           # Suppress error messages (e.g., permission denied)
command 2>/dev/null   # Run command and silence errors
```

## 🔐 SSH Access (OverTheWire)
```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
# Default password: bandit0
```
## 🧮 Decoding & Decompression
### Base64

```bash
base64 -d file.txt                       # Decode base64 file
echo "base64_string==" | base64 -d      # Decode base64 from string
```
### Archives
```bash
tar -xf file.tar                         # Extract .tar archive
gzip -d file.gz                          # Decompress .gz file
bzip2 -d file.bz2                        # Decompress .bz2 file
```

## ⚔️ CTF / Bandit-Specific Tricks
```bash
sort data.txt | uniq -u                 # Find the only line that appears once
grep "millionth" data.txt              # Find line containing the word 'millionth'
strings data.txt | grep '='            # Find strings with '=' characters
cat file | base64 -d | tar -x          # Decode base64 & extract .tar file
```
