<div align="center">
  <a href="../README.md">
    <img
      src="https://raw.githubusercontent.com/wersennyy/self-hosted-vpn-guide/bb18de14dd61cfcb675e6b2c31e7f64e7d509cd0/resources/vpn-wave-header.svg"
      width="100%"
      alt="Self-Hosted VPN"
    />
  </a>
</div>

<div align="center">

[![License: MIT](https://img.shields.io/badge/License-MIT-0d1117?style=flat-square&labelColor=0d1117)](../LICENSE)
[![OS: Linux](https://img.shields.io/badge/OS-Linux-0d1117?style=flat-square&logo=linux&logoColor=white&labelColor=0d1117)](https://www.linux.org/)

<br />

[![English](https://img.shields.io/badge/README-English-159fba?style=for-the-badge&labelColor=0a2038)](../README.en.md)
[![Русский](https://img.shields.io/badge/README-Русский-159fba?style=for-the-badge&labelColor=0a2038)](README.md)
[![Гайды](https://img.shields.io/badge/OPEN-GUIDES-159fba?style=for-the-badge&labelColor=0a2038)](./)

</div>

<br />

---

<div align="center">

> **GUIDE 03 / 05**  
> *SSH · Firewall · Fail2ban · Hardening*

</div>

---

## Server Security (VPS)

This section is dedicated to protecting your VPS. I strongly recommend following these steps **before** or **immediately after** installing the panel to avoid exposing your server to unnecessary risk.

Security is not a single command, but a set of measures. We'll go through everything in order: from SSH keys to firewall setup and brute-force protection.

---

### 1. SSH Keys and Disabling Password Login

The first and most important measure is to switch to SSH key login and disable password authentication.

#### What Are SSH Keys

SSH keys are a pair of files:

- **Private key** — stored on your computer and must never be shared.
- **Public key** — copied to the server and used to verify your identity.

Instead of a password, you use a key. This is more secure and more convenient.

#### Generating SSH Keys (on Your Computer)

**On macOS / Linux:**

1. Open Terminal.
2. Run the command:

   ```bash
   ssh-keygen -t ed25519 -C "your_email@example.com"
   ```

3. Press Enter to save the key in the default location (`~/.ssh/id_ed25519`).
4. Create and enter a passphrase — this is additional protection for the key. You can leave it empty, but I recommend setting one.

**On Windows (via PuTTY):**

1. Download and run [PuTTYgen](https://puttygen.com).
2. Select key type **Ed25519** (or RSA 4096 if Ed25519 is unavailable).
3. Click **Generate** and move your mouse to create randomness.
4. Save the private key (button **Save private key**) in a secure location.
5. Copy the public key from the top field.

#### Copying the Public Key to the Server

**On macOS / Linux:**

1. Run the command (replace `root@IP_ADDRESS` with your details):

   ```bash
   ssh-copy-id root@IP_ADDRESS
   ```

2. Enter the server password when prompted.

**On Windows (via PuTTY):**

1. Connect to the server via SSH using PuTTY (with password).
2. Create the keys directory:

   ```bash
   mkdir -p ~/.ssh
   chmod 700 ~/.ssh
   ```

3. Open the `authorized_keys` file:

   ```bash
   nano ~/.ssh/authorized_keys
   ```

4. Paste the public key (on a single line, without line breaks).
5. Save (`Ctrl+O`, `Enter`) and exit (`Ctrl+X`).
6. Set the correct permissions:

   ```bash
   chmod 600 ~/.ssh/authorized_keys
   ```

#### Verifying Key-Based Login

1. Disconnect from the server (`exit`).
2. Try connecting again:

   - **macOS / Linux:**

     ```bash
     ssh -i ~/.ssh/id_ed25519 root@IP_ADDRESS
     ```

   - **Windows (PuTTY):**
     - In PuTTY, under **Connection → SSH → Auth**, specify the path to your private key.
     - Connect to the server.

If you log in without a password, it's working.

#### Disabling Password Login

Only after you've confirmed that key-based login works, disable password authentication.

1. Connect to the server (using the key).
2. Open the SSH config:

   ```bash
   nano /etc/ssh/sshd_config
   ```

3. Find and modify (or add) the following lines:

   ```text
   PasswordAuthentication no
   ChallengeResponseAuthentication no
   UsePAM no
   ```

4. Save the file and exit.
5. Restart SSH:

   ```bash
   systemctl restart sshd
   ```

> [!WARNING]
> **Do not disable password login until you've verified that key-based login works.**  
> Otherwise, you may lose access to your server.

---

### 2. Changing the SSH Port (Optional)

By default, SSH listens on port 22. Bots often scan this port for brute-force attacks. Changing the port doesn't provide 100% protection, but it reduces the number of attack attempts.

#### How to Change the SSH Port

1. Connect to the server via SSH.
2. Open the config:

   ```bash
   nano /etc/ssh/sshd_config
   ```

3. Find the line:

   ```text
   #Port 22
   ```

4. Replace it with:

   ```text
   Port 2222
   ```

   (you can choose another free port, e.g., 2222, 2200, 2244, etc.)

5. Save the file and exit.
6. Restart SSH:

   ```bash
   systemctl restart sshd
   ```

7. Make sure the port is allowed in the firewall (covered below).

#### Connecting After Changing the Port

Now you need to specify the new port when connecting:

- **macOS / Linux:**

  ```bash
  ssh -p 2222 -i ~/.ssh/id_ed25519 root@IP_ADDRESS
  ```

- **Windows (PuTTY):**
  - In the "Port" field, enter the new port (e.g., 2222).

> [!NOTE]
> Changing the port is optional. If you're not comfortable with it, you can leave it as 22, but then it's especially important to use SSH keys and fail2ban.

---

### 3. Configuring the Firewall (UFW)

A firewall controls which ports are open to the internet and which are closed.

#### Installing UFW

On Ubuntu, UFW is usually already installed. Check:

```bash
ufw version
```

If not, install it:

```bash
apt install -y ufw
```

#### Basic UFW Configuration

1. Allow SSH (important to do this **before** enabling the firewall):

   - If you're using the default port 22:

     ```bash
     ufw allow 22/tcp
     ```

   - If you changed the port (e.g., 2222):

     ```bash
     ufw allow 2222/tcp
     ```

2. Allow ports for the panel and VPN:

   - For Marzban (panel via Caddy, HTTPS):

     ```bash
     ufw allow 443/tcp
     ```

   - For inbound (e.g., port 443 or another one you used):

     ```bash
     ufw allow 443/tcp
     ufw allow 8443/tcp
     ```

   (specify only the ports you actually use)

3. Enable the firewall:

   ```bash
   ufw --force enable
   ```

4. Check the status:

   ```bash
   ufw status verbose
   ```

You should see a list of allowed ports.

> [!WARNING]
> **Always allow the SSH port in UFW before enabling the firewall.**  
> Otherwise, you may lock yourself out of the server.

#### Blocking Unnecessary Ports

By default, UFW denies all incoming connections for which there is no `allow` rule. This is correct. Don't open ports "just in case".

---

### 4. Brute-Force Protection (Fail2ban)

Fail2ban monitors logs and automatically bans IPs that attempt to connect via SSH with incorrect credentials too frequently.

#### Installing Fail2ban

1. Install the package:

   ```bash
   apt update
   apt install -y fail2ban
   ```

2. Check the status:

   ```bash
   systemctl status fail2ban
   ```

   It should show `active (running)`.

#### Basic Fail2ban Configuration

1. Create a local config file:

   ```bash
   cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
   ```

2. Open it:

   ```bash
   nano /etc/fail2ban/jail.local
   ```

3. Find the `[sshd]` section and make sure it's enabled:

   ```text
   [sshd]
   enabled = true
   ```

4. Optionally, you can configure parameters, for example:

   ```text
   maxretry = 3
   bantime = 3600
   findtime = 600
   ```

   This means:
   - 3 failed attempts within 10 minutes → ban for 1 hour.

5. Save the file and exit.
6. Restart Fail2ban:

   ```bash
   systemctl restart fail2ban
   ```

#### Checking Fail2ban Operation

Check the status:

```bash
fail2ban-client status sshd
```

You'll see how many IPs are currently banned.

---

### 5. Basic Maintenance Recommendations

A few simple rules that will significantly improve security:

1. **Regularly update your system:**

   ```bash
   apt update && apt upgrade -y
   ```

   Do this at least once every 1–2 weeks.

2. **Don't install unnecessary software.**  
   The fewer programs on the server, the fewer potential vulnerabilities.

3. **Monitor logs.**  
   At least occasionally, check:

   ```bash
   journalctl -u sshd --no-pager -n 50
   fail2ban-client status
   ufw status verbose
   ```

4. **Use strong passwords** wherever they're still used (panel, email, domain).

5. **Back up** important configs and data (this will be covered in a separate section).

---

### 6. What's Next

After setting up security, you can safely proceed to:

- installing and configuring panels (Marzban / Remnawave);
- creating inbounds and users;
- connecting clients.

Security is not a one-time action, but an ongoing process. However, even the measures described above are enough to make your server much more secure than "out of the box".

> [!NOTE]
> In the following sections, we'll cover panel updates and maintenance, as well as additional measures for bypassing blocks.
