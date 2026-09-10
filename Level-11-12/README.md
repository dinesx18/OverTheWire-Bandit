# 🏴 Bandit Level 11 → Level 12

<img width="1375" height="522" alt="image" src="https://github.com/user-attachments/assets/93b10a96-1bda-4cb2-9c7f-5a8b4f7632b0" />


---

## 🎯 Goal

The password for the next level is stored in the file:

```text
data.txt
```

The contents of the file have been encrypted using **ROT13**.

We need to decode the ROT13 text to find the password for **Bandit Level 12**.

---

## 🔐 Step 1 — Connect to Bandit Level 11

First, connect to the Bandit Level 11 account using SSH.

```bash
ssh bandit11@bandit.labs.overthewire.org -p 2220
```

### Command Breakdown

```text
ssh
```

Used to securely connect to a remote computer.

```text
bandit11
```

The username for Level 11.

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

Specifies port **2220** instead of the default SSH port 22.

---

## 🔑 Step 2 — Enter the Password

After running the SSH command, the terminal asks for the password.

```text
bandit11@bandit.labs.overthewire.org's password:
```

Enter the password obtained from **Bandit Level 10 → Level 11**.

> ⚠️ The password is intentionally not included in this GitHub writeup.

If the password is correct, you will successfully log in as:

```text
bandit11
```

---

## 📍 Step 3 — Check the Current Directory

After logging in, check where you are.

```bash
pwd
```

### What does `pwd` do?

`pwd` means:

```text
Print Working Directory
```

It shows the current directory.

Example:

```text
/home/bandit11
```

---

## 📋 Step 4 — List the Files

Use:

```bash
ls
```

This displays the files in the current directory.

You should see:

```text
data.txt
```

---

## 📄 Step 5 — Read `data.txt`

Use:

```bash
cat data.txt
```

### What does `cat` do?

`cat` displays the contents of a file in the terminal.

The output will look like encoded text similar to:

```text
gur cnffjbeq vf ...
```

<img width="1717" height="133" alt="image" src="https://github.com/user-attachments/assets/1589e91b-c4d7-408d-88ef-c5284ead613e" />

- The text does not look like a normal password.
-
- This is because it is encoded using **ROT13**.

---

# 🔄 Step 6 — Understand ROT13

ROT13 means:

```text
Rotate by 13 positions
```

It replaces each letter with the letter that is **13 positions away** in the alphabet.

For example:

```text
A → N
B → O
C → P
D → Q
```

And:

```text
N → A
O → B
P → C
Q → D
```

Because the alphabet contains 26 letters, applying ROT13 twice returns the original text.

Example:

```text
hello
```

becomes:

```text
uryyb
```

Applying ROT13 again:

```text
uryyb
```

becomes:

```text
hello
```

---

# 🛠️ Step 7 — Decode ROT13

We can use the `tr` command to decode the text.

```bash
tr 'A-Za-z' 'N-ZA-Mn-za-m' < data.txt
```
<img width="1713" height="48" alt="image" src="https://github.com/user-attachments/assets/112632e0-0ca5-40a1-a106-1a919d52d4ac" />

---
# 🖥️ Terminal Screenshot

<img width="1715" height="247" alt="image" src="https://github.com/user-attachments/assets/f6bd5f5b-b5be-4b96-8458-2b68cc2179d4" />

## 🧩 Command Breakdown

### `tr`

```bash
tr
```

`tr` means **translate**.

It replaces characters with other characters.

---

### `'A-Za-z'`

```text
A-Za-z
```

This represents all uppercase and lowercase English letters:

```text
A-Z
a-z
```

---

### `'N-ZA-Mn-za-m'`

```text
N-ZA-M
n-za-m
```

This is the ROT13 replacement alphabet.

The uppercase letters:

```text
A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
```

are changed to:

```text
N O P Q R S T U V W X Y Z A B C D E F G H I J K L M
```

The lowercase letters are changed in the same way.

---

### `< data.txt`

```text
< data.txt
```

This redirects the contents of `data.txt` into the `tr` command.

Instead of:

```bash
cat data.txt
```

and then manually decoding the output, we directly send the file contents to `tr`.

---

# ✅ Step 8 — Get the Password

Run:

```bash
tr 'A-Za-z' 'N-ZA-Mn-za-m' < data.txt
```

The command will output the decoded text.

The decoded text contains the password for:

```text
bandit12
```

> 🔐 Do not publish the actual password in your GitHub repository.

---

# 🧠 What I Learned

### 1. ROT13

ROT13 is a simple substitution cipher where every letter is rotated by 13 positions.

```text
A ↔ N
B ↔ O
C ↔ P
```

---

### 2. `tr`

The `tr` command can translate or replace characters.

Example:

```bash
tr 'A-Z' 'N-ZA-M'
```

---

### 3. Input Redirection

The `<` symbol redirects a file into a command.

Example:

```bash
command < file
```

This means:

```text
Take the contents of file
        ↓
Send them to the command
```

---

### 4. Linux Command-Line Tools

This level showed how multiple Linux tools can be used to process file contents without opening a graphical application.

---

# 🧩 Why Each Command Was Used

| Command | Purpose                               |
| ------- | ------------------------------------- |
| `ssh`   | Connect to the Bandit server          |
| `pwd`   | Show the current directory            |
| `ls`    | List files                            |
| `cat`   | Display file contents                 |
| `tr`    | Translate characters                  |
| `<`     | Redirect file contents into a command |

---

# 🔄 Complete Command Flow

```bash
ssh bandit11@bandit.labs.overthewire.org -p 2220
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

The output is ROT13 encoded.

⬇️

```bash
tr 'A-Za-z' 'N-ZA-Mn-za-m' < data.txt
```

⬇️

```text
ROT13 decoded
        ↓
Password for bandit12
```

---

# 🎓 Key Takeaway

The main lesson from **Bandit Level 11 → Level 12** is learning how to recognize and decode **ROT13** using Linux commands.

The important command is:

```bash
tr 'A-Za-z' 'N-ZA-Mn-za-m' < data.txt
```

This translates every letter by 13 positions and reveals the password for the next level.

---

# 🏁 Final Solution

```bash
tr 'A-Za-z' 'N-ZA-Mn-za-m' < data.txt
```

The output is the password needed to log in to:

```text
bandit12
```

---

# ➡️ Next Level

After getting the password, connect to **Bandit Level 12**:

```bash
ssh bandit12@bandit.labs.overthewire.org -p 2220
```

Enter the password obtained from this level.

---

## 📚 Commands Practiced

```bash
ssh
pwd
ls
cat
tr
```

---

## ⭐ Level Completed

```text
Bandit Level 11
       ↓
   ROT13 encoded
       ↓
      tr
       ↓
ROT13 decoded
       ↓
Bandit Level 12 🔓
```
