# 🏴 Bandit Level 9 → Level 10

<img width="1382" height="352" alt="image" src="https://github.com/user-attachments/assets/726f33eb-4cf9-40b1-a493-208c7d33db80" />

---

## 🎯 Goal

The password for the next level is stored in the file:

```text
data.txt
```

The password is hidden inside one of the few human-readable strings in the file.

The password is preceded by several:

```text
=
```

characters.

So I need to:

1. Find `data.txt`.
2. Extract the human-readable strings.
3. Search for strings containing several `=` characters.
4. Identify the password.

---

## 🔐 Step 1 — Connect to Bandit Level 9

I connect to the Bandit Level 9 account using SSH.

The command is:

```bash
ssh bandit9@bandit.labs.overthewire.org -p 2220
```

### 🔎 Breaking Down the Command

```text
ssh bandit9@bandit.labs.overthewire.org -p 2220
│   │                                      │  │
│   │                                      │  └── SSH port
│   │                                      └───── Port option
│   └─────────────────────────────────────────── Username + server
└──────────────────────────────────────────────── Secure Shell
```

- `ssh` → Connects to a remote computer.
- `bandit9` → The username for this level.
- `@` → Separates the username from the server.
- `bandit.labs.overthewire.org` → The Bandit server.
- `-p` → Specifies the SSH port.
- `2220` → The port used by the Bandit game.

After running the command, the server asks:

```text
bandit9@bandit.labs.overthewire.org's password:
```

I enter the password obtained from **Level 8 → Level 9**.

> ⚠️ When typing a password in Linux, the characters are not displayed. This is normal.

After successful login, the terminal prompt becomes:

```text
bandit9@bandit:~$
```

This confirms that I am logged in as:

```text
bandit9
```

---

## 📍 Step 2 — Check My Current Location

I used:

```bash
pwd
```

### 🔎 What does `pwd` mean?

`pwd` means:

```text
Print Working Directory
```

It shows the directory I am currently inside.

The output is:

```text
/home/bandit9
```

So I am currently inside:

```text
/home/bandit9
```

---

## 📋 Step 3 — List the Files

I used:

```bash
ls
```

The output showed:

```text
data.txt
```

This means the file I need to investigate is:

```text
data.txt
```

---

## 📖 Step 4 — Understand the Problem

The level says that the password is hidden inside one of the few human-readable strings in `data.txt`.

The password is preceded by several:

```text
=
```

characters.

The file contains binary data, so simply using:

```bash
cat data.txt
```

is not the best way to find the password.

I need to extract the readable strings first.

---

## ⚠️ Step 5 — Why `cat` Is Not Useful Here

I could use:

```bash
cat data.txt
```

but the file contains binary data.

This can produce a lot of unreadable or strange characters.

The password is hidden somewhere inside the readable parts of the file.

Therefore, I need a command that extracts readable strings.

---

# 🔤 Step 6 — Use the `strings` Command

I used:

```bash
strings data.txt
```

### 🔎 What does `strings` do?

The `strings` command extracts sequences of printable characters from a file.

This is useful when a file contains binary data but also contains readable text.

For example:

```text
Binary data
     ↓
Some readable text
     ↓
More binary data
```

`strings` helps extract the readable text.

So:

```bash
strings data.txt
```

means:

> Extract the readable strings from `data.txt`.

---

# 🔎 Step 7 — Search for the `=` Characters

The level tells me that the password is preceded by several `=` characters.

Instead of manually checking all the output from:

```bash
strings data.txt
```

I can use `grep`.

The command is:

```bash
strings data.txt | grep "===="
```

---

## 🧩 Breaking Down the Command

```text
strings data.txt | grep "===="
│               │  │    │
│               │  │    └── Text pattern to search
│               │  └─────── Search command
│               └────────── Pipe
└────────────────────────── Extract readable strings
```

---

## 🔤 `strings data.txt`

```bash
strings data.txt
```

This extracts the human-readable strings from `data.txt`.

---

## 🔗 `|`

```text
|
```

The pipe sends the output of one command into another command.

