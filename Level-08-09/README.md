# 🏴 Bandit Level 8 → Level 9

<img width="1377" height="463" alt="image" src="https://github.com/user-attachments/assets/3957518b-8142-4836-bc7d-182534b6f961" />


---

## 🎯 Goal

The password for the next level is stored in the file:

```text
data.txt
```

The password is the **only line of text that occurs exactly once**.

The file contains many repeated lines, so I need to find the one line that appears only once. This is the official goal for Level 8 → Level 9. :contentReference[oaicite:0]{index=0}

---

## 🔐 Step 1 — Connect to Bandit Level 8

I connect to the Bandit Level 8 account using SSH.

The command is:

```bash
ssh bandit8@bandit.labs.overthewire.org -p 2220
```

### 🔎 Breaking Down the Command

```text
ssh bandit8@bandit.labs.overthewire.org -p 2220
│   │                                      │  │
│   │                                      │  └── SSH port
│   │                                      └───── Port option
│   └─────────────────────────────────────────── Username + server
└──────────────────────────────────────────────── Secure Shell
```

- `ssh` → Connects to a remote computer.
- `bandit8` → The username for this level.
- `@` → Separates the username from the server.
- `bandit.labs.overthewire.org` → The Bandit server.
- `-p` → Specifies the SSH port.
- `2220` → The port used by the Bandit game.

After running the command, the server asks:

```text
bandit8@bandit.labs.overthewire.org's password:
```

I enter the password obtained from **Level 7 → Level 8**.

> ⚠️ When typing a password in Linux, the characters are not displayed. This is normal.

After successful login, the prompt becomes:

```text
bandit8@bandit:~$
```

This confirms that I am logged in as:

```text
bandit8
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
/home/bandit8
```

So I am currently inside:

```text
/home/bandit8
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

The level says that the password is:

> The only line of text that occurs only once.

So `data.txt` contains many lines.

Most of the lines appear multiple times, but one line appears only once.

I need to identify that unique line.

---

## 👀 Step 5 — Check the File

I can use:

```bash
cat data.txt
```

This displays the contents of the file.

However, the file contains many lines, so it is difficult to manually find the one line that appears only once.

Instead, I can use the `sort` and `uniq` commands.

---

# 🔤 Step 6 — Sort the File

I used:

```bash
sort data.txt
```

### 🔎 What does `sort` do?

```bash
sort data.txt
```

sorts the lines in `data.txt`.

For example, if the file contains:

```text
apple
banana
apple
orange
banana
```

after sorting:

```text
apple
apple
banana
banana
orange
```

The duplicate lines are now next to each other.

This is important because `uniq` works with **adjacent duplicate lines**.

---

# 🔗 Step 7 — Use a Pipe

Instead of saving the sorted output to another file, I can send it directly to another command.

I use the pipe symbol:

```text
|
```

The pipe connects the output of one command to the input of another command.

For example:

```bash
sort data.txt | uniq
```

means:

```text
sort data.txt
      ↓
    output
      ↓
      |
      ↓
    uniq
      ↓
   result
