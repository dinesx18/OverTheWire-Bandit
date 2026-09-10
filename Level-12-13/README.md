# 🏴 Bandit Level 12 → Level 13
<img width="1592" height="527" alt="image" src="https://github.com/user-attachments/assets/0ae2d45d-7787-4ce3-9eca-8c3057bd463e" />



---

## 🎯 Goal

The password for the next level is stored in:

```text
data.txt
```

However, `data.txt` is **not the original file**.

It is a **hexdump** of a file that has been compressed multiple times using different compression methods.

The goal is to:

1. Reverse the hexdump.
2. Identify the file type.
3. Decompress the file.
4. Repeat the process until we reach normal text.
5. Read the password for **Bandit Level 13**.

---

# 🔐 Step 1 — Connect to Bandit Level 12

First, connect to the Bandit Level 12 account.

```bash
ssh bandit12@bandit.labs.overthewire.org -p 2220
```

### Command Breakdown

```text
ssh
```

Used to connect to a remote computer securely.

```text
bandit12
```

The username for Level 12.

```text
@
```

Separates the username from the hostname.

```text
bandit.labs.overthewire.org
```

The OverTheWire Bandit server.

```text
-p 2220
```

Connects using port `2220`.

---

# 🔑 Step 2 — Enter the Password

The terminal will ask:

```text
bandit12@bandit.labs.overthewire.org's password:
```

Enter the password obtained from **Bandit Level 11 → Level 12**.

> ⚠️ The actual password is not included in this GitHub writeup.

---

# 📍 Step 3 — Check the Current Directory

Run:

```bash
pwd
```

`pwd` means:

```text
Print Working Directory
```

It shows where you are currently located.

---

# 📋 Step 4 — List the Files

Run:

```bash
ls
```

You should see:

```text
data.txt
```

---

# 📄 Step 5 — Look at `data.txt`

Run:

```bash
cat data.txt
```

The output will contain many hexadecimal characters.

For example:

```text
00000000: 1f8b 0808 ...
00000010: ...
```

This tells us that `data.txt` is a **hexdump**.

We cannot simply use:

```bash
cat data.txt
```

to get the password.

We first need to convert the hexdump back into the original binary file.

---

# 📁 Step 6 — Create a Temporary Working Directory

We should not modify the original `data.txt`.

Create a directory inside `/tmp`:

```bash
mkdir /tmp/bandit12
```

### What does `mkdir` do?

`mkdir` means:

```text
Make Directory
```

It creates a new directory.

---

# 📋 Step 7 — Copy `data.txt`

Copy the file into our temporary directory:

```bash
cp data.txt /tmp/bandit12/
```

### What does `cp` do?

`cp` means:

```text
copy
```

It creates a copy of `data.txt`.

---

# 📂 Step 8 — Enter the Temporary Directory

Run:

```bash
cd /tmp/bandit12
```

### What does `cd` do?

`cd` means:

```text
Change Directory
```

It moves us into another directory.

---

# 🔎 Step 9 — Check the File

Run:

```bash
ls
```

You should see:

```text
data.txt
```

---

# 🔄 Step 10 — Reverse the Hexdump

Now we need to convert the hexdump back into its original binary form.

Use:

```bash
xxd -r data.txt data
```

### What does `xxd` do?

`xxd` is a tool used to create and reverse hexadecimal representations of files.

The important option here is:

```text
-r
```

`-r` means:

```text
reverse
```

So:

```bash
xxd -r data.txt data
```

means:

```text
Take the hexdump in data.txt
        ↓
Reverse it
        ↓
Create the original file as data
```

---

# 🔎 Step 11 — Identify the File Type

Now run:

```bash
file data
```

This is one of the most important commands in this level.

`file` examines the contents of a file and tells us what type of file it is.

The result may say something like:

```text
data: gzip compressed data
```

or:

```text
data: bzip2 compressed data
```

or:

```text
data: POSIX tar archive
```

We need to use the appropriate command based on what `file` tells us.

---

# 🧠 Why Do We Use `file`?

We don't want to guess the compression type.

Instead:

```bash
file data
```

tells us what we are dealing with.

The process is:

```text
data
 ↓
file
 ↓
Identify compression
 ↓
Use correct decompression command
```

---

# 🗜️ Step 12 — If the File Is Gzip

If the output from:

```bash
file data
```

says:

```text
gzip compressed data
```

rename the file:

```bash
mv data data.gz
```

Then decompress it:

```bash
gzip -d data.gz
```

### Command Breakdown

```text
mv
```

Moves or renames a file.

```text
data
```

Current filename.

```text
data.gz
```

New filename.

The `.gz` extension tells us that the file is gzip compressed.

---

# 🗜️ Step 13 — If the File Is Bzip2

If:

```bash
file data
```

says:

```text
bzip2 compressed data
```

rename the file:

```bash
mv data data.bz2
```

Then decompress:

```bash
bzip2 -d data.bz2
```

### Command Breakdown

```text
bzip2
```

A compression/decompression program.

```text
-d
```

Means:

```text
decompress
```

---

# 📦 Step 14 — If the File Is a Tar Archive

If:

```bash
file data
```

says:

```text
POSIX tar archive
```

rename it:

```bash
mv data data.tar
```

Then extract it:

```bash
tar -xf data.tar
```

### Command Breakdown

```text
tar
```

Used to create and extract archive files.

```text
-x
```

Extract files.

```text
-f
```

Specifies the archive file.

Therefore:

```bash
tar -xf data.tar
```

means:

```text
Extract the contents of data.tar
```

---

# 🔁 Step 15 — Repeat the Process

This is the most important part of Level 12.

