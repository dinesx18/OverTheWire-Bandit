# 🏴 Bandit Level 12 → Level 13

<img width="1600" height="500" alt="Bandit Level 12 to 13" src="YOUR_SCREENSHOT_LINK_HERE" />

---

## 🎯 Goal

The password for the next level is stored in the file:

```text
data.txt
```

The file `data.txt` is a **hexdump of a file that has been repeatedly compressed**.

For this level, we need to:

1. Create a temporary directory.
2. Copy `data.txt` into the temporary directory.
3. Reverse the hexdump using `xxd`.
4. Identify the file type using `file`.
5. Decompress or extract the file.
6. Check the file type again.
7. Repeat the process until we reach normal ASCII text.
8. Read the password for **Bandit Level 13**.

---

## 🔐 Step 1 — Connect to Bandit Level 12

First, connect to the Bandit Level 12 account using SSH.

```bash
ssh bandit12@bandit.labs.overthewire.org -p 2220
```

### Command Breakdown

```text
ssh
```

Used to securely connect to a remote computer.

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

The hostname of the OverTheWire Bandit server.

```text
-p 2220
```

Specifies SSH port `2220`.

---

## 🔑 Step 2 — Enter the Password

After running the SSH command, the terminal asks for the password.

```text
bandit12@bandit.labs.overthewire.org's password:
```

Enter the password obtained from:

```text
Bandit Level 11 → Level 12
```

> ⚠️ The password is intentionally not included in this GitHub writeup.

If the password is correct, you will successfully log in as:

```text
bandit12
```

---

## 📍 Step 3 — Check the Current Directory

Run:

```bash
pwd
```

### What does `pwd` do?

`pwd` means:

```text
Print Working Directory
```

It shows the directory where you are currently working.

You should see something similar to:

```text
/home/bandit12
```

---

## 📋 Step 4 — List the Files

Run:

```bash
ls
```

You should see:

```text
data.txt
```

---

## 📄 Step 5 — Check the File Type

Run:

```bash
file data.txt
```

You should see something similar to:

```text
data.txt: ASCII text
```

Although the file is detected as ASCII text, its contents are actually a **hexdump**.

---

## 📁 Step 6 — Create a Temporary Directory

The level recommends creating a temporary directory because we will be creating and modifying several files.

Run:

```bash
mktemp -d
```

Example output:

```text
/tmp/tmp.abc123
```

> ⚠️ Your temporary directory name will be different.

### What does `mktemp -d` do?

```text
mktemp
```

Creates a temporary file or directory.

```text
-d
```

Tells `mktemp` to create a directory.

Therefore:

```bash
mktemp -d
```

creates a temporary directory with a random name.

---

## 📋 Step 7 — Copy `data.txt`

Suppose your temporary directory is:

```text
/tmp/tmp.abc123
```

Copy `data.txt` into it:

```bash
cp data.txt /tmp/tmp.abc123/
```

> ⚠️ Replace `/tmp/tmp.abc123/` with the actual directory name you received from `mktemp -d`.

### What does `cp` do?

```text
cp
```

means **copy**.

This command:

```bash
cp data.txt /tmp/tmp.abc123/
```

copies `data.txt` into the temporary directory.

---

## 📂 Step 8 — Enter the Temporary Directory

Run:

```bash
cd /tmp/tmp.abc123
```

Replace the directory name with your actual temporary directory.

Then run:

```bash
ls
```

You should see:

```text
data.txt
```

---

## 🔄 Step 9 — Reverse the Hexdump

Now we need to convert the hexdump back into the original binary file.

Run:

```bash
xxd -r data.txt data
```

### What does `xxd` do?

`xxd` is used to create hexadecimal dumps and to convert hexadecimal data back into binary.

The option:

```text
-r
```

means:

```text
reverse
```

Therefore:

```bash
xxd -r data.txt data
```

takes the hexdump from:

```text
data.txt
```

and creates the original binary file:

