# 🏴 Bandit Level 14 → Level 15

<img width="1271" height="635" alt="image" src="https://github.com/user-attachments/assets/b1264896-b859-471b-82c6-66b84649311d" />


---

## 🎯 Goal

The password for the next level can be retrieved by submitting the password of the current level to:

```text
port 30000 on localhost
```

For this level, we need to:

1. Connect to Bandit Level 14.
2. Use the current Level 14 password.
3. Connect to port `30000` on `localhost`.
4. Submit the current password to the service.
5. Receive the password for **Bandit Level 15**.

---

## 🔐 Step 1 — Connect to Bandit Level 14

First, connect to the Bandit Level 14 account using SSH.

```bash
ssh bandit14@bandit.labs.overthewire.org -p 2220
```

### Command Breakdown

```text
ssh
```

Used to securely connect to a remote computer.

```text
bandit14
```

The username for Level 14.

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
bandit14@bandit.labs.overthewire.org's password:
```

Enter the password obtained from:

```text
Bandit Level 13 → Level 14
```

> ⚠️ The password is intentionally not included in this GitHub writeup.

If the password is correct, you will successfully log in as:

```text
bandit14
```

---

## 📍 Step 3 — Check the Current User

Run:

```bash
whoami
```

The output should be:

```text
bandit14
```

### What does `whoami` do?

```text
whoami
```

Displays the username of the current user.

This confirms that we are logged in as:

```text
bandit14
```

---

## 📋 Step 4 — Check the Current Directory

Run:

```bash
pwd
```

The output should be similar to:

```text
/home/bandit14
```

### What does `pwd` do?

`pwd` means:

```text
Print Working Directory
```

It shows the directory where we are currently working.

---

## 🌐 Step 5 — Understand `localhost`

The level tells us to connect to:

```text
localhost
```

### What is `localhost`?

`localhost` refers to the same computer on which the command is being executed.

It usually resolves to:

```text
127.0.0.1
```

So:

```text
localhost
```

and:

```text
127.0.0.1
```

refer to the local machine.

---

## 🔢 Step 6 — Understand Port 30000

The level tells us that the service is running on:

```text
port 30000
```

A **port** identifies a network service running on a computer.

For example:

```text
localhost:30000
```

means:

```text
Host     → localhost
Port     → 30000
```

We need to connect to this service and send the current password.

---

## 🔌 Step 7 — Connect to Port 30000

We can use the `nc` command.

Run:

```bash
nc localhost 30000
```

### What does `nc` do?

`nc` means:

```text
Netcat
```

Netcat is a command-line networking utility that can create connections to TCP or UDP services.

The command:

```bash
nc localhost 30000
```

means:

```text
Connect to localhost
        ↓
Use port 30000
        ↓
Open a network connection
```

---

## 🔑 Step 8 — Submit the Current Password

After running:

```bash
nc localhost 30000
```

the connection waits for input.

Enter the **current Bandit Level 14 password**:

```text
<YOUR_LEVEL_14_PASSWORD>
```

Then press:

```text
Enter
```

> ⚠️ Do not publish the actual password in your GitHub repository.

If the password is correct, the service returns the password for:

```text
Bandit Level 15
```

---

## 🖥️ Step 9 — Alternative Method Using `echo`

Instead of manually typing the password after connecting, we can send it directly using `echo` and a pipe.

The general format is:

```bash
echo "PASSWORD" | nc localhost 30000
```

Replace:

```text
PASSWORD
```

with your actual Level 14 password.

For example:

```bash
echo "<YOUR_LEVEL_14_PASSWORD>" | nc localhost 30000
```

### What does `echo` do?

```text
echo
```

prints text to the terminal.

Example:

```bash
echo "hello"
```

Output:

```text
hello
```

---

## 🔗 Step 10 — Understand the Pipe `|`

The pipe symbol:

```text
|
```

connects the output of one command to the input of another command.

For example:

```bash
echo "PASSWORD" | nc localhost 30000
```

works like this:

```text
echo "PASSWORD"
       ↓
   Password text
       ↓
       |
       ↓
nc localhost 30000
       ↓
Send password to service
```

So we don't need to manually type the password into `nc`.

---

## 🔓 Step 11 — Get the Level 15 Password

Run:

```bash
nc localhost 30000
```

Then enter the current Level 14 password.

The service will return a response containing the password for:

```text
bandit15
```

> 🔐 Keep the password private and do not publish it in your GitHub repository.

---

# 🖥️ Complete Command Sequence

## Connect to Bandit Level 14

```bash
ssh bandit14@bandit.labs.overthewire.org -p 2220
```

## Verify the current user

```bash
whoami
```

## Check the current directory

```bash
pwd
```

## Connect to port 30000

```bash
nc localhost 30000
```

## Enter the current Level 14 password

```text
<YOUR_LEVEL_14_PASSWORD>
```

The service will return the password for Level 15.

---

# ⚡ One-Line Solution

You can also send the password directly:

```bash
echo "<YOUR_LEVEL_14_PASSWORD>" | nc localhost 30000
```

This performs the following:

```text
echo password
      ↓
      |
      ↓