```

---

# 🔎 Step 8 — Use `uniq`

The command I use is:

```bash
sort data.txt | uniq -u
```

This is the main solution for this level. :contentReference[oaicite:1]{index=1}

---

## 🧩 Breaking Down the Command

```text
sort data.txt | uniq -u
│            │  │    │
│            │  │    └── Show only unique lines
│            │  └─────── Remove duplicate lines
│            └─────────── Pipe
└──────────────────────── Sort the file
```

---

## 🔤 `sort data.txt`

```bash
sort data.txt
```

This sorts all the lines in `data.txt`.

Why?

Because duplicate lines need to be next to each other before `uniq` can identify them correctly.

---

## 🔗 `|`

```text
|
```

The pipe sends the output of:

```bash
sort data.txt
```

directly into:

```bash
uniq -u
```

So I don't need to create another file.

---

## 🧹 `uniq`

```bash
uniq
```

`uniq` is used to filter repeated lines.

It works with adjacent duplicate lines.

That's why I use `sort` first.

---

## ⭐ `-u`

```bash
uniq -u
```

The `-u` option means:

```text
unique
```

It tells `uniq` to display only lines that occur exactly once.

Therefore:

```bash
sort data.txt | uniq -u
```

means:

> Sort all the lines, group identical lines together, and display only the line that appears exactly once.

---

# 🧪 Step 9 — Run the Complete Command

I run:

```bash
sort data.txt | uniq -u
```

The command returns one line.

That line is the password for the next level.

> ⚠️ I do not publish the actual password in this GitHub README.

---

# 🤔 Why Can't I Just Use `uniq -u data.txt`?

I should not rely on:

```bash
uniq -u data.txt
```

because `uniq` checks **adjacent** duplicate lines.

If identical lines are separated by other lines, `uniq` may not recognize them as duplicates.

For example:

```text
apple
banana
apple
```

The two `apple` lines are not adjacent.

After using:

```bash
sort
```

the lines become:

```text
apple
apple
banana
```

Now `uniq` can correctly identify the duplicates.

Therefore, the important combination is:

```bash
sort data.txt | uniq -u
```

---

# 🔑 Step 10 — Get the Password for Level 9

The output from:

```bash
sort data.txt | uniq -u
```

is the only line that occurs once.

Therefore, that line is the password for:

```text
bandit9
```

I copy the password and use it to log in to the next level.

---

# 🖥️ Terminal Screenshot
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/fe16c635-3536-49f7-b0bf-ded1d0ae168b" />

<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/5797adb2-c158-4fe6-852f-723f0f4ebeae" />


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

### `cat`

```bash
cat data.txt
```

Displays the contents of `data.txt`.

---

### `sort`

```bash
sort data.txt
```

Sorts the lines of a file.

---

### `|`

```text
|
```

The pipe sends the output of one command into another command.

---

### `uniq`

```bash
uniq
```

Filters repeated adjacent lines.

---

### `uniq -u`

```bash
uniq -u
```

Displays only lines that occur exactly once.

---

# 🧩 Why Each Command Was Used

| Command | Why I Used It |
|---|---|
| `pwd` | To check my current location |
| `ls` | To see the available files |
| `cat data.txt` | To view the contents of the file |
| `sort data.txt` | To sort the lines and group duplicates |
| `\|` | To send the output to another command |
| `uniq` | To filter duplicate lines |
| `uniq -u` | To display only the line that occurs once |

---

# 🎓 Key Takeaway

This level taught me how to find a unique line inside a file containing many repeated lines.

The important command is:

```bash
sort data.txt | uniq -u
```

First:

```bash
sort data.txt
```

sorts the lines so identical lines are next to each other.

Then:

```bash
uniq -u
```

shows only the line that occurs exactly once.

The pipe:

```text
|
```

connects the two commands.

So the complete process is:

```text
data.txt
   ↓
sort
   ↓
Repeated lines are grouped
   ↓
uniq -u
   ↓
Only line occurring once
   ↓
Password for bandit9
```

The main thing I learned is:

> **`sort` + `uniq -u` can be used to find a line that occurs only once.**

---

# 🔄 Complete Command Flow

```text
SSH as bandit8
       ↓
      pwd
       ↓
      ls
       ↓
   data.txt
       ↓
sort data.txt
       ↓
Sort all lines
       ↓
      |
       ↓
   uniq -u
       ↓
Show only the line occurring once
       ↓
Password for bandit9
```

---

# 🏁 Final Solution

The main command that solves this level is:

```bash
sort data.txt | uniq -u
```

### Command 1

```bash
sort data.txt
```

Sorts all lines in the file.

### Command 2

```bash
uniq -u
```

Displays only the line that occurs exactly once.

### Combined

```bash
sort data.txt | uniq -u
```

This gives the password for:

```text
bandit9
```

---

## ➡️ Next

**Bandit Level 9 → Level 10** 🚀