```text
data
```

---

## 🔍 Step 10 — Identify the File

Run:

```bash
file data
```

The output should identify the first compression format.

It should look similar to:

```text
data: gzip compressed data
```

This tells us that the file is compressed using:

```text
gzip
```

---

## 🗜️ Step 11 — Rename the File

Rename the file:

```bash
mv data data.gz
```

### What does `mv` do?

```text
mv
```

means **move**.

It can also be used to rename files.

Here:

```bash
mv data data.gz
```

renames:

```text
data
```

to:

```text
data.gz
```

---

## 📦 Step 12 — Decompress the Gzip File

Run:

```bash
gzip -d data.gz
```

### What does `gzip -d` do?

```text
gzip
```

works with gzip-compressed files.

```text
-d
```

means:

```text
decompress
```

So:

```bash
gzip -d data.gz
```

decompresses the file and produces:

```text
data
```

---

## 🔍 Step 13 — Check the File Again

Run:

```bash
file data
```

Now the file should be identified as:

```text
data: bzip2 compressed data
```

The next compression format is:

```text
bzip2
```

---

## 🗜️ Step 14 — Rename the Bzip2 File

Run:

```bash
mv data data.bz2
```

This changes the filename from:

```text
data
```

to:

```text
data.bz2
```

---

## 📦 Step 15 — Decompress the Bzip2 File

Run:

```bash
bzip2 -d data.bz2
```

### What does `bzip2 -d` do?

```text
bzip2
```

works with bzip2-compressed files.

```text
-d
```

means:

```text
decompress
```

After decompression, we get:

```text
data
```

---

## 🔍 Step 16 — Check the File Again

Run:

```bash
file data
```

The output should indicate:

```text
data: gzip compressed data
```

So the file is compressed with gzip again.

---

## 🗜️ Step 17 — Rename the File

Run:

```bash
mv data data.gz
```

---

## 📦 Step 18 — Decompress the Gzip File

Run:

```bash
gzip -d data.gz
```

---

## 🔍 Step 19 — Check the File Again

Run:

```bash
file data
```

Now the output should show:

```text
data: POSIX tar archive
```

This means the file is a **TAR archive**.

---

## 📦 Step 20 — Rename the TAR Archive

Run:

```bash
mv data data.tar
```

---

## 📂 Step 21 — Extract the TAR Archive

Run:

```bash
tar -xf data.tar
```

### What does `tar -xf` do?

```text
tar
```

is used to create and extract archive files.

```text
-x
```

means:

```text
extract
```

```text
-f
```

means:

```text
use the specified archive file
```

Therefore:

```bash
tar -xf data.tar
```

extracts the contents of `data.tar`.

Now run:

```bash
ls
```

You should see another file:

```text
data5.bin
```

---

## 🔍 Step 22 — Identify `data5.bin`

Run:

```bash
file data5.bin
```

The output should indicate:

```text
data5.bin: POSIX tar archive
```

So this is another TAR archive.

---

## 📦 Step 23 — Extract `data5.bin`

Run:

```bash
tar -xf data5.bin
```

Then:

```bash
ls
```

You should now see:

```text
data6.bin
```

---

## 🔍 Step 24 — Identify `data6.bin`

Run:

```bash
file data6.bin
```

The output should indicate:

```text
data6.bin: bzip2 compressed data
```

So the file is compressed using **bzip2**.

---

## 🗜️ Step 25 — Rename `data6.bin`

Run:

```bash
mv data6.bin data6.bz2
```

---

## 📦 Step 26 — Decompress `data6.bz2`

Run:

```bash
bzip2 -d data6.bz2
```

This produces:

```text
data6
```

---

## 🔍 Step 27 — Check `data6`

Run:

```bash
file data6
```

The output should indicate:

```text
data6: POSIX tar archive
```

So `data6` is another TAR archive.

---

## 🗜️ Step 28 — Rename the TAR Archive

Run:

