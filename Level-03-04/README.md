# 🏴 Bandit Level 3 → Level 4

<img width="1407" height="355" alt="image" src="https://github.com/user-attachments/assets/b85d4672-f007-4404-bf07-2101272e285d" />


---

## 🔐 Step 1 — Connect to Bandit Level 3

Now that I have the password for the next level, I need to log in as `bandit3`.

The username changes from:

```text
bandit2
```
to:
```
bandit3
```

I use the same Bandit server and SSH port that I learned in the previous levels.

The command is:
```
ssh bandit3@bandit.labs.overthewire.org -p 2220
```
After running the command, the server asks me to enter the password:
```
bandit3@bandit.labs.overthewire.org's password:
```
## 🔑 Step 2 — Enter the Password

I entered the password that I obtained from the previous level (Level 2 → Level 3).
```
⚠️ When typing the password in the Linux terminal, the characters are not displayed on the screen. This is normal.
```
After entering the correct password and pressing Enter, I successfully logged in to Bandit Level 3.

The terminal prompt became:
```
bandit3@bandit:~$
```
This confirms that I am now logged in as the bandit3 user.

## 🎯 Goal

- The password for the next level is stored in a hidden file inside the inhere directory.
- The important part of this level is finding and reading the hidden file.

## 📋 Step 1 — Check the Files

<img width="1717" height="167" alt="image" src="https://github.com/user-attachments/assets/99205908-9661-4b41-af92-973b90e0d66b" />


First, I used:
```
ls
```
The output showed:
```
inhere
```
This means there is a directory called:
```
inhere
```
in the home directory.

## 📂 Step 2 — Enter the inhere Directory

I used:
```
cd inhere
```
## 🔎 Breaking Down the Command
```
cd inhere
│  │
│  └── Directory I want to enter
└───── Change directory
```
- cd → Changes the current directory.
- inhere → The directory I want to enter.

After running the command, I am inside the inhere directory.

🔎 Breaking Down the Prompt:
```
bandit3@bandit:~/inhere$
│       │       │       │
│       │       │       └── `$` means the shell is ready for a command
│       │       └────────── Current directory: `inhere`
│       └────────────────── Hostname: `bandit`
└────────────────────────── Username: `bandit3`
```
bandit3 → The user I am currently logged in as.
@ → Separates the username from the hostname.
bandit → The hostname of the Bandit server.
: → Separates the hostname from the current directory.
~/inhere → I am inside the inhere directory in the user's home directory.
$ → Indicates that the terminal is ready to accept a command.

## 🔎 Step 3 — Check for Hidden Files

<img width="358" height="62" alt="image" src="https://github.com/user-attachments/assets/b6ad4b2f-4d4a-48b5-b1e7-8a693c3948b8" />

I used:

```bash
ls
```
The terminal showed:
```
bandit3@bandit:~/inhere$
```
This is because normal ls does not show hidden files.

So I used:
```
ls -la
```
or
```
ll
```
### 🔎 Breaking Down the Command
```
ls -la
│  │
│  └── Show detailed information and hidden files
└───── List directory contents
ls → Lists files and directories.
-l → Shows detailed information about the files.
-a → Shows all files, including hidden files.

ll
│
└── Shortcut/alias for an ls command
    └── Can show detailed information
        └── On your system, it also shows hidden files
```
<img width="1712" height="242" alt="image" src="https://github.com/user-attachments/assets/110b0431-e320-47f2-882f-608a90a25d76" />

The output showed a hidden file:
```
total 12
drwxr-xr-x 2 root    root    4096 Jun 24 14:59 ./
drwxr-xr-x 3 root    root    4096 Jun 24 14:59 ../
-rw-r----- 1 bandit4 bandit3   33 Jun 24 14:59 ...Hiding-From-You

```
### 🕵️ Step 4 — Identify the Hidden File

The file is:
```
...Hiding-From-You
```
- The filename starts with a dot (.).

- In Linux, files beginning with . are normally hidden.

- That is why the file did not appear when I used:
```
ls
```
I needed to use:
```
ls -la
```
or 
```
ll
```
to see it.

### 📖 Step 5 — Read the Hidden File

Now that I found the hidden file, I used:
```
cat ...Hiding-From-You
```
🔎 Breaking Down the Command
```
cat ...Hiding-From-You
│   │
│   └── Hidden file to read
└────── Display the file contents
```
cat → Displays the contents of a file.
...Hiding-From-You → The hidden file containing the password.

The command displays the password for Bandit Level 4.

## 🔑 Step 6 — Get the Password for Level 4

After running:
```
cat ...Hiding-From-You
```
- the terminal displays the password for Bandit Level 4.
- I copied the password from the terminal.
- The password is then used to log in as:
```
bandit4
```
## 🖥️ Terminal Screenshot

<img width="1717" height="352" alt="image" src="https://github.com/user-attachments/assets/4a0f5d57-4b41-4846-8979-42649fe886f7" />


## 🧠 What I Learned
- `ls` → Lists the files and directories in the current directory.
- `cd` → Changes the current directory.
- `cd inhere` → Enters the inhere directory.
- `ls -la or ll` → Shows all files, including hidden files, with detailed information.
- `-a` → Shows hidden files.
- `...Hiding-From-You` → The hidden file containing the password.
- `cat` → Displays the contents of a file.
- `cat ...Hiding-From-You` → Reads the hidden file.
- Hidden files → Files beginning with `.` are normally not shown by a normal `ls` command.
## 🎓 Key Takeaway

The important commands I learned in this level were:
```
cd inhere
ls -la
cat ...Hiding-From-You
```
The -a option in ls -la allows me to see hidden files that are not normally displayed.

The password is stored inside the ...Hiding-From-You file.

## ➡️ Next

The password found in the ...Hiding-From-You file is used to continue to:

Bandit Level 4 → Level 5


### ✅ Your Level 03 → 04 flow

```text
SSH as bandit3
       ↓
      ls
       ↓
  cd inhere
       ↓
      ls
       ↓
    ls -la
       ↓
   find ...Hiding-From-You
       ↓
  cat ...Hiding-From-You
       ↓
Password for bandit4
```
