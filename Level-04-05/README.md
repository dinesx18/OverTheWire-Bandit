# 🏴 Bandit Level 4 → Level 5

<img width="1403" height="382" alt="image" src="https://github.com/user-attachments/assets/13aa54bc-cc41-4a9f-b337-e0a1e1737081" />

---

## 🎯 Goal

The password for the next level is stored in the **only human-readable file** in the `inhere` directory.

There are several files in the directory, so I need to identify which file contains readable text.

---

## 🔐 Step 1 — Connect to Bandit Level 4

First, I connect to the Bandit Level 4 account using SSH.

The command is:

```bash
ssh bandit4@bandit.labs.overthewire.org -p 2220
```

### 🔎 Breaking Down the Command

```text
ssh bandit4@bandit.labs.overthewire.org -p 2220
│   │                                      │  │
│   │                                      │  └── SSH port
│   │                                      └───── Port option
│   └─────────────────────────────────────────── Username + server
└──────────────────────────────────────────────── Secure Shell
```

- `ssh` → Connects to a remote computer using Secure Shell.
- `bandit4` → The username I want to log in as.
- `@` → Separates the username from the hostname.
- `bandit.labs.overthewire.org` → The Bandit server.
- `-p` → Specifies the SSH port.
- `2220` → The port used by the Bandit game.

After running the command, the server asks for the password:

```text
bandit4@bandit.labs.overthewire.org's password:
```

I enter the password I obtained from **Level 3 → Level 4**.

> ⚠️ Linux does not show characters while typing a password in the terminal. This is normal.

After successful login, the prompt becomes:

```text
bandit4@bandit:~$
```

This confirms that I am logged in as:

```text
bandit4
```

---

## 📍 Step 2 — Check My Current Location

Before searching for files, I used:

```bash
pwd
```

### 🔎 What does `pwd` mean?

`pwd` means:

```text
Print Working Directory
```

It shows the directory I am currently inside.

The output was:

```text
/home/bandit4
```

This means I am currently inside:

```text
/home/bandit4
```

### 🧠 Why did I use `pwd`?

I used `pwd` to confirm exactly where I am before working with files.

---

## 📋 Step 3 — List the Files

Next, I used:

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

inside `/home/bandit4`.

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

After running the command, my prompt changed to:

```text
bandit4@bandit:~/inhere$
```

This tells me that I am now inside the `inhere` directory.

---

## 📋 Step 5 — List the Files Inside `inhere`

I used:

```bash
ls
```

The output showed:

```text
-file00
-file01
-file02
-file03
-file04
-file05
-file06
-file07
-file08
-file09
```

There are **10 files**.

The filenames are:

```text
-file00
-file01
-file02
-file03
-file04
-file05
-file06
-file07
-file08
-file09
```

The problem is that I don't know which file contains the password.

The goal says that the password is inside the **only human-readable file**.

So I need to check the type of every file.

---

## ⚠️ Step 6 — Why Can't I Simply Use `cat`?

I first tried:

```bash
cat -- -file00
```

The command executed, but the output looked like random or unreadable characters.

### 🤔 Why did this happen?

`cat` simply displays the contents of a file.

It does **not** determine whether the file contains readable text.

If a file contains binary data, `cat` may display strange characters on the terminal.

So:

```bash
cat -- -file00
```

did not tell me whether `-file00` was the correct file.

It only showed me the raw contents of that file.

Therefore, I needed another command.

---

## 🧹 Step 7 — Reset the Terminal

Because the binary file produced strange characters on the terminal, I used:

```bash
reset
```

### 🔎 What does `reset` do?

`reset` resets the terminal to a normal state.

After displaying binary data, the terminal can sometimes look strange or behave unexpectedly.

Using:

```bash
reset
```

helps restore the terminal display.

After running it, the terminal returned to normal.

---

## 🔎 Step 8 — Check the Type of One File

I then tried:

```bash
file -- -file00
```

### 🔎 Breaking Down the Command

```text
file -- -file00
│    │  │
│    │  └── Filename
│    └───── Stop processing options
└────────── Identify the file type
```

- `file` → Identifies the type of a file.
- `--` → Tells the command that option processing has ended.
- `-file00` → The filename.

### 🤔 Why is `--` important?

The filename begins with:

```text
-
```

Linux commands can interpret something beginning with `-` as an option.

Using:

```bash
file -- -file00
```

makes it clear that:

```text
-file00
```

is a filename.

The output was:

```text
-file00: data
```

This tells me that `-file00` is a **data** file.

It is not the human-readable file I am looking for.

---

## 🔍 Step 9 — Check All Files at Once

Instead of checking every file individually, I can check all of them with one command:

```bash
file -- *
```

### 🔎 Breaking Down the Command

```text
file -- *
│    │  │
│    │  └── Wildcard matching the files
│    └───── Stop processing options
└────────── Identify file types
```

### `file`

The `file` command identifies what type of data a file contains.

### `--`

The `--` tells the command:

> Stop interpreting the following arguments as options.

This is important because all the filenames begin with `-`.

### `*`

The `*` is a wildcard.

It matches the files in the current directory.

So:

```bash
file -- *
```

means:

> Check the type of all the files in the current directory.

---

## 🧪 Step 10 — Analyze the Output

The command produced:

```text
-file00: data
-file01: data
-file02: data
-file03: data
-file04: data
-file05: data
-file06: OpenPGP Public Key
-file07: ASCII text
-file08: data
-file09: Motorola S-Record; binary data in text format
```

Now I can analyze each file.

### 📄 `-file00`

