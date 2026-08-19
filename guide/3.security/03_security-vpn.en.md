## 🛡️ Server Security (Protection against attacks and brute‑force attempts)

As soon as your VPS is activated, hacker bots start scanning its ports around the clock and trying to guess the SSH password. To prevent your VPN server from being hacked or blocked for spam, we will definitely configure our server’s protection.

> [!IMPORTANT]
> Follow the steps strictly in order. ---

### Choose a way to configure the SSH port:

<details>
<summary><b>🟢 OPTION 1: Easy one‑command method (For beginners)</b></summary>
<br>

If you’re afraid to manually edit system files via `nano`, use this automated command. She will do everything for you without the risk of erasing anything unnecessary.

1. Run the automatic SSH configuration script:
   ```bash
   sudo apt install sed -y && sudo sed -i 's/#Port 22/Port 2222/g' /etc/ssh/sshd_config && sudo sed -i 's/Port 22/Port 2222/g' /etc/ssh/sshd_config
   ```
   *(This command will automatically find the required line in the system and safely replace the standard port 22 with the new port `2222`)*.

2. **Be sure** to open this port in the UFW firewall so that the server doesn’t block you:
   ```bash
   sudo ufw allow 2222/tcp
   ```

3. Restart the SSH service so that the changes take effect:
   ```bash
   sudo systemctl restart ssh
   ```

</details>

<details>
<summary><b>🔥 OPTION 2: Advanced manual method (For pros + Key-based login)</b></summary>
<br>

A classic, proven method with complete password disablement and a switch to cryptographic keys.

#### Step 1. Manually move SSH to a non-standard port
1. Open the SSH configuration file:
  ```bash
   sudo nano /etc/ssh/sshd_config
   ```
2. Find the line `#Port 22` (or `Port 22`).
3. Uncomment it (remove the `#` sign if present) and change the port number:
   ```text
   Port 2222
   ```
4. Save the file (`Ctrl+O`, then `Enter`) and exit (`Ctrl+X`).
5. **If you are using the UFW firewall, be sure to allow the new port before restarting!**
  ```bash
   sudo ufw allow 2222/tcp
   ```
6. Restart the SSH service to apply the settings:
   ```bash
   sudo systemctl restart ssh
   ```
*Now, when connecting to the server for the first time, you will need to specify port 2222 (in Termius or via the command `ssh root@IP -p 2222`).*

#### Step 2. SSH key-based login (Password disablement)
Brute-forcing a text password is only a matter of time. SSH key-based authentication uses asymmetric encryption: only the computer that physically holds your private key will be able to log in to the server. At the same time, logging in using regular passwords is completely blocked.

1. **On your home computer** (in the Linux/Mac terminal or PowerShell on Windows), generate a key pair:
   ```bash
   ssh-keygen -t ed25519 -C "my-vps-key"
   ```
   *(Press Enter to keep the default settings)*.
2. Copy your public key to the VPS server:
   ```bash
   ssh-copy-id -p 2222 root@IP_OF_YOUR_SERVER
   ```
3. Check that you can now log in to the server without entering a password.
4. **Completely disable password-based login.** On the server, open the file `/etc/ssh/sshd_config` again, find and change the following parameters:
   ```text
   PasswordAuthentication no
   PermitRootLogin prohibit-password
   ```
5. Restart SSH: `sudo systemctl restart ssh`. Now bots will physically be unable to brute‑force passwords.

</details>

---

### Step 3. Installing Fail2Ban (Hacker Auto‑Ban)
*This step is mandatory for both options.* 

**Fail2Ban** scans system logs and, if it detects that someone has entered the password incorrectly several times in a row or is trying to hack your `3x-ui` panel, it automatically blocks the attacker’s IP address at the system level.

1. Install the utility with a single command:
   ```bash
   sudo apt update && sudo apt install fail2ban -y
   ```
2. Run and enable autostart when the server starts:
   ```bash
   sudo systemctl start fail2ban
   sudo systemctl enable fail2ban
   ```
3. The basic settings already protect SSH. To check the status and the list of banned bots, use the command:
   ```bash
   sudo fail2ban-client status sshd
   ```
### 🏁 Security Conclusion

Following these simple steps raises the protection of your VPS to the level of corporate standards:
* **Changing the port** removes your server from the radar of 99% of automated hacker bots.
* **Disabling passwords** makes manual selection (brute force) technically impossible.
* **Fail2Ban** acts as a smart shield that instantly isolates any suspicious “guests”.

Now your VPN server not only bypasses restrictions but is also reliably protected from hacking. You can sleep peacefully! 🛡️