```bash
mv data6 data6.tar
```

---

## 📦 Step 29 — Extract `data6.tar`

Run:

```bash
tar -xf data6.tar
```

Then run:

```bash
ls
```

You should now see:

```text
data8.bin
```

---

## 🔍 Step 30 — Identify `data8.bin`

Run:

```bash
file data8.bin
```

The output should indicate:

```text
data8.bin: gzip compressed data
```

So this file is compressed using gzip.

---

## 🗜️ Step 31 — Rename `data8.bin`

Run:

```bash
mv data8.bin data8.gz
```

---

## 📦 Step 32 — Decompress `data8.gz`

Run:

```bash
gzip -d data8.gz
```

This produces:

```text
data8
```

---

## 🔍 Step 33 — Check the Final File

Run:

```bash
file data8
```

Now the output should be:

```text
data8: ASCII text
```

🎉 We have finally reached normal text!

---

## 🔓 Step 34 — Read the Password

Run:

```bash
cat data8
```

### What does `cat` do?

```text
cat
```

displays the contents of a file in the terminal.

The output is the password for:

```text
bandit13
```

> 🔐 Do not publish the actual password in your GitHub repository.

---

# 🖥️ Complete Command Sequence

```bash
ssh bandit12@bandit.labs.overthewire.org -p 2220

pwd

ls

file data.txt

mktemp -d

cp data.txt /tmp/tmp.XXXXXX/

cd /tmp/tmp.XXXXXX/

ls

xxd -r data.txt data

file data

mv data data.gz

gzip -d data.gz

file data

mv data data.bz2

bzip2 -d data.bz2

file data

mv data data.gz

gzip -d data.gz

file data

mv data data.tar

tar -xf data.tar

ls

file data5.bin

tar -xf data5.bin

ls

file data6.bin

mv data6.bin data6.bz2

bzip2 -d data6.bz2

file data6

mv data6 data6.tar

tar -xf data6.tar

ls

file data8.bin

mv data8.bin data8.gz

gzip -d data8.gz

file data8

cat data8
```

> ⚠️ `/tmp/tmp.XXXXXX/` is only an example. Replace it with the actual directory name returned by `mktemp -d`.

---

# 🧩 Command Breakdown

## `ssh`

```bash
ssh bandit12@bandit.labs.overthewire.org -p 2220
```

Connects to the Bandit Level 12 server.

---

## `pwd`

```bash
pwd
```

Shows the current working directory.

---

## `ls`

```bash
ls
```

Lists the files in the current directory.

---

## `file`

```bash
file filename
```

Identifies the type of a file.

This is one of the most important commands in this level.

---

## `mktemp -d`

```bash
mktemp -d
```

Creates a temporary directory.

---

## `cp`

```bash
cp source destination
```

Copies a file.

Example:

```bash
cp data.txt /tmp/tmp.XXXXXX/
```

---

## `cd`

```bash
cd directory
```

Changes the current directory.

---

## `xxd -r`

```bash
xxd -r data.txt data
```

Reverses the hexdump and creates the original binary file.

---

## `mv`

```bash
mv old_name new_name
```

Moves or renames a file.

Examples:

```bash
mv data data.gz
```

```bash
mv data data.bz2
```

```bash
mv data data.tar
```

---

## `gzip -d`

```bash
gzip -d file.gz
```

Decompresses a gzip file.

---

## `bzip2 -d`

```bash
bzip2 -d file.bz2
```

Decompresses a bzip2 file.

---

## `tar -xf`

```bash
tar -xf file.tar
```

Extracts the contents of a TAR archive.

---

## `cat`

```bash
cat data8
```

Displays the contents of the final text file.

---

# 🧠 Why We Used `file` Again and Again

The file is compressed repeatedly using different formats.

After every decompression, we do not automatically know what the next format is.

Therefore, we use:

```bash
file data
```

to identify the next format.

The process is:

