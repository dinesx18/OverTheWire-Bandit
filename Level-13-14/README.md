# 🏴 Bandit Level 13 → Level 14

<img width="1606" height="595" alt="image" src="https://github.com/user-attachments/assets/bfc4c60e-c0ac-4a99-b628-47bd74c19968" />


---

## 🎯 Goal

The password for the next level is stored in:

```text
/etc/bandit_pass/bandit14
```

However, this file can only be read by the user:

```text
bandit14
```

For this level, we are **not given the password directly**.

Instead, the home directory contains a **private SSH key** that can be used to log in to the next level.

The main task is to:

1. Log in to `bandit13`.
2. Find the private SSH key in the home directory.
3. Use the private key to log in as `bandit14`.
4. Read the password from `/etc/bandit_pass/bandit14`.

---

## 🔐 Step 1 — Connect to Bandit Level 13

First, connect to the Bandit Level 13 account using SSH.

```bash
ssh bandit13@bandit.labs.overthewire.org -p 2220
```

### Command Breakdown

```text
ssh
```

Used to securely connect to a remote computer.

```text
bandit13
```

The username for Level 13.

```text
@
```

Separates the username from the hostname.

```text
bandit.labs.overthewire.org
```

The hostname of the OverTheWire Bandit server.

```text
-p 2220
```

Specifies SSH port `2220`.

---

## 🔑 Step 2 — Enter the Password

After running the SSH command, the terminal asks for the password.

```text
bandit13@bandit.labs.overthewire.org's password:
```

Enter the password obtained from:

```text
Bandit Level 12 → Level 13
```

> ⚠️ The password is intentionally not included in this GitHub writeup.

If the password is correct, you will successfully log in as:

```text
bandit13
```

---

## 📍 Step 3 — Check the Current Directory

Run:

```bash
pwd
```

### What does `pwd` do?

`pwd` means:

```text
Print Working Directory
```

It shows the directory where you are currently working.

You should see:

```text
/home/bandit13
```

---

## 📋 Step 4 — List the Files

Run:

```bash
ls
```

You should see a file similar to:

```text
sshkey.private
```

This is the **private SSH key** provided for this level.

---

## 🔍 Step 5 — Check the Private Key

Run:

```bash
file sshkey.private
```

The output should identify it as a private key.

You can also inspect the beginning of the key with:

```bash
head sshkey.private
```

You should see something similar to:

```text
-----BEGIN RSA PRIVATE KEY-----
```

The exact key contents should **not** be published in your GitHub repository.

---

## 🔐 Step 6 — Understand the Private SSH Key

A private SSH key can be used to authenticate to an SSH server without entering a password.

Instead of:

```bash
ssh username@server
```

we can specify a private key using:

```bash
ssh -i private_key username@server
```

The:

```text
-i
```

option tells SSH which private key to use.

---

## 🔑 Step 7 — Use the Private Key

We need to use the private key to log in as:

```text
bandit14
```

Run:

```bash
ssh -i sshkey.private bandit14@localhost -p 2220
```

### Command Breakdown

```text
ssh
```

Starts an SSH connection.

```text
-i sshkey.private
```

Tells SSH to use `sshkey.private` as the identity/private key.

```text
bandit14
```

The username we want to log in as.

```text
@
```

Separates the username from the hostname.

```text
localhost
```

Means the current machine.

The Bandit levels are running on the same server, so we can connect to the next account through `localhost`.

```text
-p 2220
```

Uses SSH port `2220`.

---

## 🖥️ Step 8 — Connect to Bandit Level 14

Run:

```bash
ssh -i sshkey.private bandit14@localhost -p 2220
```

If everything is correct, SSH will authenticate using the private key.

You should now be logged in as:

```text
bandit14
```

You can verify this using:

```bash
whoami
```

The output should be:

```text
bandit14
```

---

## 🔍 Step 9 — Read the Password File

The level tells us that the password is stored in:

```text
/etc/bandit_pass/bandit14
```

Now that we are logged in as `bandit14`, we can read the file.

Run:

```bash
cat /etc/bandit_pass/bandit14
```

### What does `cat` do?

```text
cat
```

displays the contents of a file in the terminal.

The command:

```bash
cat /etc/bandit_pass/bandit14
```

reads the password file for Level 14.

The output is the password needed for:

```text
bandit14
```

> 🔐 Do not publish the actual password in your GitHub repository.

---

# 🖥️ Complete Command Sequence

## Connect to Level 13

```bash
ssh bandit13@bandit.labs.overthewire.org -p 2220
```

## Check the directory

```bash
pwd
```

## List the files

```bash
ls
```

## Check the private key

```bash
file sshkey.private
```

