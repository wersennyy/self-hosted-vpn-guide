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

> **GUIDE 01 / 04**  
> *VPS · Initial Setup · Basic Protection · Marzban*

</div>

---

## 1. Domain Purchase
### How and Where to Buy a Domain

If you don't have your own domain yet, no problem. Registration takes 10–15 minutes and requires no special knowledge.

#### What is a Domain and Why You Need It

A domain is a website name on the internet, for example:

- `example.com`
- `mysite.net`
- `myvpn.org`

For Marzban, you need a domain to:

- use it in the **VLESS + Reality** protocol as "masking";
- issue a real HTTPS certificate for it;
- access the panel and subscriptions via a clean URL, not just by IP.

You don't need a "fancy" or expensive domain. The simplest and cheapest one will do, as long as you can manage DNS records.

#### Where You Can Buy a Domain

Domains are sold by special companies — registrars. Several popular options with links:

- **Reg.ru** — one of the most well-known registrars in Russia:  
  [https://www.reg.ru](https://www.reg.ru)
- **Nic.ru** — a large registrar, often has promotions:  
  [https://www.nic.ru](https://www.nic.ru)
- **Beget.com** — hosting + registrar, simple panel:  
  [https://beget.com](https://beget.com)
- **Namecheap.com** — international registrar, often cheap domains:  
  [https://www.namecheap.com](https://www.namecheap.com)

This is not an advertisement, just examples. Choose one that has:

- the domain zone you need (`.com`, `.net`, `.org`, etc.);
- a clear management panel;
- decent support.

#### Which Domain Zone to Choose

For a VPN panel, the domain zone doesn't really matter. These will work:

- `.com` — [https://www.reg.ru/domain/com/](https://www.reg.ru/domain/com/)
- `.net` — [https://www.reg.ru/domain/net/](https://www.reg.ru/domain/net/)
- `.org` — [https://www.reg.ru/domain/org/](https://www.reg.ru/domain/org/)
- `.site` — [https://www.reg.ru/domain/site/](https://www.reg.ru/domain/site/)
- `.online` — [https://www.reg.ru/domain/online/](https://www.reg.ru/domain/online/)

The main things are that the domain is:

- inexpensive (often from 100–300 rubles per year);
- with the ability to manage DNS;
- without mandatory complex verification if you want to start quickly.

#### Step-by-Step Domain Registration (Using Reg.ru as an Example)

I'll show using Reg.ru as an example; other registrars are very similar.

1. **Go to the registrar's website**  
   Open [https://www.reg.ru](https://www.reg.ru) in your browser.

2. **Enter your desired domain name**  
   In the search field, type something like:
   - `myvpn123`
   - `myhomevpn`
   - any other word + numbers if it's taken.

   Click "Check" or a similar button.

3. **Choose an available domain**  
   The system will show which zones are available. Choose the cheapest and clearest one, for example:
   - `myvpn123.com`
   - `myvpn123.net`

   Click "Buy" or "Register".

4. **Create an account / log in**  
   If you don't have an account yet, register:
   - specify your e-mail;
   - set a password;
   - confirm your e-mail.

   Registration page: [https://www.reg.ru/registration/](https://www.reg.ru/registration/)

5. **Fill in owner details**  
   By rules, you need to specify domain owner details (full name, phone, e-mail). Fill them in with real data to avoid problems in the future.

6. **Pay for the domain**  
   Pay for the order by card or another available method. After payment, the domain will appear in your personal account.

   Personal account: [https://www.reg.ru/my/](https://www.reg.ru/my/)

7. **Check that the domain is yours**  
   In your personal account, find the section "My domains" or similar. Your new domain should be displayed there.

#### What to Do After Purchase

After registering the domain, you will need to:

- log in to the domain management panel;
- find the "DNS servers" or "DNS management" section;
- later — create 2–3 subdomains there (`panel`, `sub`, `node`) and point them to your VPS IP.

We will cover DNS setup in detail in the next subsection, once you have both the domain and the VPS.

> [!NOTE]
> If you're not sure which domain to choose, pick the simplest and cheapest `.com` or `.net` with any available name. For VPN, it doesn't really matter.


---


## 2. Server (VPS) Purchase

Now that you have a domain (or at least understand how to buy one), the next step is to rent a VPS where the Marzban panel will run.

### What VPS is Needed for Marzban

For a personal VPN based on Marzban, an inexpensive virtual server will do. Main requirements:

- **OS:** Ubuntu 22.04 or 24.04 (we'll use 24.04 in this guide);
- **CPU:** 1 core (2 is better);
- **RAM:** minimum 1 GB, comfortable — 2 GB;
- **Disk:** 15–20 GB SSD;
- **Port:** 100 Mbit/s and higher;
- **Location:** anywhere convenient for you and where there are no issues accessing needed resources (I chose Finland, it's closest to me).

For one to three users, a tariff around 400–600 rubles per month is usually enough. If you plan more people or serious loads, better take something more powerful.

### Where You Can Rent a VPS

There are many hosting providers with ruble payments online. I started with a simple and inexpensive server at:

- [Hostkey](https://hostkey.ru) — for ~490 rub/month, this is more than enough for a personal VPN.

Other options worth checking:

- [xorek.cloud](https://xorek.cloud) — an alternative, sometimes cheaper;
- [play2go.cloud](https://play2go.cloud/) — gaming server hosting, also suitable;
- [my.u1host.com](https://my.u1host.com) — a time-tested option.

This is not an advertisement, just examples. Choose yourself, read reviews, and make sure that:

- Ubuntu 22.04/24.04 is supported;
- the network is decent and support is adequate;
- price and specs suit you.

### Step-by-Step VPS Purchase (General Scheme)

Interfaces differ between hosting providers, but the general sequence is similar everywhere.

1. **Register on the hosting website**  
   Specify your e-mail, set a password, confirm your e-mail.

2. **Go to the "VPS" / "Virtual servers" section**  
   Choose a tariff that fits the requirements above (Ubuntu, 1–2 cores, 1–2 GB RAM).

3. **Choose the operating system**  
   In the image settings, select **Ubuntu 24.04** (or 22.04 if 24.04 is not available).

4. **Choose a location**  
   If there's a choice of city/country, select one that's convenient for you (closer to you or where access to resources is better).

5. **Pay for the tariff**  
   Pay for the order by card or another available method.

6. **Get server credentials**  
   After creating the VPS, you will receive:
   - public IP address;
   - login (usually `root`);
   - password (or SSH key if you used one).

   Save these details in a safe place.

7. **Check server access**  
   Try connecting via SSH (this will be covered in a separate section). If the connection works — the server is ready.

### What Must Be Ready Before Panel Setup

By the time you start Marzban setup, you should have:

- a rented VPS with Ubuntu 22.04/24.04;
- IP address, login and password (or SSH key) for the server;
- a registered domain and access to DNS management;
- an e-mail created for certificates.

If all this is ready, you can proceed to server preparation and Marzban panel installation.


## 3. Server Preparation and Marzban Panel Installation

Before setting up the panel, I strongly recommend reading and applying recommendations from a separate guide on server protection:

- **[3.security](https://github.com/wersennyy/self-hosted-vpn-guide/blob/main/guide/3.security/03_security-vpn.ru.md)** — SSH setup, firewall, basic server protection.

I intentionally moved security questions to a separate file to focus here on Marzban installation and setup. I'll briefly describe minimal server preparation (SSH connection, updates, utilities installation), but detailed protection recommendations are better viewed in the separate guide above.

### 3.1. Basic Server Preparation

Before installing Marzban, you need to perform minimal server preparation.

#### Connecting to the Server via SSH

Connect to your VPS via SSH.

**If you're on Windows:**

1. Download and install [PuTTY](https://putty.org.ru/) (I'm attaching the Russian version with the "ru" suffix, as the regular one doesn't work for me).
2. Launch PuTTY.
3. In the "Host Name (or IP address)" field, enter your server's IP address.
4. Leave the port as `22`.
5. Click "Open".
6. In the window that appears, enter:
   - login: usually `root`;
   - password: the one provided by the hosting (characters won't be displayed when typing — this is normal).

**If you're on macOS or Linux:**

1. Open a terminal.
2. Enter the command:

   ```bash
   ssh root@IP_АДРЕС_СЕРВЕРА
   ```

   For example:

   ```bash
   ssh root@45.76.123.45
   ```

3. Press Enter.
4. When asked `Are you sure you want to continue connecting (yes/no/[fingerprint])?`, type `yes`.
5. Enter the password (characters won't be displayed) and press Enter.

If everything went successfully, you'll see a command prompt, something like:

```bash
root@vps:~#
```

> [!NOTE]
> If the hosting gave you an SSH key instead of a password, you need to connect using the key. Usually this is a command like:
> ```bash
> ssh -i путь/к/ключу root@IP_АДРЕС
> ```
> Check the exact command and instructions in your hosting documentation.

#### System Update

After the first connection, I strongly recommend updating the system. This will patch known vulnerabilities and install the latest package versions.

Run:

```bash
apt update && apt upgrade -y
```

- `apt update` — updates the list of available packages;
- `apt upgrade -y` — installs updates without additional prompts.

Wait for the commands to complete.

#### Installing Required Packages

For Marzban installation and domain work, we'll need some utilities.

Install the basic set:

```bash
apt install -y curl wget git
```

These packages will be useful for:

- downloading scripts and files;
- working with archives;
- installing Docker and the panel itself.

> [!NOTE]
> More detailed recommendations on server protection (SSH keys setup, firewall, fail2ban, etc.) are described in a separate guide:  
> **[3.security](https://github.com/wersennyy/self-hosted-vpn-guide/blob/main/guide/3.security/03_security-vpn.ru.md)**.  
> If you plan to use the server not only for VPN, I strongly advise reading it.

Basic server preparation is now complete. Next, we proceed to Marzban installation.


### 3.2. Marzban Installation

Now that the server is prepared, we proceed to installing the Marzban panel. I'll show installation via Docker — this is the official and most convenient method.

#### What is Docker (Very Briefly)

Very simply: Docker is a tool that allows running applications in isolated containers.

- Each container is like a "separate system" with its own files and settings.
- You don't need to manually install dependencies, libraries, etc. — everything is already inside the image.
- For Marzban, this means: you install Docker once, and then the panel runs in a container that's easy to update and back up.

You don't need to deeply understand Docker to use Marzban. Just follow the commands I'll show.

#### Installing Docker and Docker Compose

First, let's install Docker and Docker Compose, which are needed for Marzban.

1. Update the package list and install required utilities:

   ```bash
   apt update
   apt install -y curl gnupg
   ```

2. Add Docker's GPG key:

   ```bash
   install -m 0755 -d /etc/apt/keyrings
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg
   chmod a+r /etc/apt/keyrings/docker.gpg
   ```

3. Add Docker repository:

   ```bash
   echo \
     "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
     $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
     tee /etc/apt/sources.list.d/docker.list > /dev/null
   ```

4. Update the package list and install Docker:

   ```bash
   apt update
   apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
   ```

5. Check that Docker and Compose are installed:

   ```bash
   docker --version
   docker compose version
   ```

   You should see something like:

   ```text
   Docker version 27.x.x, build ...
   Docker Compose version v2.x.x
   ```

Docker is now installed and ready.

#### Creating a Folder for Marzban

I recommend storing Marzban configuration in a separate folder. This makes backups easier and prevents losing settings.

1. Create a folder, for example `/opt/marzban`:

   ```bash
   mkdir -p /opt/marzban
   cd /opt/marzban
   ```

2. Inside this folder, we'll create `docker-compose.yml` and `.env` files.

#### Creating the `docker-compose.yml` File

Create the `docker-compose.yml` file in the `/opt/marzban` folder:

```bash
nano docker-compose.yml
```

Paste the following content:

```yaml
services:
  marzban:
    image: gozargah/marzban:latest
    restart: always
    env_file: .env
    network_mode: host
    volumes:
      - /var/lib/marzban:/var/lib/marzban
```

Save the file (`Ctrl+O`, then `Enter`) and exit (`Ctrl+X`).

> [!NOTE]
> This is a minimal configuration to start. Later, when setting up the domain and HTTPS, we'll expand it.

#### Creating the `.env` File

In the same folder, create the `.env` file:

```bash
nano .env
```

First, generate a random secret for Marzban:

```bash
openssl rand -hex 32
```

Copy the command output (a long string of letters and digits).

Now paste it into the `.env` file:

```text
MARZBAN_JWT_SECRET=insert_the_openssl_string_here
```

Example:

```text
MARZBAN_JWT_SECRET=a3f1b8c9d2e4f5a6b7c8d9e0f1a2b3c4d5e6f7a8b9c0d1e2f3a4b5c6d7e8f9a0
```

Save the file and exit.

#### Launching Marzban

Now let's start the panel.

1. While in the `/opt/marzban` folder, run:

   ```bash
   docker compose up -d
   ```

2. Check that the container started:

   ```bash
   docker compose ps
   ```

   You should see the `marzban` container with status `Up`.

3. Open in your browser:

   ```text
   http://IP_АДРЕС_СЕРВЕРА:8000
   ```

   For example:

   ```text
   http://45.76.123.45:8000
   ```

You should see the Marzban panel login page.

#### First Login to the Panel

On first launch, you need to create an admin.

1. Open the panel at `http://IP_АДРЕС_СЕРВЕРА:8000`.
2. Enter:
   - desired admin login;
   - password (remember it or save it in a safe place).
3. Click "Create Admin" or a similar button.

After this, you'll log in to the panel and be able to create users and configure inbound rules.

> [!NOTE]
> For now, the panel runs over HTTP and is accessible by IP. In the next step, we'll set up the domain, HTTPS, and more secure access.

Basic Marzban installation is now complete. Next, we proceed to domain and HTTPS setup.




### 3.3. Domain and HTTPS Setup for the Panel

Now let's set up the domain and HTTPS so the panel opens via a secure URL and is protected by a certificate.

#### Why Domain and HTTPS for the Panel

Currently, the panel is accessible at:

```text
http://IP_АДРЕС_СЕРВЕРА:8000
```

This is inconvenient and insecure:

- the address is easy to find and share;
- the connection is unencrypted;
- browsers may warn about an "insecure connection".

We'll make the panel accessible at an address like:

```text
[https://panel.ваш-домен.com](https://panel.ваш-домен.com)
```

For this, we need to:

- create a subdomain for the panel (e.g., `panel`);
- point it to the server IP;
- configure Marzban and reverse proxy;
- issue an HTTPS certificate.

#### Step 1. Creating a Subdomain for the Panel in DNS

Log in to your domain management panel (where you bought it: Reg.ru, Nic.ru, Beget, Namecheap, etc.).

We need to create one DNS `A` record for the `panel` subdomain.

##### How This Looks at Different Registrars

Interfaces differ, but the idea is the same: create an `A` record with name `panel` and value — your server's IP.

**Example for Reg.ru:**

1. Log in to your Reg.ru account.
2. Go to "My domains".
3. Click on the desired domain.
4. Select "DNS servers and zone management" (or similar).
5. Click "Add record".
6. Choose record type `A`.
7. Fill in the fields:
   - **Name/Host/Subdomain:** `panel`
   - **IP address:** your VPS IP
   - **TTL:** leave default.
8. Save the record.

**Example for Nic.ru:**

1. Account → "My domains".
2. Click on the domain.
3. Section "DNS" / "Zone management".
4. Add a new record:
   - **Type:** `A`
   - **Name:** `panel`
   - **IP:** your server IP.
5. Save.

**Example for Beget:**

1. Account → "DNS".
2. Select the domain.
3. Add a record:
   - **Type:** `A`
   - **Subdomain:** `panel`
   - **IP:** your VPS IP.
4. Save.

**Example for Namecheap:**

1. Account → "Domain List".
2. Click "Manage" on the desired domain.
3. Go to "Advanced DNS".
4. Add a new record:
   - **Type:** `A Record`
   - **Host:** `panel`
   - **Value:** your server IP.
5. Save.

In the end, you should have a record like:

```text
panel  A  IP_АДРЕС_СЕРВЕРА
```

Save changes. DNS propagation may take from a few minutes to several hours, but usually it's fast for new records.

##### Checking DNS

Check that the subdomain works. On your computer, run:

```bash
ping panel.ваш-домен.com
```

Replace `ваш-домен.com` with your real domain, for example:

```bash
ping panel.myvpn.net
```

You should see that the domain resolves to your server's IP. If it says "unknown host" instead of an IP — DNS hasn't updated yet or the record was created incorrectly.

> [!NOTE]
> If `ping` doesn't work (no reply), this isn't always an error. The main thing is that the domain resolves to the correct IP.  
> You can also check via:
> ```bash
   nslookup panel.ваш-домен.com
