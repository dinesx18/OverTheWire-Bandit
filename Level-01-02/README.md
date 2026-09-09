# 🏴 Bandit Level 1 → Level 2

<img width="1592" height="526" alt="Screenshot 2026-09-09 214354" src="https://github.com/user-attachments/assets/b5d56b55-39e0-4eef-b8f8-06c68035be8a" />

## 🔐 Step 1 — Connect to Bandit Level 1

I connected to the Bandit Level 1 account using:

```bash
ssh bandit1@bandit.labs.overthewire.org -p 2220
```

After running the command, the server asked me to enter the password:
```bash
bandit1@bandit.labs.overthewire.org's password:
```

## 🔑 Step 2 — Enter the Password

I entered the password that I obtained from the previous level (Level 0 → Level 1).

⚠️ When typing the password in the Linux terminal, the characters are not displayed on the screen. This is normal and is a security feature.

After entering the correct password and pressing Enter, I successfully logged in to Bandit Level 1.

The terminal prompt became:
```bash
bandit1@bandit:~$
```

This confirms that I am now logged in as the bandit1 user.


## 🎯 Goal

The password for the next level is stored in a file called `-` located in the home directory.

After completing Level 0, I logged into Bandit Level 1 using the password I found in the previous level.

---

## 📋 Step 1 — Check the Files

<img width="1722" height="110" alt="image" src="https://github.com/user-attachments/assets/ee55aa03-12e1-4769-a7d3-f136d6023d43" />


I first used:

```bash
ls
```

The output showed:

```text
-
```

This means there is a file in the home directory whose filename is simply:

```text
-
```

---

## 🔎 Step 2 — Why `cat -` Is Different

<img width="1722" height="112" alt="image" src="https://github.com/user-attachments/assets/6f5cea05-2e94-4584-8a28-d51bde41b1e9" />


Normally, I can read a file using:

```bash
cat filename
```

For example:

```bash
cat readme
```

But this level has a special filename:

```text
-
```

If I run:

```bash
cat -
```

`cat` interprets `-` as standard input rather than treating it as the name of the file.

So `cat -` is **not the correct way to read this file**.

---

## 🛠️ Step 3 — Read the File Using `./`

<img width="1717" height="67" alt="image" src="https://github.com/user-attachments/assets/2ec2c4d5-f0d8-4565-9b2c-c7a3b3c54f88" />

---

To tell Linux that `-` is a filename in the current directory, I use:

```bash
cat ./-
```

### 🔎 Breaking Down the Command

```text
cat ./-
│   │
│   └── File named "-" in the current directory
└────── Display the file contents
```

- `cat` → Displays the contents of a file.
- `./` → Means the current directory.
- `-` → The actual filename.

Therefore:

```bash
cat ./-
```

means:

> Display the contents of the file named `-` located in the current directory.

---

## 🔑 Step 4 — Get the Password for Level 2

After running:

```bash
cat ./-
```

the terminal displays the password for **Bandit Level 2**.

I copied the password from the terminal.

The password is then used to log in as:

```text
bandit2
```

---

## 🖥️ Terminal Screenshot

<img width="1717" height="158" alt="image" src="https://github.com/user-attachments/assets/686b192f-0ae4-4353-8664-d4048b17f72e" />



## 🧠 What I Learned

1. `ls` → Lists the files and directories in the current directory.
2. `-` → Can be used as a special character by Linux commands, often representing standard input or output.
3. `cat -` → Causes `cat` to read from standard input instead of treating `-` as a normal filename.
4. `./` → Represents the current directory.
5. `cat ./-` → Reads a file whose filename is `-` from the current directory.
6. `cat` → Displays the contents of a file.
7. Special filenames → Some filenames can have characters that have special meanings to Linux commands.

## 🎓 Key Takeaway

The important command I learned in this level was:

```bash
cat ./-
```

Using `./` tells Linux that `-` is the name of a file in the current directory.

## ➡️ Next

The password found in the `-` file is used to continue to **Bandit Level 2-3**.
