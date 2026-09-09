# Bandit Level 0 --> Level 1

<img width="1667" height="632" alt="Screenshot 2026-09-09 211256" src="https://github.com/user-attachments/assets/62c1e47b-1871-44d5-bef6-a6b03da974fc" />

## 📂 Step 3 — Check the Current Directory

After successfully logging into the Bandit server, I first checked my current location using:

```bash
pwd
```

### 🔎 What is `pwd`?

`pwd` stands for **Print Working Directory**.

It shows the full path of the directory I am currently working in.

The output was:

```text
/home/bandit0
```

This tells me that I am currently inside the `bandit0` user's home directory.

---

## 📋 Step 4 — List the Files

Next, I used:

```bash
ls
```

### 🔎 What is `ls`?

`ls` stands for **list**.

It displays the files and directories available in the current directory.

The output was:

```text
readme
```

This tells me that there is a file named `readme` in the current directory.

At this point, I know that the `readme` file may contain useful information for completing the level.

---

## 📖 Step 5 — Read the `readme` File

I used the following command:

```bash
cat readme
```

### 🔎 What is `cat`?

`cat` is a Linux command commonly used to display the contents of a file directly in the terminal.

In this command:

```bash
cat readme
```

- `cat` → displays the contents of a file.
- `readme` → the name of the file I want to read.

The command displayed a message from the Bandit server.

It also provided the password needed for the next level.

---

## 🔑 Step 6 — Copy the Password for Bandit Level 1

After running:

```bash
cat readme
```

the terminal displays the password for the next level.

I copied the password shown after:

```text
The password you are looking for is:
```

This password is needed to log in to **Bandit Level 1**.

### 📋 Copy the Password

I selected the password from the terminal and copied it.

The password is not a new command. It is the **login credential for the next level**.

I then use this password when SSH asks for the password while logging in as `bandit1`.

---

## 🔐 Step 7 — Connect to Bandit Level 1

The username changes from:

```text
bandit0
```

to:

```text
bandit1
```

The server and port remain the same.

I use:

```bash
ssh bandit1@bandit.labs.overthewire.org -p 2220
```

After running the command, the terminal asks:

```text
bandit1@bandit.labs.overthewire.org's password:
```

I paste the password I copied from the `readme` file and press **Enter**.

If the password is correct, I successfully enter **Bandit Level 1**.

### 🔄 The Process

```text
cat readme
      ↓
Password is displayed
      ↓
Copy the password
      ↓
SSH as bandit1
      ↓
Paste the password
      ↓
Enter
      ↓
Bandit Level 1
```

## 🖥️ Terminal Screenshot

<img width="1717" height="278" alt="image" src="https://github.com/user-attachments/assets/cfc905eb-e5c5-414f-9b65-338b837b3b31" />


---

## 🔄 Step 7 — Connect to Bandit Level 1

After obtaining the password, I can connect to the next level using SSH.

The username changes from:

```text
bandit0
```

to:

```text
bandit1
```

The server and port remain the same:

```text
bandit.labs.overthewire.org
```

and:

```text
2220
```

The SSH command is:

```bash
ssh bandit1@bandit.labs.overthewire.org -p 2220
```

When prompted, I enter the password that I obtained from the `readme` file.

---

## 🧠 What I Learned

In Level 0 → Level 1, I learned how to:

- Use `pwd` to find my current directory.
- Use `ls` to list files.
- Identify the `readme` file.
- Use `cat` to read a file.
- Find the password for the next level.
- Use the next level's username with SSH.
- Reuse the same server and port for the next level.

### 🛠️ Commands Used

| Command | Purpose |
|---|---|
| `pwd` | Shows the current working directory |
| `ls` | Lists files and directories |
| `cat readme` | Displays the contents of the `readme` file |
| `ssh bandit1@bandit.labs.overthewire.org -p 2220` | Connects to Level 1 |

## 🎓 Level 0 → Level 1 Summary

```text
Logged in as bandit0
        ↓
pwd
        ↓
Found /home/bandit0
        ↓
ls
        ↓
Found readme
        ↓
cat readme
        ↓
Found the password for Level 1
        ↓
Connect as bandit1
        ↓
Level 1 started
```

## ➡️ Next

Now I can begin **Bandit Level 1 → Level 2**.
