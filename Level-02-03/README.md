#🏴 Bandit Level 2 → Level 3

<img width="1396" height="480" alt="image" src="https://github.com/user-attachments/assets/145f8d13-294d-4176-a94e-1d055f94314d" />
 
 ---

##🔐 Step 1 — Connect to Bandit Level 2

Now that I have the password for the next level, I need to log in as bandit2.

The username changes from:
```bash
bandit1
```
to:
```bash
bandit2
```
I use the same Bandit server and SSH port that I learned in the previous levels.

The command is:
```bash
ssh bandit2@bandit.labs.overthewire.org -p 2220
```

After running the command, the server asks me to enter the password:
```bash
bandit2@bandit.labs.overthewire.org's password:
```
##🔑 Step 2 — Enter the Password

I entered the password that I obtained from the previous level (Level 1 → Level 2).
```bash
⚠️ When typing the password in the Linux terminal, the characters are not displayed on the screen. This is normal.
```
After entering the correct password and pressing Enter, I successfully logged in to Bandit Level 2.

The terminal prompt became:
```bash
bandit2@bandit:~$
```
This confirms that I am now logged in as the bandit2 user.

🎯 Goal

The password for the next level is stored in a file called:
```bash
--spaces in this filename--
```
The file is located in the home directory.

The important part of this level is that the filename contains spaces.

📋 Step 1 — Check the Files

<img width="1720" height="97" alt="image" src="https://github.com/user-attachments/assets/c486b2dd-78ff-4c28-abc3-7cc7b7d5bab5" />

First, I used:
```
ls
```
The output showed:
```
--spaces in this filename--
```
This means there is a file in the home directory whose filename contains spaces.

🔎 Step 2 — Why Spaces Cause a Problem

Normally, I can read a file using:
```
cat filename
```
For example:
```
cat readme
```
But this filename contains spaces:
```
--spaces in this filename--
```
If I try:
```
cat --spaces in this filename--
```
- Linux does not treat the entire text as one filename.
- Instead, the shell separates the command into different arguments because of the spaces.
- The filename also begins with `--`, so I use `--` to tell `cat` to stop processing options.
- I use double quotes so the entire filename is treated as one argument.

##🛠️ Step 3 — Use Quotes Around the Filename

I can solve this by putting the filename inside quotation marks:
```
cat -- "--spaces in this filename--"
```
### 🔎 Breaking Down the Command

```text
cat -- "--spaces in this filename--"
│   │   │
│   │   └── The complete filename
│   └───── Stop option processing
└───────── Display the file contents
```

GNU's documentation explains that quoting filenames is useful for filenames containing spaces or other characters that could otherwise be interpreted specially by the shell.

Therefore:
```
cat -- "--spaces in this filename--"
```
means:

Display the contents of the file named --spaces in this filename-- in the current directory.

##🔑 Step 4 — Get the Password for Level 3

After running:
```
cat -- "--spaces in this filename--"
```
the terminal displays the password for Bandit Level 3.

I copied the password from the terminal.

The password is then used to log in as:
```
bandit3
```
🖥️ Terminal Screenshot

<img width="1718" height="142" alt="image" src="https://github.com/user-attachments/assets/4e72eb02-ad14-4103-b69b-88b029f1519c" />

## 🧠 What I Learned

- `ls` → Lists the files and directories in the current directory.
- `Spaces` → Spaces normally separate different arguments in a Linux command.
- `--` → Tells `cat` to stop processing options and treat what follows as a filename.
- `"..."` → Keeps the filename containing spaces as one argument.
- `cat` → Displays the contents of a file.
- `cat -- "--spaces in this filename--"` → Reads the file whose name contains spaces and begins with `--`.
- `Quoting filenames` → Helps Linux correctly handle filenames containing spaces or special characters.
##🎓 Key Takeaway

The important command I learned in this level was:
```
cat -- "--spaces in this filename--"
```
- The quotation marks tell the shell to treat the entire filename, including the spaces, as one argument.

- This is important when working with files that have spaces in their names.

➡️ Next

The password found in the --spaces in this filename-- file is used to continue to:

Bandit Level 3 → Level 4
