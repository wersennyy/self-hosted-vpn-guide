# 🖥️ Step‑by‑step VPS deployment and 3x-ui panel configuration

In this guide, I have detailed how to rent a server, protect it from basic attacks, install the control panel, and launch the VLESS + Reality protocol.

---

## 🏠 Step 1.Server purchase and basic protection (Hardening)

1. **Hosting selection:** There are a lot of different sites available on the Internet with rentals of various servers WITH PAYMENT IN RUBLES, I chose the simplest and most inexpensive server on the site [Hostkey](https://hostkey.ru ) for 490 rubles/month. For a personal VPN, this is enough.

## , Server Characteristics 
To implement a VPN server, I selected a server with the following parameters:

* **Processor (CPU):**  1 vCPU.
* **Random Access Memory (RAM):** 1 GB.
* **Storage (Disk):** 40 GB NVMe SSD (this is even a lot; you can get much less — 20 GB will be more than enough).
* **Bandwidth (Port):** 1 Gbps.
* **Traffic:** 3 TB (up to 10 users will be more than enough).
* **Location (Geo):** I chose Finland because it’s the closest location to me.

2. **Payment and receipt of server data and management:**
   Select the server settings and make the payment.If they ask for an email address, enter it.Within 10 minutes, you will receive the login and password via email.After the purchase, you will be able to manage the server on the website.
Turn it on and click the “Go to terminal” button.
> [!NOTE]
> **If you suddenly don’t see this button, follow the guide below ↓**
<details>
<summary>📋 Guide to help</summary>
Open the terminal on the PC and connect to the server via SSH (take the IP and temporary password from the hosting account):
   ```bash
   ssh root@YOUR_SERVER_IP
   ```
</details>

8. **Password change:** First, change the standard root password to your own long and complex one to prevent bots from brute‑forcing the server:
   ```bash
   passwd root
   ```
9. **System update:**We apply all the latest security patches and restart the server so that the changes take effect:
   ```bash
   sudo apt update && sudo apt upgrade -y && reboot
   ```
   *After the reboot, wait a minute and reconnect via SSH, but this time with the new password.*

---

## 🛠️ Step 2. Installing and configuring the 3x-ui panel

To avoid manually tinkering with the raw Xray JSON configurations, we’ll set up a convenient web panel. It will automatically assemble the necessary configuration files.

1. **Running the installer:** Copy and paste the command from the official automatic installation script:
   ```bash
   bash <(curl -Ls https://raw.githubusercontent.com/mhsanaei/3x-ui/master/install.sh)
   ```
   > **This is the official script for the automatic installation of the panel.**

2. **Setup during installation:** 
   * The script will ask if you want to change the default port, login, and password. ** We definitely agree (press `y`)**.
   * Enter your custom username, a complex password, and a port for entering the panel (for example, `2053` or any other free one).
3. **Data retention:** Write down the received data. The address of the panel now looks like this: `https://YOUR_SERVER_IP:YOUR_PORT`

---

## 🔒 Step 3. Log in to the panel and create a connection (Inbound)

1. Open a browser and go to the address of our panel: `http://YOUR_SERVER_IP:YOUR_PORT`.
2. Enter the login and password that you specified when installing 3x-ui.
3. Go to the **Inbounds (Incoming connections)** section and click the **Add Inbound (Add connection)** button.

### Connection settings (VLESS-Reality):
* **Remark (Name):** My-Private-VPN (or any other name)
* **Protocol (Protocol):** `vless`
* **Port (Port):** `51820` (I chose this port; it’s standard for WireGuard, but we’ll be using TCP)
* **Client (Client):** We keep one user by default; the ID will be generated automatically.
* **Transmission (Transport):** `tcp`
* **Security (Security):** Select `reality`
* **uTLS:** `chrome` (masking as the Chrome browser)
* **Dest (Where to redirect traffic for masking):** `yahoo.com:443` or `microsoft.com:443`
* **Server Names (Sni):** `yahoo.com` or `microsoft.com`
* **Private Key / Public Key:** Click the **Get New Keys (Generate)** button so that the panel itself generates the encryption keys.

Click **Create (Create)**. That’s it — the server part is fully ready and is disguised as the official website!

> [!NOTE]
> **Continued in the *Client-vpn* file**
