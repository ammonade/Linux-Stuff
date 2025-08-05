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
```

### Hidden Files
```bash
find . -name ".*"                # Find all hidden files
find . -type f -size 1033c       # Find file of exact size (e.g., 1033 bytes)
find . -type f -exec file {} \; | grep "ASCII"   # Find readable text files
```

```bash
find / -type f -size 1033c -user bandit7 -group bandit6 2>/dev/null     # Finds files owned by user bandit7 and group bandit6 (/ is to start at the root)
2>/dev/null              # Sends any error messages (2nd stream for error) to dev/null (void)
sort file.txt            # Sorts the file in alphabetical order
sort file.txt | uniq -u  # Sorts the file in alphabetical order and then only displays non duplicate lines
```

## 📝 Writing into files 
```bash
/tmp/       # Temporary directory which is created on all linux servers and systems, files inside get deleted on reboot
touch       # Creates a file in the current or specified directory

touch /tmp/myfile.txt                # Creates a file myfile.txt in the tmp directory
echo "hello world" > myfile.txt      # Echo prints out text, use > to direct the printed text (like into myfile.txt)
base64 -d file.txt > /tmp/myfile.txt # Direct the decoded base64 file into myfile.txt in tmp for further analysis or editing
```

## 📖 Reading & Searching Files
```bash
cat file.txt                    # Read a file
cat ./-filename                 # Read a file with a dash prefix
strings filename                # Extract readable strings from a binary
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
### PIPING 🚬🚬
```bash
|                     # DA PIPE OPERATOR takes the output of one command and uses it as input for the next (very importanto)
command1 | command2   # Output of command1 goes into command2 as input
eg sort data.txt | uniq -u # Prints unique non-duplicate lines from data.txt
cat file.txt | sort | uniq -c | sort -n  # Read file.txt -> sort read file in alphabetical order -> removes any duplicate lines
                                         # but also shows the number of times each duplicate line occurs eg 2 Apple, 3 Ball etc.
                                         # -> sorts the counted lines numerically i.e the number of times they appeared here (least frequency would be at the top)
```

## 🔐 SSH Access (OverTheWire)
```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
# Default password: bandit0
```
## 🧮 Decoding & Decompression
### Base64

```bash
base64 -d file.txt                      # Decode base64 file
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
sort data.txt | uniq -u                # Find the only line that appears once
grep "millionth" data.txt              # Find line containing the word 'millionth'
strings data.txt | grep '='            # Find strings with '=' characters
cat file | base64 -d | tar -x          # Decode base64 & extract .tar file
```


