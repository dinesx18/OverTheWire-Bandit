# 🏴 Bandit Level 5 → Level 6

<img width="1407" height="355" alt="Bandit Level 5 → Level 6" src="YOUR_SCREENSHOT_LINK_HERE" />

---

## 🎯 Goal

The password for the next level is stored in a file somewhere under the `inhere` directory.

The file must be:

- Human-readable
- Exactly **1033 bytes** in size
- Not executable

So I need to search for a file that matches these conditions.

---

## 🔐 Step 1 — Connect to Bandit Level 5

I connect to the Bandit Level 5 account using SSH.

The command is:

```bash
ssh bandit5@bandit.labs.overthewire.org -p 2220
```

### 🔎 Breaking Down the Command

```text
ssh bandit5@bandit.labs.overthewire.org -p 2220
│   │                                      │  │
│   │                                      │  └── SSH port
│   │                                      └───── Port option
│   └─────────────────────────────────────────── Username + server
└──────────────────────────────────────────────── Secure Shell
```

- `ssh` → Connects to a remote computer.
- `bandit5` → The username I want to log in as.
- `@` → Separates the username from the server.
- `bandit.labs.overthewire.org` → The Bandit server.
- `-p` → Specifies the SSH port.
- `2220` → The port used by the Bandit game.

After running the command, the server asks:

```text
bandit5@bandit.labs.overthewire.org's password:
```

I enter the password obtained from **Level 4 → Level 5**.

> ⚠️ When typing a password in Linux, the characters are not displayed. This is normal.

After successful login, the prompt becomes:

```text
bandit5@bandit:~$
```

This confirms that I am logged in as:

