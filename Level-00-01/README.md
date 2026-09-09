# 🏴 Bandit Level 0 → Level 1

<img width="1667" height="632" alt="Screenshot 2026-09-09 211256" src="https://github.com/user-attachments/assets/8230f8c8-4423-450c-94e4-af0f4e1f23a0" />


After successfully logging into the Bandit Level 0 server, I started looking for the password required for the next level.

## 📂 Step 1 — Check the Current Directory

I first used:

```bash
pwd
```

### 🔎 What is `pwd`?

`pwd` stands for **Print Working Directory**.

It displays the full path of the directory I am currently working in.

The output was:

```text
/home/bandit0
```

This shows that I am currently inside the `bandit0` user's home directory.

---

## 📋 Step 2 — List the Files

Next, I used:

```bash
ls
```

### 🔎 What is `ls`?

`ls` stands for **list**.

It displays the files and directories in the current directory.

The output showed:

```text
readme
```

This tells me that a file named `readme` exists in the current directory.

---

## 📖 Step 3 — Read the `readme` File

Since I found a file named `readme`, I used:

```bash
cat readme
```

### 🔎 What is `cat`?

`cat` is a Linux command commonly used to display the contents of a file.

In this command:

- `cat` → displays the contents of a file.
- `readme` → the file I want to read.

The command displayed the contents of the `readme` file, which contained the password for the next level.

---

## 🔑 Step 4 — Copy the Password for Level 1

After running:

```bash
cat readme
```

the terminal displayed the password for the next level.

I copied the password from the terminal.

This password is used to authenticate as the `bandit1` user.

> ⚠️ The password is not included here because this is a public GitHub write-up.

---

## 🖥️ Terminal Screenshot

<img width="1717" height="278" alt="Screenshot 2026-09-09 211910" src="https://github.com/user-attachments/assets/1e196669-55df-402b-bf3f-25ec53de56eb" />


---

## 🔐 Step 5 — Connect to Bandit Level 1

Now that I have the password for the next level, I need to log in as `bandit1`.

The username changes from:

```text
bandit0
```

to:

```text
bandit1
```

I use the same Bandit server and SSH port that I learned in Level 0.

The command is:

```bash
ssh bandit1@bandit.labs.overthewire.org -p 2220
```

The server then asks for the password.

I paste the password that I obtained from the `readme` file and press **Enter**.

If the password is correct, I am logged into **Bandit Level 1**.

---

## 🔄 Level 0 → Level 1 Process

```text
Already logged in as bandit0
        ↓
pwd
        ↓
Check current directory
        ↓
ls
        ↓
Find readme
        ↓
cat readme
        ↓
Read the next-level password
        ↓
Copy the password
        ↓
SSH as bandit1
        ↓
Enter the password
        ↓
Level 1
```

## 🧠 What I Learned

- `pwd` shows the current working directory.
- `ls` lists files and directories.
- `cat` displays the contents of a file.
- The `readme` file contained the password for the next level.
- Each Bandit level uses a different username.
- The password found in one level is used to access the next level.

## 🎓 Key Takeaway

The important commands I learned in Level 0 → Level 1 were:

```bash
pwd
ls
cat readme
```

These commands helped me locate and read the file containing the password for the next level.

## ➡️ Next

After obtaining the password, I successfully moved from **Bandit Level 0 to Level 1**.
