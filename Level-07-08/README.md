# 🏴 Bandit Level 7 → Level 8

<img width="1382" height="377" alt="image" src="https://github.com/user-attachments/assets/45932378-90d8-4388-ba61-271307aebe60" />


---

## 🎯 Goal

The password for the next level is stored in the file:

```text
data.txt
```

The password is located next to the word:

```text
millionth
```

So I need to search inside `data.txt` and find the line containing `millionth`.

---

## 🔐 Step 1 — Connect to Bandit Level 7

I connect to the Bandit Level 7 account using SSH.

The command is:

```bash
ssh bandit7@bandit.labs.overthewire.org -p 2220
```

### 🔎 Breaking Down the Command

```text
ssh bandit7@bandit.labs.overthewire.org -p 2220
│   │                                      │  │
│   │                                      │  └── SSH port
│   │                                      └───── Port option
│   └─────────────────────────────────────────── Username + server
└──────────────────────────────────────────────── Secure Shell
```

- `ssh` → Connects to a remote computer.
- `bandit7` → The username for this level.
- `@` → Separates the username from the server.
- `bandit.labs.overthewire.org` → The Bandit server.
- `-p` → Specifies the SSH port.
- `2220` → The port used by the Bandit game.

After running the command, the server asks for the password:

```text
bandit7@bandit.labs.overthewire.org's password:
```

I enter the password obtained from **Level 6 → Level 7**.

> ⚠️ When typing a password in Linux, the characters are not displayed. This is normal.

After successful login, the terminal prompt becomes:

```text
bandit7@bandit:~$
```

This confirms that I am logged in as:

```text
bandit7
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
/home/bandit7
```

So I am currently inside:

```text
/home/bandit7
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

## 📖 Step 4 — Understand the File

The level tells me that the password is located next to the word:

```text
millionth
```

The file contains many lines, so opening the entire file with:

```bash
cat data.txt
```

would produce a lot of output.

Instead, I can search directly for the word:

```text
millionth
```

For this, I can use the `grep` command.

---

# 🔎 Step 5 — Search for `millionth`

I used:

```bash
grep millionth data.txt
```

This searches the file for the word:

```text
millionth
```

---

## 🧩 Breaking Down the Command

```text
grep millionth data.txt
│    │         │
│    │         └── File to search
│    └──────────── Text to search for
└───────────────── Search command
```

### `grep`

```bash
grep
```

`grep` is used to search for matching text inside files.

---

### `millionth`

```text
millionth
```

This is the word I am searching for.

The level tells me that the password is located next to this word.

---

### `data.txt`

```text
data.txt
```

This is the file I want to search.

Therefore:

```bash
grep millionth data.txt
```

means:

> Search `data.txt` for the word `millionth`.

---

# 🧪 Step 6 — Run the Command

I run:

```bash
grep millionth data.txt
```

The command finds the matching line:

```text
millionth YOUR_PASSWORD_HERE
```

The first part is:

```text
millionth
```

and the value next to it is the password for the next level.

> ⚠️ I do not publish the actual password in this GitHub README.

---

# 🔑 Step 7 — Get the Password for Level 8

The text after:

```text
millionth
```

is the password for:

```text
bandit8
```

I copy the password from the terminal and use it to log in to the next level.

---

# 🖥️ Terminal Screenshot

<img width="1711" height="177" alt="image" src="https://github.com/user-attachments/assets/9921c34c-78ca-4e82-9fc4-7afe864b4870" />


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

### `grep`

```bash
grep millionth data.txt
```

Searches for specific text inside a file.

---

### Search word

```text
millionth
```

This is the word I was asked to find.

---

### `data.txt`

```text
data.txt
```

This is the file that contains the password.

---

# 🧩 Why Each Command Was Used

| Command | Why I Used It |
|---|---|
| `pwd` | To check my current location |
| `ls` | To see the available files |
| `grep millionth data.txt` | To search for `millionth` inside `data.txt` |

---

# 🎓 Key Takeaway

This level taught me how to search for specific text inside a file.

Instead of displaying the entire file using:

```bash
cat data.txt
```

I used:

```bash
grep millionth data.txt
```

This directly searches for the word:

```text
millionth
```

The matching line contains:

```text
millionth PASSWORD
```

The password next to `millionth` is used to continue to:

**Bandit Level 8**.

The main thing I learned is:

> **Use `grep` when you need to find specific text inside a file.**

---

# 🔄 Complete Command Flow

```text
SSH as bandit7
       ↓
      pwd
       ↓
      ls
       ↓
   data.txt
       ↓
grep millionth data.txt
       ↓
Find the line containing "millionth"
       ↓
Password next to "millionth"
       ↓
Password for bandit8
```

---

# 🏁 Final Solution

The main command that solves this level is:

```bash
grep millionth data.txt
```

It searches `data.txt` for:

```text
millionth
```

The password next to `millionth` is the password for:

```text
bandit8
```

---

## ➡️ Next

**Bandit Level 8 → Level 9** 🚀
