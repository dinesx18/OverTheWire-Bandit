# Bandit Level 0

<img width="1586" height="573" alt="bandit-level-0" src="https://github.com/user-attachments/assets/da7204e3-baf6-4686-b6d7-63f53cf6909e" />

## 🎯 Goal

The goal of this level is to connect to the Bandit server using SSH.

## 🔐 Step 1 — Connect using SSH

I used the following command in Kali Linux:

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

This command is used to connect to the Bandit server using SSH.

### 🔎 Breaking down the command

- `ssh` → Secure Shell, used to connect to a remote computer.
- `bandit0` → The username used for Level 0.
- `@` → Separates the username from the hostname.
- `bandit.labs.overthewire.org` → The Bandit server hostname.
- `-p` → Specifies which port SSH should use.
- `2220` → The SSH port used by the Bandit server.

<img width="1920" height="1200" alt="Screenshot 2026-09-09 193026" src="https://github.com/user-attachments/assets/33065880-ccb2-4386-852a-9a9d0a2b00d7" />

## 🔑 Step 2 — Enter the Password

After running the SSH command, the Bandit server asked me for the password.

For Level 0 password is:

```text
Password: bandit0
```

<img width="637" height="1280" alt="Screenshot 2026-09-09 193711 (2)" src="https://github.com/user-attachments/assets/66b05baf-414b-4cac-b7e7-fc4ac8fe9e63" />