The file is compressed **multiple times**.

After every decompression, run:

```bash
file data
```

or, if the extracted filename changes:

```bash
ls
file <filename>
```

Then identify the next compression format.

The general process is:

```text
Hexdump
   ↓
xxd -r
   ↓
Compressed file
   ↓
file
   ↓
Identify type
   ↓
Decompress
   ↓
file
   ↓
Identify next type
   ↓
Decompress
   ↓
Repeat
   ↓
ASCII text
   ↓
Password
```

---

# 🧩 Common Commands Used in This Level

## Gzip

```bash
mv data data.gz
gzip -d data.gz
```

---

## Bzip2

```bash
mv data data.bz2
bzip2 -d data.bz2
```

---

## Tar

```bash
mv data data.tar
tar -xf data.tar
```

---

# 🔎 Step 16 — Keep Checking With `file`

After every decompression, check the result.

For example:

```bash
file data
```

If it says gzip:

```bash
mv data data.gz
gzip -d data.gz
```

Then check again:

```bash
file data
```

If it says bzip2:

```bash
mv data data.bz2
bzip2 -d data.bz2
```

Then check again.

Continue until the output finally says something like:

```text
ASCII text
```

---

# 📖 Step 17 — Read the Final File

When the file is finally identified as normal text, use:

```bash
cat data
```

If the extracted file has another filename, use:

```bash
ls
```

to find the filename and then:

```bash
cat <filename>
```

The final text contains the password for **Bandit Level 13**.

> 🔐 Do not publish the actual password in your GitHub repository.

---

# 🧠 What I Learned

### 1. Hexdump

A hexdump represents the binary contents of a file using hexadecimal numbers.

The command:

```bash
xxd -r
```

can reverse a hexdump back into binary data.

---

### 2. `file`

The `file` command identifies the type of a file based on its contents.

Example:

```bash
file data
```

It can tell us whether the file is:

```text
gzip
bzip2
tar
ASCII text
```

---

### 3. Gzip

Gzip is a compression format.

Decompress using:

```bash
gzip -d filename.gz
```

---

### 4. Bzip2

Bzip2 is another compression format.

Decompress using:

```bash
bzip2 -d filename.bz2
```

---

### 5. Tar

Tar is commonly used to create archives containing multiple files.

Extract using:

```bash
tar -xf filename.tar
```

---

### 6. Temporary Directories

We used:

```text
/tmp
```

because it is a suitable location for temporary files while solving the challenge.

---

# 🧩 Why Each Command Was Used

| Command    | Purpose                      |
| ---------- | ---------------------------- |
| `ssh`      | Connect to the Bandit server |
| `pwd`      | Show current directory       |
| `ls`       | List files                   |
| `cat`      | Display file contents        |
| `mkdir`    | Create a directory           |
| `cp`       | Copy the file                |
| `cd`       | Change directory             |
| `xxd -r`   | Reverse the hexdump          |
| `file`     | Identify the file type       |
| `mv`       | Rename a file                |
| `gzip -d`  | Decompress gzip              |
| `bzip2 -d` | Decompress bzip2             |
| `tar -xf`  | Extract a tar archive        |

---

# 🎓 Key Takeaway

The main lesson from **Bandit Level 12 → Level 13** is learning how to identify and repeatedly decompress files.

The important commands are:

```bash
xxd -r
file
gzip -d
bzip2 -d
tar -xf
```

The general strategy is:

```text
Identify → Decompress → Identify → Decompress → Repeat
```

until the final file becomes readable text.

---

# 🔄 Complete Command Flow

```bash
ssh bandit12@bandit.labs.overthewire.org -p 2220
```

⬇️

```bash
pwd
```

⬇️

```bash
ls
```

⬇️

```bash
cat data.txt
```

⬇️

Create a temporary directory:

```bash
mkdir /tmp/bandit12
```

⬇️

Copy the file:

```bash
cp data.txt /tmp/bandit12/
```

⬇️

Enter the directory:

```bash
cd /tmp/bandit12
```

⬇️

Reverse the hexdump:

```bash
xxd -r data.txt data
```

⬇️

Identify the file:

```bash
file data
```

⬇️

Decompress according to the identified type:

```bash
gzip -d data.gz
```

or:

```bash
bzip2 -d data.bz2
```

or:

```bash
tar -xf data.tar
```

⬇️

Check again:

```bash
file data
```

⬇️

Repeat the process.

⬇️

Finally:

```bash
cat data
```

⬇️

```text
Password for bandit13 🔓
```

---

# 🏁 Final Solution

The key technique for this level is:

```bash
xxd -r data.txt data
```

Then repeatedly:

```bash
file data
```

and use the correct decompression command:

```bash
gzip -d
```

```bash
bzip2 -d
```

```bash
tar -xf
```

until the final file contains readable text.

---
# 🖥️ Terminal Screenshot



# 📚 Commands Practiced

```bash
ssh
pwd
ls
cat
mkdir
cp
cd
xxd
file
mv
gzip
bzip2
tar
```

---

# ⭐ Level Completed

```text
Bandit Level 12
       ↓
   data.txt
       ↓
    Hexdump
       ↓
    xxd -r
       ↓
Compressed File
       ↓
      file
       ↓
 Identify Format
       ↓
    Decompress
       ↓
      file
       ↓
    Repeat 🔄
       ↓
   ASCII Text
       ↓
Password for Bandit 13 🔓
```

---

# ➡️ Next Level

After obtaining the password, connect to Bandit Level 13:

```bash
ssh bandit13@bandit.labs.overthewire.org -p 2220
```

Enter the password obtained from this level.