So:

```bash
strings data.txt | grep "===="
```

works like:

```text
strings data.txt
       ↓
Readable strings
       ↓
       |
       ↓
grep "===="
       ↓
Matching lines
```

---

## 🔎 `grep`

```bash
grep
```

`grep` searches text for a specific pattern.

---

## `====`

```text
====
```

This is the pattern I am searching for.

The level tells me that the password is preceded by several `=` characters.

So I search for lines containing multiple `=` characters.

---

# 🧪 Step 8 — Run the Complete Command

I run:

```bash
strings data.txt | grep "===="
```

The command filters the readable strings and displays the lines containing several `=` characters.

The output contains the line with the password.

> ⚠️ I do not publish the actual password in this GitHub README.

---

# 🎯 Step 9 — Identify the Password

The important result has the following structure:

```text
========== PASSWORD
```

The readable text after the `=` characters is the password.

I identify that value as the password for the next level.

---

# 🔑 Step 10 — Get the Password for Level 10

The password found using:

```bash
strings data.txt | grep "===="
```

is used to log in as:

```text
bandit10
```

I copy the password from my terminal and use it for the next level.

> ⚠️ The actual password is not included in this README.

---

# 🖥️ Terminal Screenshot

<img width="1717" height="657" alt="Bandit Level 9 Terminal" src="YOUR_SCREENSHOT_LINK_HERE" />

---

# 🧠 What I Learned

### `pwd`

```bash
pwd
```

Shows the current working directory.

---

### `ls`

```bash
ls
```

Lists files and directories.

---

### `file`

```bash
file data.txt
```

Identifies the type of the file.

---

### `cat`

```bash
cat data.txt
```

Displays the contents of a file.

However, it is not very useful here because `data.txt` contains binary data.

---

### `strings`

```bash
strings data.txt
```

Extracts human-readable strings from a file.

---

### `grep`

```bash
grep "===="
```

Searches for lines containing the specified pattern.

---

### `|`

```text
|
```

The pipe sends the output of one command into another command.

---

# 🧩 Why Each Command Was Used

| Command | Why I Used It |
|---|---|
| `pwd` | To check my current location |
| `ls` | To find `data.txt` |
| `file data.txt` | To check the file type |
| `cat data.txt` | To understand what happens when viewing the file directly |
| `strings data.txt` | To extract readable strings |
| `grep "===="` | To search for strings containing several `=` characters |
| `strings data.txt \| grep "===="` | To combine both operations and find the password |

---

# 🎓 Key Takeaway

This level taught me how to find readable text inside a file containing binary data.

The important command is:

```bash
strings data.txt | grep "===="
```

First:

```bash
strings data.txt
```

extracts the human-readable strings.

Then:

```bash
grep "===="
```

filters those strings and shows the lines containing several `=` characters.

The pipe:

```text
|
```

connects the two commands.

So the process is:

```text
data.txt
   ↓
strings
   ↓
Extract readable strings
   ↓
grep "===="
   ↓
Find strings with several =
   ↓
Identify password
   ↓
Password for bandit10
```

The main thing I learned is:

> **Use `strings` when a file contains binary data but you need to find readable text inside it.**

---

# 🔄 Complete Command Flow

```text
SSH as bandit9
       ↓
      pwd
       ↓
      ls
       ↓
   data.txt
       ↓
file data.txt
       ↓
File contains binary data
       ↓
strings data.txt
       ↓
Extract readable strings
       ↓
grep "===="
       ↓
Find strings containing several =
       ↓
Identify password
       ↓
Password for bandit10
```

---

# 🏁 Final Solution

The main command that solves this level is:

```bash
strings data.txt | grep "===="
```

### Command 1

```bash
strings data.txt
```

Extracts human-readable strings from `data.txt`.

### Command 2

```bash
grep "===="
```

Searches for strings containing several `=` characters.

### Combined Command

```bash
strings data.txt | grep "===="
```

This reveals the readable string containing the password for:

```text
bandit10
```

---

## ➡️ Next

**Bandit Level 10 → Level 11** 🚀