```text
bandit5
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

It shows my current location.

The output was:

```text
/home/bandit5
```

So I am currently inside:

```text
/home/bandit5
```

---

## 📋 Step 3 — List the Files

I used:

```bash
ls
```

The output showed:

```text
inhere
```

This means there is a directory called:

```text
inhere
```

inside `/home/bandit5`.

---

## 📂 Step 4 — Enter the `inhere` Directory

I used:

```bash
cd inhere
```

### 🔎 Breaking Down the Command

```text
cd inhere
│  │
│  └── Directory I want to enter
└───── Change directory
```

- `cd` → Changes the current directory.
- `inhere` → The directory I want to enter.

After running the command, the prompt becomes:

```text
bandit5@bandit:~/inhere$
```

This confirms that I am now inside the `inhere` directory.

---

## 📋 Step 5 — Check the Contents of `inhere`

I used:

```bash
ls
```

The output showed many directories:

```text
maybehere00
maybehere01
maybehere02
maybehere03
maybehere04
maybehere05
maybehere06
maybehere07
maybehere08
maybehere09
maybehere10
maybehere11
maybehere12
maybehere13
maybehere14
maybehere15
maybehere16
maybehere17
maybehere18
maybehere19
```

There are many directories.

Each directory can contain files, so manually checking every file would take a lot of time.

Instead, I can use the `find` command.

---

## 🔎 Step 6 — Search for the Correct File

I used:

```bash
find . -type f -size 1033c ! -executable
```

This is the most important command in this level.

It searches through the current directory and all its subdirectories.

---

## 🧩 Breaking Down the Command

```text
find . -type f -size 1033c ! -executable
│    │  │       │            │
│    │  │       │            └── Must NOT be executable
│    │  │       └─────────────── Exactly 1033 bytes
│    │  └─────────────────────── Regular file
│    └────────────────────────── Current directory
└─────────────────────────────── Search
```

### `find`

```bash
find
```

Searches for files and directories.

---

### `.`

```text
.
```

The dot means:

```text
Current directory
```

So:

```bash
find .
```

means:

> Start searching from the current directory.

I am currently inside:

```text
/home/bandit5/inhere
```

so the search starts there.

---

### `-type f`

```bash
-type f
```

This tells `find` to search only for regular files.

```text
-type
```

means:

> Check the type.

```text
f
```

means:

> Regular file.

Therefore:

```bash
-type f
```

means:

> Find only files.

---

### `-size 1033c`

```bash
-size 1033c
```

This searches for a file that is exactly:

```text
1033 bytes
```

The `c` means:

```text
bytes
```

Therefore:

```bash
-size 1033c
```

means:

> Find a file whose size is exactly 1033 bytes.

---

### `! -executable`

```bash
! -executable
```

The `!` means:

```text
NOT
```

And:

```text
-executable
```

checks whether the file is executable.

Therefore:

```bash
! -executable
```

means:

> The file must NOT be executable.

---

## 🎯 Step 7 — Find the Matching File

After running:

```bash
find . -type f -size 1033c ! -executable
```

the command returned:

```text
./maybehere07/.file2
```

This means Linux found the file that matches the required conditions.

The file is:

```text
.file2
```

inside:

```text
maybehere07
```

---

## 📂 Step 8 — Understand the File Path

The result was:

```text
./maybehere07/.file2
```

Breaking it down:

```text
./maybehere07/.file2
│  │         │
│  │         └── File name
│  └──────────── Directory
└─────────────── Current directory
```

- `./` → Current directory.
- `maybehere07` → Directory containing the file.
- `.file2` → The file containing the password.

The filename begins with:

```text
.
```

so `.file2` is a hidden file.

---

## 📖 Step 9 — Read the File

I used:

```bash
cat ./maybehere07/.file2
```

### 🔎 Breaking Down the Command

```text
cat ./maybehere07/.file2
│   │
│   └── Path to the file
└────── Display the file contents
```

- `cat` → Displays the contents of a file.
- `./` → Current directory.
- `maybehere07` → Directory containing the file.
- `.file2` → The hidden file.

The command displays the password stored inside the file.

---

## 🔑 Step 10 — Get the Password for Level 6

The terminal displayed the password:

```text
YOUR_PASSWORD_FROM_TERMINAL
```

I then use this password to log in as:

```text
bandit6
```

> ⚠️ I am not publishing the actual password in this GitHub README.

---

## 🖥️ Terminal Screenshot

<img width="1717" height="657" alt="Bandit Level 5 Terminal" src="YOUR_SCREENSHOT_LINK_HERE" />

---

## 🧠 What I Learned

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

Lists files and directories.

---

### `cd`

```bash
cd inhere
```

Changes the current directory.

---

### `find`

```bash
find .
```

Searches for files and directories from the current directory.

---

### `-type f`

```bash
-type f
```

Searches only for regular files.

---

### `-size 1033c`

```bash
-size 1033c
```

Searches for a file that is exactly 1033 bytes.

The `c` means bytes.

---

### `! -executable`

```bash
! -executable
```

Searches for files that are not executable.

---

### `cat`

```bash
cat ./maybehere07/.file2
```

Displays the contents of the file.

---

## 🧩 Why Each Command Was Used

| Command | Why I Used It |
|---|---|
| `pwd` | To check my current location |
| `ls` | To see files and directories |
| `cd inhere` | To enter the `inhere` directory |
| `find .` | To search through the directory and subdirectories |
| `-type f` | To search only regular files |
| `-size 1033c` | To find a file exactly 1033 bytes |
| `! -executable` | To exclude executable files |
| `cat` | To read the password from the file |

---

## 🎓 Key Takeaway

This level taught me how to find a file using specific conditions.

Instead of manually checking all the directories, I used:

```bash
find . -type f -size 1033c ! -executable
```

This searches for a file that is:

```text
Regular file
     +
Exactly 1033 bytes
     +
Not executable
```

The command found:

```text
./maybehere07/.file2
```

I then used:

```bash
cat ./maybehere07/.file2
```

to display the password.

The main thing I learned is:

> **The `find` command can search for files based on specific properties.**

---

## 🔄 Complete Command Flow

```text
SSH as bandit5
       ↓
      pwd
       ↓
      ls
       ↓
  cd inhere
       ↓
      ls
       ↓
Many maybehere directories
       ↓
find . -type f -size 1033c ! -executable
       ↓
./maybehere07/.file2
       ↓
cat ./maybehere07/.file2
       ↓
Password for bandit6
```

---

## 🏁 Final Solution

The main command that solves this level is:

```bash
find . -type f -size 1033c ! -executable
```

It finds:

```text
./maybehere07/.file2
```

Then:

```bash
cat ./maybehere07/.file2
```

displays the password for the next level.

---

## ➡️ Next

**Bandit Level 6 → Level 7** 🚀
