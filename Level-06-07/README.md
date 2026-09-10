# 🏴 Bandit Level 6 → Level 7

<img width="1387" height="457" alt="image" src="https://github.com/user-attachments/assets/6e069e39-980e-4d62-bd18-80c7ebfc6f1b" />

---

## 🎯 Goal

The password for the next level is stored somewhere on the server.

The file has these conditions:

- It is owned by the user `bandit7`.
- It belongs to the group `bandit6`.
- It is exactly **33 bytes** in size.

So I need to search the entire server for a file that matches all three conditions.

---

## 🔐 Step 1 — Connect to Bandit Level 6

I connect to the Bandit Level 6 account using SSH.

The command is:

```bash
ssh bandit6@bandit.labs.overthewire.org -p 2220
```

### 🔎 Breaking Down the Command

```text
ssh bandit6@bandit.labs.overthewire.org -p 2220
│   │                                      │  │
│   │                                      │  └── SSH port
│   │                                      └───── Port option
│   └─────────────────────────────────────────── Username + server
└──────────────────────────────────────────────── Secure Shell
```

- `ssh` → Connects to a remote computer.
- `bandit6` → The username for this level.
- `@` → Separates the username from the server.
- `bandit.labs.overthewire.org` → The Bandit server.
- `-p` → Specifies the SSH port.
- `2220` → The port used by the Bandit game.

After running the command, the server asks:

```text
bandit6@bandit.labs.overthewire.org's password:
```

I enter the password obtained from **Level 5 → Level 6**.

> ⚠️ When typing a password in Linux, the characters are not displayed. This is normal.

After successful login, the prompt becomes:

```text
bandit6@bandit:~$
```

This confirms that I am logged in as:

```text
bandit6
```

---

## 📍 Step 2 — Check My Current Location

<img width="1716" height="223" alt="image" src="https://github.com/user-attachments/assets/b34a2cec-e616-46ec-ac0a-da8aa0b3ebb7" />

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

The output is:

```text
/home/bandit6
```

So I am currently inside:

```text
/home/bandit6
```

---

## 📋 Step 3 — Check the Files

I used:

```bash
ls
```

This shows the files and directories in my current location.

However, the goal says that the password file is located:

```text
somewhere on the server
```

So the file may not be inside my home directory.

Therefore, I need to search from the root of the filesystem.

---

# 🔎 Step 4 — Search the Entire Server

The main command is:

```bash
find / -user bandit7 -group bandit6 -size 33c
```

This searches the entire server for a file matching the required conditions.

---

## 🧩 Breaking Down the Command

```text
find / -user bandit7 -group bandit6 -size 33c
│    │  │              │              │
│    │  │              │              └── Exactly 33 bytes
│    │  │              └───────────────── Group must be bandit6
│    │  └──────────────────────────────── Owner must be bandit7
│    └─────────────────────────────────── Search from root
└──────────────────────────────────────── Search command
```

---

## 🔍 `find`

```bash
find
```

The `find` command searches for files and directories.

It can search using properties such as:

- Owner
- Group
- Size
- Name
- Permissions
- File type

---

## 🌳 `/`

```text
/
```

The `/` represents the **root directory**.

So:

```bash
find /
```

means:

> Search starting from the root of the filesystem.

This allows the command to search across the entire server.

---

## 👤 `-user bandit7`

```bash
-user bandit7
```

This tells `find` to search for files owned by:

```text
bandit7
```

So the owner must be:

```text
bandit7
```

---

## 👥 `-group bandit6`

```bash
-group bandit6
```

This tells `find` to search for files belonging to the group:

```text
bandit6
```

So the group must be:

```text
bandit6
```

---

## 📏 `-size 33c`

```bash
-size 33c
```

This searches for a file that is exactly:

```text
33 bytes
```

The `c` means:

```text
bytes
```

Therefore:

```bash
-size 33c
```

means:

> Find a file that is exactly 33 bytes.

---

# ⚠️ Step 5 — Run the Command Without `2>/dev/null`

First, I tried the command without hiding errors:

```bash
find / -user bandit7 -group bandit6 -size 33c
```

Because I am searching the entire server, some directories are protected and I do not have permission to read them.

Therefore, the terminal may display messages such as:

```text
find: '/root': Permission denied
find: '/proc/...': Permission denied
find: '/sys/...': Permission denied
```

<img width="832" height="908" alt="Screenshot 2026-09-10 194431" src="https://github.com/user-attachments/assets/1da2887b-4c5f-4ade-aa6f-2f90311c4733" />
<img width="683" height="833" alt="Screenshot 2026-09-10 194453" src="https://github.com/user-attachments/assets/228678b3-f12f-45bf-beae-524b2b53fec4" />



These errors are normal.

They do not mean that the command failed.

The `find` command is still searching the directories that I am allowed to access.

Eventually, the correct file is found:

```text
/var/lib/dpkg/info/bandit7.password
```

---

# 🧹 Step 6 — Use `2>/dev/null`

