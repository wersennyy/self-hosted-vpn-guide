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

> **GUIDE 02 / 04**  
> *Inbounds · Users · Clients · Diagnostics*

</div>

---

## Connection Setup: First Inbound, User, and Client

In this section, we will fully configure your VPN connection based on Marzban:

- create the first inbound using the **VLESS + Reality** protocol;
- add a user with limits;
- obtain a subscription link and QR code;
- connect a client on your phone or computer.

I recommend following these steps sequentially and not skipping any, especially if you're doing this for the first time.

---

### 1. Creating the First Inbound (VLESS + Reality)

You already have the Marzban panel installed and accessible via HTTPS. The next step is to create an inbound through which clients will connect.

We will use the modern and blockage-resistant protocol **VLESS + Reality**.

#### What is VLESS + Reality (Very Briefly)

- **VLESS** — a lightweight and fast protocol over Xray, without extra encryption at its own level (all encryption happens inside TLS).
- **Reality** — a masking mechanism that makes your connection look like regular HTTPS traffic to a popular website.

For you, this means:

- the connection looks like a normal website visit;
- it's harder to distinguish from legitimate traffic;
- good resistance to DPI and blocking.

#### Preparing a Domain for Masking

For Reality, we need a domain that will be used as "masking".

We already created the `panel` subdomain for the panel. Now let's create another one — for Reality masking.

1. Log in to your domain management panel (where you created `panel`).
2. Create a new DNS `A` record:
   - **Name/Host/Subdomain:** `node` (or any other name, e.g., `site`, `mask`);
   - **IP address:** your VPS IP;
   - **TTL:** leave default.
3. Save the record.

You should end up with something like:

```text
node  A  YOUR_VPS_IP
```

Check that the domain resolves:

```bash
ping node.yourdomain.com
```

Replace `yourdomain.com` with your actual domain.

> [!NOTE]
> This domain will be used as "masking" for Reality.  
> Later, you can put a simple placeholder site on it, but for now, just the DNS record is enough.

#### Creating an Inbound in the Marzban Panel

1. Open the Marzban panel at:

   ```text
   https://panel.yourdomain.com
   ```

2. Log in with the admin credentials you created earlier.

3. In the left menu, find the **Inbounds** section (or similar, depending on the version).

4. Click **Add Inbound** / **Create Inbound**.

5. Fill in the parameters:

   - **Protocol:** `VLESS`
   - **Transport:** `tcp` (or `ws` if you prefer, but I recommend `tcp` to start)
   - **Port:** choose a free one, e.g., `443` or another (if port 443 is already taken, you can use `8443`, `2053`, etc.)
   - **TLS:** enable
   - **Reality:** enable

6. Configure Reality:

   - **Private Key:** generate a random private key. The panel usually has a "Generate" button. If not, generate it on the server:

     ```bash
     openssl genpkey -algorithm ed25519 -outform DER | base64 -w0
     ```

     This command will generate a private key for Reality in base64 format. Copy the output and paste it into the "Private Key" field in the panel.

   - **Server Names:** specify your masking domain, for example:

     ```text
     node.yourdomain.com
     ```

   - **Dest:** specify the address your connection will "pretend" to be. Popular sites are often used, for example:

     ```text
     www.cloudflare.com:443
     ```

     or

     ```text
     www.microsoft.com:443
     ```

     This doesn't mean traffic will go there — it's only for masking.

7. Save the inbound.

After saving, you'll see a new inbound with status `Active` (or similar).

> [!NOTE]
> Remember or write down:
> - inbound name;
> - port;
> - masking domain.  
> You'll need these when creating a user and connecting the client.

---

### 2. Creating a User and Subscription

Now that the inbound is ready, let's create the first user and get a subscription link.

#### Creating a User in Marzban

1. In the panel, go to the **Users** section.

2. Click **Add User** / **Create User**.