## View the beginning of the key

```bash
head sshkey.private
```

## Use the private key to log in to Level 14

```bash
ssh -i sshkey.private bandit14@localhost -p 2220
```

## Verify the current user

```bash
whoami
```

## Read the Level 14 password

```bash
cat /etc/bandit_pass/bandit14
```

---

# 🧩 Command Breakdown

## `ssh`

```bash
ssh bandit13@bandit.labs.overthewire.org -p 2220
```

Connects to the Bandit server using SSH.

---

## `pwd`

```bash
pwd
```

Shows the current working directory.

---

## `ls`

```bash
ls
```

Lists the files in the current directory.

---

## `file`

```bash
file sshkey.private
```

Identifies the type of the private key file.

---

## `head`

```bash
head sshkey.private
```

Displays the beginning of the private key file.

It can be useful for confirming that the file contains an SSH private key.

---

## `ssh -i`

```bash
ssh -i sshkey.private bandit14@localhost -p 2220
```

Uses the specified private key to authenticate to the SSH server.

The important part is:

```text
-i sshkey.private
```

which tells SSH to use the private key.

---

## `whoami`

```bash
whoami
```

Displays the username of the current user.

Example:

```text
bandit14
```

---

## `cat`

```bash
cat /etc/bandit_pass/bandit14
```

Displays the contents of the password file.

---

# 🔐 How SSH Key Authentication Works

Normally, we connect using a username and password:

```text
Username
    +
Password
    ↓
SSH Server
    ↓
Login
```

In this level, we use a private SSH key instead:

```text
Private SSH Key
       ↓
SSH Authentication
       ↓
bandit14
       ↓
Login
```

The private key replaces the need to enter the Bandit password directly.

---

# 🧠 What I Learned

## 1. SSH Private Keys

A private SSH key can be used to authenticate to an SSH server.

Example:

```bash
ssh -i sshkey.private user@server
```

---

## 2. The `-i` Option

The `-i` option specifies the private key that SSH should use.

Example:

```bash
ssh -i sshkey.private bandit14@localhost -p 2220
```

Here:

```text
-i
```

means use an identity/private key.

```text
sshkey.private
```

is the private key file.

---

## 3. `localhost`

`localhost` refers to the current machine.

In this level, we use:

```bash
bandit14@localhost
```

because the next Bandit account is on the same server.

---

## 4. SSH Key Authentication

SSH supports authentication using cryptographic keys.

The private key is kept secret and is used to prove that we are authorized to access the account.

---

## 5. `whoami`

The `whoami` command tells us which user account we are currently using.

Example:

```bash
whoami
```

Output:

```text
bandit14
```

---

## 6. Password Files

Bandit stores level passwords in:

```text
/etc/bandit_pass/
```

For this level, the required password file is:

```text
/etc/bandit_pass/bandit14
```

---

# 🧩 Why Each Command Was Used

| Command | Purpose |
| ------- | ------- |
| `ssh` | Connect to the Bandit server |
| `pwd` | Show the current directory |
| `ls` | List files |
| `file` | Identify the private key file |
| `head` | Display the beginning of the key |
| `ssh -i` | Authenticate using the private SSH key |
| `whoami` | Check the current username |
| `cat` | Read the password file |

---

# 🔄 Complete Process

```text
Bandit Level 13
       ↓
      ssh
       ↓
Login using bandit13 password
       ↓
      ls
       ↓
sshkey.private
       ↓
Private SSH Key
       ↓
ssh -i sshkey.private
       ↓
bandit14@localhost
       ↓
Bandit Level 14
       ↓
cat /etc/bandit_pass/bandit14
       ↓
Password for Bandit Level 14 🔓
```

---

# 🏁 Final Solution

The important command for this level is:

```bash
ssh -i sshkey.private bandit14@localhost -p 2220
```

After successfully logging in as `bandit14`, read the password using:

```bash
cat /etc/bandit_pass/bandit14
```

The output is the password needed for the next level.

---

# ➡️ Next Level

After getting the password, you can connect to **Bandit Level 14** using the normal Bandit server connection:

```bash
ssh bandit14@bandit.labs.overthewire.org -p 2220
```

Enter the password obtained from:

```text
/etc/bandit_pass/bandit14
```

---

## 📚 Commands Practiced

```bash
ssh
pwd
ls
file
head
whoami
cat
```

---

# ⭐ Level Completed

```text
Bandit Level 13
       ↓
   sshkey.private
       ↓
 Private SSH Key
       ↓
ssh -i sshkey.private
       ↓
   bandit14
       ↓
cat /etc/bandit_pass/bandit14
       ↓
Bandit Level 14 🔓
```