```text
file
 ↓
Identify the format
 ↓
Rename if necessary
 ↓
Decompress / extract
 ↓
file again
 ↓
Repeat
```

---

# 🔄 Compression Chain

The complete chain is:

```text
data.txt
   ↓
Hexdump
   ↓
xxd -r
   ↓
gzip
   ↓
bzip2
   ↓
gzip
   ↓
tar
   ↓
tar
   ↓
bzip2
   ↓
tar
   ↓
gzip
   ↓
ASCII text
   ↓
cat
   ↓
Password for bandit13 🔓
```

---

# 🔄 Step-by-Step Format Table

| Step | File | Format | Action |
|------|------|--------|--------|
| 1 | `data.txt` | Hexdump | `xxd -r` |
| 2 | `data` | gzip | `gzip -d` |
| 3 | `data` | bzip2 | `bzip2 -d` |
| 4 | `data` | gzip | `gzip -d` |
| 5 | `data` | TAR | `tar -xf` |
| 6 | `data5.bin` | TAR | `tar -xf` |
| 7 | `data6.bin` | bzip2 | `bzip2 -d` |
| 8 | `data6` | TAR | `tar -xf` |
| 9 | `data8.bin` | gzip | `gzip -d` |
| 10 | `data8` | ASCII text | `cat` |

---

# 🧠 What I Learned

## 1. Hexdump

A hexdump represents binary data using hexadecimal values.

We can reverse a hexdump using:

```bash
xxd -r
```

---

## 2. `file`

The `file` command identifies the type of a file.

Example:

```bash
file data
```

It can tell us whether the file is:

```text
gzip compressed data
```

or:

```text
bzip2 compressed data
```

or:

```text
POSIX tar archive
```

or:

```text
ASCII text
```

---

## 3. Gzip

Gzip is a compression format.

To decompress:

```bash
gzip -d file.gz
```

---

## 4. Bzip2

Bzip2 is another compression format.

To decompress:

```bash
bzip2 -d file.bz2
```

---

## 5. TAR

TAR is an archive format used to package files together.

To extract:

```bash
tar -xf file.tar
```

---

## 6. `mv`

`mv` can move or rename files.

Example:

```bash
mv data data.gz
```

---

## 7. `cp`

`cp` copies files.

Example:

```bash
cp data.txt /tmp/tmp.XXXXXX/
```

---

## 8. Temporary Directories

`mktemp -d` creates a temporary working directory.

```bash
mktemp -d
```

This is useful when working with multiple temporary files.

---

# 🧩 Why Each Command Was Used

| Command | Purpose |
| ------- | ------- |
| `ssh` | Connect to the Bandit server |
| `pwd` | Show the current directory |
| `ls` | List files |
| `file` | Identify the file format |
| `mktemp -d` | Create a temporary directory |
| `cp` | Copy `data.txt` |
| `cd` | Enter the temporary directory |
| `xxd -r` | Reverse the hexdump |
| `mv` | Rename files |
| `gzip -d` | Decompress gzip files |
| `bzip2 -d` | Decompress bzip2 files |
| `tar -xf` | Extract TAR archives |
| `cat` | Display the final password |

---

# 🏁 Final Solution

The final command is:

```bash
cat data8
```

This displays the password needed to log in to:

```text
bandit13
```

---

# ➡️ Next Level

After getting the password, connect to **Bandit Level 13**:

```bash
ssh bandit13@bandit.labs.overthewire.org -p 2220
```

Enter the password obtained from Level 12.

---

## 📚 Commands Practiced

```bash
ssh
pwd
ls
file
mktemp
cp
cd
xxd
mv
gzip
bzip2
tar
cat
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
      gzip
       ↓
     bzip2
       ↓
      gzip
       ↓
      tar
       ↓
      tar
       ↓
     bzip2
       ↓
      tar
       ↓
      gzip
       ↓
  ASCII text
       ↓
      cat
       ↓
Bandit Level 13 🔓
```