3. Fill in the parameters:

   - **Username:** user name, e.g., `user1`, `phone`, `pc` — whatever you prefer.
   - **Inbounds:** select the previously created inbound with VLESS + Reality.
   - **Expire date:** expiration date. For testing, you can set it far in the future, e.g., one year.
   - **Data limit:** traffic limit. You can leave it unlimited or set, for example, 50 GB.

4. Save the user.

After creation, you'll see the user card with their status, used traffic, and links.

#### Getting the Subscription Link and QR Code

For each user, Marzban generates:

- **Subscription URL** — a link that can be imported into a client;
- **QR code** — for quick connection from a phone.

1. Open the created user's card.

2. Find the **Subscription Link** field.

3. Copy the link. It will look something like:

   ```text
   https://panel.yourdomain.com/sub/USERNAME/TOKEN
   ```

4. A QR code should also be available (button "Show QR").

> [!NOTE]
> This link can be imported into most modern clients:  
> v2rayNG, Hiddify, Clash Verge, Nekoray, and others.

---

### 3. Connecting the Client (Happ)

Now let's connect your device to the VPN using the **Happ** client.

I'll describe installation and setup for Android / iOS / Windows. The logic is the same everywhere: install the app → import the subscription → connect.

#### What is Happ

Happ is a modern client for working with Xray/VLESS subscriptions. It:

- supports importing links from Marzban;
- automatically updates configurations;
- has a simple interface;
- is available on Android, iOS, Windows, and macOS.

Official website: [Happ](https://www.happ.su/main/ru).

---

#### Connecting on Android

1. **Install Happ**

   - Open Google Play.
   - Search for "Happ" or follow the link from the official repository.
   - Install the app.

2. **Import the Subscription**

   - Open Happ.
   - On the main screen, tap **«+»** or **«Add profile»**.
   - Select **«Import from URL»**.
   - Paste the subscription link you copied from Marzban:

     ```text
     https://panel.yourdomain.com/sub/USERNAME/TOKEN
     ```

   - Tap **«Import»**.

3. **Connect**

   - After import, a configuration will appear in the list (usually named after your inbound or user).
   - Tap on it to select.
   - Tap the big **«Connect»** button.

4. **Check the Connection**

   - Open [https://ipleak.net](https://ipleak.net) or [https://2ip.ru](https://2ip.ru).
   - Make sure the IP has changed to your VPS IP.
   - Check that websites load.

---

#### Connecting on iOS (iPhone / iPad)

1. **Install Happ**  
   (If you're in Russia, there's an alternative called INCY, fully identical to Happ, but available in the App Store. If you want to use Happ specifically, you'll need to change the App Store region (check a YouTube guide for this).)

   - Open the App Store.
   - Search for "Happ".
   - Install the app.

2. **Import the Subscription**

   - Open Happ.
   - On the main screen, tap **«+»** or **«Add subscription»**.
   - Select **«Import from URL»**.
   - Paste the link from Marzban:

     ```text
     https://panel.yourdomain.com/sub/USERNAME/TOKEN
     ```

   - Tap **«Import»**.

3. **Connect**

   - After import, a configuration will appear in the list.
   - Tap on it.
   - Tap **«Connect»**.

4. **Check the Connection**

   - Open any IP check website.
   - Make sure the IP has changed to your VPS IP.

---

#### Connecting on Windows

1. **Install Happ**

   - Download the Happ installer for Windows from the official website.
   - Install the app.

2. **Import the Subscription**

   - Open Happ.
   - Click **«+»** or **«Add subscription»**.
   - Select **«Import from URL»**.
   - Paste the link from Marzban:

     ```text
     https://panel.yourdomain.com/sub/USERNAME/TOKEN
     ```

   - Click **«Import»**.

3. **Connect**

   - A configuration will appear in the list.
   - Select it.
   - Click **«Connect»**.

4. **Check the Connection**

   - Open an IP check website.
   - Make sure the IP has changed.

> [!NOTE]
> (On Linux, it's the same process.)

---

> [!NOTE]
> If you have connection issues in Happ:
> - check that the subscription link is copied in full;
> - try refreshing the subscription in the app;
> - make sure the inbound is active in Marzban.