nc localhost 30000
      ↓
Password submitted
      ↓
Level 15 password returned
```

> ⚠️ Replace `<YOUR_LEVEL_14_PASSWORD>` with the actual password from Level 13 → Level 14.

---

# 🧩 Command Breakdown

## `ssh`

```bash
ssh bandit14@bandit.labs.overthewire.org -p 2220
```

Connects to the Bandit Level 14 server.

---

## `whoami`

```bash
whoami
```

Displays the username of the current user.

Expected output:

```text
bandit14
```

---

## `pwd`

```bash
pwd
```

Displays the current working directory.

Expected output:

```text
/home/bandit14
```

---

## `nc`

```bash
nc localhost 30000
```

Connects to the service running on port `30000` of the local machine.

### Breakdown

```text
nc
```

Netcat, a command-line networking utility.

```text
localhost
```

The local machine.

```text
30000
```

The destination port.

---

## `echo`

```bash
echo "PASSWORD"
```

Prints the specified text.

---

## `|`

```text
|
```

The pipe sends the output of one command to another command.

Example:

```bash
echo "PASSWORD" | nc localhost 30000
```

The password printed by `echo` becomes the input to `nc`.

---

# 🌐 Understanding the Network Connection

The command:

```bash
nc localhost 30000
```

creates a connection to:

```text
Host: localhost
Port: 30000
```

The connection can be represented as:

```text
Your Terminal
      ↓
     nc
      ↓
localhost
      ↓
Port 30000
      ↓
Bandit Service
      ↓
Submit Level 14 Password
      ↓
Receive Level 15 Password
```

---

# 🧠 What I Learned

## 1. Localhost

`localhost` refers to the current computer.

It commonly resolves to:

```text
127.0.0.1
```

---

## 2. Network Ports

A port identifies a network service running on a computer.

In this level, the required port is:

```text
30000
```

---

## 3. Netcat

`nc` stands for:

```text
Netcat
```

It can be used to create network connections from the command line.

Example:

```bash
nc localhost 30000
```

---

## 4. TCP Connection

Netcat can connect to TCP services.

In this level, the service is available on:

```text
localhost:30000
```

We connect to the service and submit the current password.

---

## 5. Pipe

The pipe symbol:

```text
|
```

passes the output of one command as input to another command.

Example:

```bash
echo "PASSWORD" | nc localhost 30000
```

---

## 6. `echo`

The `echo` command prints text.

Example:

```bash
echo "hello"
```

Output:

```text
hello
```

---

# 🧩 Why Each Command Was Used

| Command | Purpose |
| ------- | ------- |
| `ssh` | Connect to the Bandit server |
| `whoami` | Check the current username |
| `pwd` | Show the current directory |
| `nc` | Connect to port 30000 |
| `echo` | Send the password as text |
| `\|` | Send command output to another command |

---

# 🔄 Complete Process

```text
Bandit Level 14
       ↓
      ssh
       ↓
Login using Level 13 password
       ↓
     whoami
       ↓
   Confirm bandit14
       ↓
nc localhost 30000
       ↓
Submit Level 14 password
       ↓
Bandit service checks password
       ↓
Password for Level 15
       ↓
Bandit Level 15 🔓
```

---

# 🏁 Final Solution

The main command used to solve this level is:

```bash
nc localhost 30000
```

Then enter the current Level 14 password.

Alternatively, the password can be sent directly:

```bash
echo "<YOUR_LEVEL_14_PASSWORD>" | nc localhost 30000
```

The service returns the password for:

```text
bandit15
```

---

# ➡️ Next Level

After obtaining the password, connect to **Bandit Level 15**:

```bash
ssh bandit15@bandit.labs.overthewire.org -p 2220
```

Enter the password obtained from the service on port `30000`.

---

## 📚 Commands Practiced

```bash
ssh
whoami
pwd
nc
echo
```

---

# ⭐ Level Completed

```text
Bandit Level 14
       ↓
Current Level 14 Password
       ↓
nc localhost 30000
       ↓
Password submitted
       ↓
Bandit Service
       ↓
Password for Bandit Level 15
       ↓
Bandit Level 15 🔓
```
