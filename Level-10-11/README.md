# 🏴 Bandit Level 10 → Level 11

<img width="1382" height="423" alt="image" src="https://github.com/user-attachments/assets/aae91111-6851-49c6-9016-696d443083e6" />

---

## 🎯 Goal

The password for the next level is stored in:

```text
data.txt
```

The file contains **Base64 encoded data**.

So I need to decode the contents of `data.txt` to get the password.

---

## 🔐 Step 1 — Connect to Bandit Level 10

Now that I have the password for the next level, I need to log in as `bandit10`.

The username changes from:

```text
bandit9
```

to:

```text
bandit10
```

I use the same Bandit server and SSH port.

The command is:

```bash
ssh bandit10@bandit.labs.overthewire.org -p 2220
```

After running the command, the server asks:

```text
bandit10@bandit.labs.overthewire.org's password:
```

## 🔑 Step 2 — Enter the Password

I enter the password that I obtained from the previous level:

**Bandit Level 9 → Level 10**

> ⚠️ When typing the password in the Linux terminal, the characters are not displayed. This is normal.

After entering the correct password and pressing Enter, I successfully log in.

The terminal prompt becomes:

```text
bandit10@bandit:~$
```

This confirms that I am now logged in as:

```text
bandit10
```

---

## 🎯 Goal

The password for the next level is stored in:

```text
data.txt
```

The file contains:

```text
Base64 encoded data
```

So I need to decode it.

---

## 📋 Step 3 — Check the Files

First, I used:

```bash
ls
```

The output showed:

```text
data.txt
```

This means the file containing the encoded password is:

```text
data.txt
```

---

## 📖 Step 4 — View the Encoded Data

I used:

```bash
cat data.txt
```

The terminal displays something similar to:

```text
VGhlIHBhc3N3b3JkIGlzIGhpZGRlbiBoZXJl
```

The output looks like random letters and numbers.

This is because the contents are **Base64 encoded**.

<img width="1710" height="135" alt="image" src="https://github.com/user-attachments/assets/210a0c57-99c8-4c57-b976-01e949add119" />

---

# 🔤 Step 5 — What Is Base64?

Base64 is an encoding method used to represent data using a set of characters.

A Base64 string can contain:

```text
A-Z
a-z
0-9
+
/
=
```

For example:

```text
SGVsbG8=
```

can be decoded to:

```text
Hello
```

Base64 is **encoding**, not encryption.

That means it does not provide secret protection. It simply changes the representation of the data.

---

# 🔓 Step 6 — Use the `base64` Command

Linux provides a command called:

```bash
base64
```

It can be used to encode and decode Base64 data.

To decode a file, I use:

```bash
base64 -d data.txt
```

---

## 🔎 Breaking Down the Command

```text
base64 -d data.txt
│      │  │
│      │  └── File containing Base64 data
│      └───── Decode option
└──────────── Base64 command
```

### `base64`

```bash
base64
```

This command is used to encode or decode Base64 data.

### `-d`

```bash
-d
```

The `-d` option means:

```text
decode
```

So:

```bash
base64 -d
```

means:

> Decode Base64 data.

### `data.txt`

```text
data.txt
```

This is the file containing the encoded data.

Therefore:

```bash
base64 -d data.txt
```

means:

> Decode the Base64 data stored inside `data.txt`.

---

# 🧪 Step 7 — Decode the File

I run:

```bash
base64 -d data.txt
```

- The command decodes the contents of `data.txt`.
- The terminal displays the password for the next level.
- The output will look like:

```text
YOUR_PASSWORD_HERE
```

<img width="1717" height="67" alt="image" src="https://github.com/user-attachments/assets/50ba82d0-38b8-47a3-ac34-f6fea2e1793d" />


---

# 🔑 Step 8 — Get the Password for Level 11

The decoded output is the password for:

```text
bandit11
```

- I copy the password from the terminal.
- I will use it to log in to the next level.

---

# 🖥️ Terminal Screenshot

<img width="1712" height="227" alt="image" src="https://github.com/user-attachments/assets/142a8b3e-9d69-4533-8ee7-c4e937babbce" />


---

# 🧠 What I Learned

### `pwd`

```bash
pwd
```

Shows my current working directory.

---

### `ls`

```bash
ls
```

Lists the files and directories.

---

### `cat`

```bash
cat data.txt
```

Displays the contents of `data.txt`.

---

### `base64`

```bash
base64
```

Used to encode or decode Base64 data.

---

### `-d`

```bash
-d
```

Means:

```text
decode
```

---

### `base64 -d data.txt`

```bash
base64 -d data.txt
```

Decodes the Base64 encoded contents of `data.txt`.

---

# 🧩 Why Each Command Was Used

| Command | Why I Used It |
|---|---|
| `pwd` | To check my current location |
| `ls` | To find `data.txt` |
| `cat data.txt` | To view the encoded data |
| `base64 -d data.txt` | To decode the Base64 data and obtain the password |

---

# 🎓 Key Takeaway

This level taught me how to decode Base64 data using Linux.

The important command is:

```bash
base64 -d data.txt
```

The command:

```text
base64
```

selects the Base64 tool.

The option:

```text
-d
```

means decode.

The file:

```text
data.txt
```

contains the Base64 encoded password.

So:

```text
data.txt
     ↓
Base64 encoded data
     ↓
base64 -d
     ↓
Decoded text
     ↓
Password for bandit11
```

The main thing I learned is:

> **Base64 is an encoding method, and `base64 -d` can be used to decode Base64 data.**

---

# 🔄 Complete Command Flow

```text
SSH as bandit10
       ↓
      pwd
       ↓
      ls
       ↓
   data.txt
       ↓
cat data.txt
       ↓
Base64 encoded text
       ↓
base64 -d data.txt
       ↓
Decoded text
       ↓
Password for bandit11
```

---

# 🏁 Final Solution

First, I can view the encoded data:

```bash
cat data.txt
```

Then I decode it:

```bash
base64 -d data.txt
```

The decoded output is the password for:

```text
bandit11
```

---

## ➡️ Next

**Bandit Level 11 → Level 12** 🚀