The permission errors make the output difficult to read.

So I can run the same command with:

```bash
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

Now the permission error messages are hidden.

The result is easier to see:

```text
/var/lib/dpkg/info/bandit7.password
```


---

## 🔎 What Does `2>/dev/null` Mean?

```text
2
↓
Standard Error
↓
>
Redirect
↓
/dev/null
↓
Discard the output
```

So:

```bash
2>/dev/null
```

means:

> Send error messages to `/dev/null`, where they are discarded.

### Important

It does **not** change the search.

It only hides the error messages.

Both commands search for the same file:

### Without hiding errors

```bash
find / -user bandit7 -group bandit6 -size 33c
```

### With errors hidden

```bash
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

The second command simply gives cleaner output.

---

# 🎯 Step 7 — Find the Correct File

The search gives:

```text
/var/lib/dpkg/info/bandit7.password
```

This file matches all three conditions:

```text
Owner  → bandit7
Group  → bandit6
Size   → 33 bytes
```

Therefore, this is the file containing the password.

---

# 📂 Step 8 — Understand the File Path

The path is:

```text
/var/lib/dpkg/info/bandit7.password
```

Breaking it down:

```text
/
│
├── var
│
├── lib
│
├── dpkg
│
├── info
│
└── bandit7.password
```

The filename is:

```text
bandit7.password
```

and it is located inside:

```text
/var/lib/dpkg/info/
```

---

# 📖 Step 9 — Read the File

Now that I found the correct file, I use:

```bash
cat /var/lib/dpkg/info/bandit7.password
```

### 🔎 Breaking Down the Command

```text
cat /var/lib/dpkg/info/bandit7.password
│   │
│   └── Full path to the password file
└────── Display the file contents
```

- `cat` → Displays the contents of a file.
- `/var/lib/dpkg/info/bandit7.password` → The full path to the file.

The command displays the password for the next level.

---

# 🔑 Step 10 — Get the Password for Level 7

After running:

```bash
cat /var/lib/dpkg/info/bandit7.password
```

the terminal displays the password for:

```text
bandit7
```

I copy the password and use it to log in to the next level.

> ⚠️ I am intentionally not publishing the actual password in this GitHub README.

---

# 🖥️ Terminal Screenshot

<img width="1716" height="112" alt="image" src="https://github.com/user-attachments/assets/23d22ace-441c-4f07-87f4-5233908069e5" />

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

### `find`

```bash
find /
```

Searches for files and directories starting from the root directory.

---

### `-user`

```bash
-user bandit7
```

Searches for files owned by the user `bandit7`.

---

### `-group`

```bash
-group bandit6
```

Searches for files belonging to the group `bandit6`.

---

### `-size`

```bash
-size 33c
```

Searches for a file that is exactly 33 bytes.

---

### `2>/dev/null`

```bash
2>/dev/null
```

Hides error messages such as permission errors.

---

### `cat`

```bash
cat /var/lib/dpkg/info/bandit7.password
```

Displays the contents of the password file.

---

# 🧩 Why Each Command Was Used

| Command | Why I Used It |
|---|---|
| `pwd` | To check my current location |
| `ls` | To see files and directories |
| `find /` | To search the entire server |
| `-user bandit7` | To find a file owned by `bandit7` |
| `-group bandit6` | To find a file belonging to group `bandit6` |
| `-size 33c` | To find a file exactly 33 bytes |
| `2>/dev/null` | To hide permission error messages |
| `cat` | To read the password file |

---

# 🎓 Key Takeaway

This level taught me how to use `find` with multiple conditions.

The important command is:

```bash
find / -user bandit7 -group bandit6 -size 33c
```

This searches the entire server for a file that satisfies:

```text
Owner  → bandit7
Group  → bandit6
Size   → 33 bytes
```

The search finds:

```text
/var/lib/dpkg/info/bandit7.password
```

I can also use:

```bash
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

to hide permission errors and make the output cleaner.

Then I use:

```bash
cat /var/lib/dpkg/info/bandit7.password
```

to read the password.

The main thing I learned is:

> **`find` can search the entire filesystem using multiple conditions at the same time.**

---

# 🔄 Complete Command Flow

```text
SSH as bandit6
       ↓
      pwd
       ↓
      ls
       ↓
Search entire server
       ↓
find / -user bandit7 -group bandit6 -size 33c
       ↓
Permission denied messages
       ↓
Use 2>/dev/null
       ↓
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
       ↓
/var/lib/dpkg/info/bandit7.password
       ↓
cat /var/lib/dpkg/info/bandit7.password
       ↓
Password for bandit7
```

---

# 🏁 Final Solution

### Search without hiding errors:

```bash
find / -user bandit7 -group bandit6 -size 33c
```

### Search while hiding permission errors:

```bash
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

### Read the password:

```bash
cat /var/lib/dpkg/info/bandit7.password
```

---

## ➡️ Next

**Bandit Level 7 → Level 8** 🚀