```text
-file00: data
```

This is identified as:

```text
data
```

So it is not the human-readable file.

### 📄 `-file01`

```text
-file01: data
```

Not the correct file.

### 📄 `-file02`

```text
-file02: data
```

Not the correct file.

### 📄 `-file03`

```text
-file03: data
```

Not the correct file.

### 📄 `-file04`

```text
-file04: data
```

Not the correct file.

### 📄 `-file05`

```text
-file05: data
```

Not the correct file.

### 🔐 `-file06`

```text
-file06: OpenPGP Public Key
```

This file contains an:

```text
OpenPGP Public Key
```

This is cryptographic data, so it is not the human-readable text file I need.

Therefore:

```text
-file06
```

is not the correct file.

### ⭐ `-file07`

```text
-file07: ASCII text
```

This is important.

The file is identified as:

```text
ASCII text
```

ASCII text represents ordinary readable text characters.

The Bandit goal says that the password is in the **only human-readable file**.

Therefore:

```text
-file07
```

is the file I need.

### 📄 `-file08`

```text
-file08: data
```

This is identified as data.

So it is not the correct file.

### 📄 `-file09`

```text
-file09: Motorola S-Record; binary data in text format
```

This is not the simple human-readable password file I am looking for.

Therefore, it is not the correct file.

---

## 🎯 Step 11 — Find the Correct File

After checking all the file types, I found:

```text
-file07: ASCII text
```

This matches the requirement:

```text
Only human-readable file
```

Therefore, the file containing the password is:

```text
-file07
```

---

## 📖 Step 12 — Read `-file07`

Because the filename starts with `-`, I use `--` before the filename.

The command is:

```bash
cat -- -file07
```

### 🔎 Breaking Down the Command

```text
cat -- -file07
│   │  │
│   │  └── File I want to read
│   └───── Stop option processing
└───────── Display file contents
```

- `cat` → Displays the contents of a file.
- `--` → Stops the command from interpreting the next argument as an option.
- `-file07` → The filename.

So:

```bash
cat -- -file07
```

means:

> Display the contents of the file named `-file07`.

---

## 🔑 Step 13 — Get the Password

After running:

```bash
cat -- -file07
```

the terminal displays the password for the next level.

The password is then used to log in as:

```text
bandit5
```

I copied the password from the terminal and used it for the next level.

> ⚠️ I am intentionally not publishing the actual password in this README.

---

## 🖥️ Terminal Screenshot

<img width="1716" height="677" alt="image" src="https://github.com/user-attachments/assets/8befe07e-3100-45be-b217-05587ad4a2e5" />

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

Lists files and directories in the current directory.

---

### `cd`

```bash
cd inhere
```

Changes the current directory.

---

### `cat`

```bash
cat -- -file07
```

Displays the contents of a file.

`cat` does not determine whether the file is readable. It simply outputs the file contents.

---

### `reset`

```bash
reset
```

Resets the terminal when the display becomes messed up, such as after displaying binary data.

---

### `file`

```bash
file -- *
```

Identifies the type of each file.

This was the most important command in this level.

---

### `--`

```text
--
```

Tells many Linux commands to stop processing command-line options.

This is especially useful when filenames begin with:

```text
-
```

For example:

```bash
cat -- -file07
```

---

### `*`

```text
*
```

A wildcard that can match multiple filenames.

For example:

```bash
file -- *
```

checks all matching files in the current directory.

---

### `ASCII text`

```text
ASCII text
```

Indicates that the file contains readable text characters.

In this level, this helped me identify the correct file.

---

## 🧩 Why Each Command Was Used

| Command | Why I Used It |
|---|---|
| `pwd` | To check where I am |
| `ls` | To see files and directories |
| `cd inhere` | To enter the `inhere` directory |
| `cat -- -file00` | To test the contents of a file |
| `reset` | To restore the terminal after binary-looking output |
| `file -- -file00` | To check the type of one file |
| `file -- *` | To check the type of all files |
| `cat -- -file07` | To read the human-readable file |

---

## 🎓 Key Takeaway

The main challenge in this level was **not simply reading a file**.

The challenge was identifying the correct file.

There were 10 files:

```text
-file00
-file01
-file02
-file03
-file04
-file05
-file06
-file07
-file08
-file09
```

I used:

```bash
file -- *
```

to check all of them.

The result showed:

```text
-file07: ASCII text
```

Therefore, `-file07` is the human-readable file.

I then used:

```bash
cat -- -file07
```

to read the password.

---

## 🔄 Complete Command Flow

```text
SSH as bandit4
       ↓
      pwd
       ↓
      ls
       ↓
  cd inhere
       ↓
      ls
       ↓
cat -- -file00
       ↓
 Strange / unreadable output
       ↓
     reset
       ↓
file -- -file00
       ↓
    -file00: data
       ↓
   file -- *
       ↓
Check all 10 file types
       ↓
-file06 → OpenPGP Public Key
-file07 → ASCII text
       ↓
Identify -file07
       ↓
cat -- -file07
       ↓
Password for bandit5
```

---

## 🏁 Final Solution

The important commands for this level are:

```bash
pwd
```

```bash
ls
```

```bash
cd inhere
```

```bash
file -- *
```

```bash
cat -- -file07
```

The key idea I learned is:

> **Use `file` to identify the type of a file before trying to read it.**

And when a filename starts with `-`, using:

```text
--
```

helps tell the command that the next argument is a filename and not an option.

---

## ➡️ Next

The password found in:

```text
-file07
```

is used to continue to:

**Bandit Level 5 → Level 6** 🚀
