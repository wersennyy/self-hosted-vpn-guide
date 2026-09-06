# 📞 Bypassing Whitelists via Calls (Slow but Reliable Method)

## ⚠️ Warning Right Away
This method is **emergency**, not for everyday use. Speed will be low, ping high. But when everything else is blocked — this is one of the few working options. Enough to access social networks.

## 🔍 What is WS (Whitelist)?
When the operator enables **whitelists**, everything is blocked by default. Only sites from the approved list are allowed:
- Gosuslugi, banks
- Yandex, VK, Mail.ru
- Social networks and search engines from the Ministry of Digital Development registry

Regular VPNs (WireGuard, OpenVPN) don't work — their IPs are not in the whitelist, connection is terminated.

### 💡 How It Works
The idea is to route traffic through services that are **already in the whitelist** — video calls:
- **Yandex Telemost**
- **VK Calls** (via VK TURN servers)
- **WB Stream**

Traffic is masked inside a video call. For the operator's DPI systems, it looks like regular VoIP traffic, not a VPN tunnel.

---

## 🛠️ whitelist-bypass (kulikov0)
### What It Is
Open-source tool that creates a SOCKS5 proxy through a video call. Traffic goes through VK/Yandex media relays, so it bypasses whitelists.

### Real Numbers

| Parameter | Value |
|-----------|-------|
| Speed | 50-500 Kbps |
| Ping | 300-800ms |
| For | Text, email, messengers |
| Not for | YouTube, torrents, streaming |

---

## 📱 Setup on Android

### Option 1: whitelist-bypass.apk

**Step 1. Download APK**
- Go to GitHub: [https://github.com/kulikov0/whitelist-bypass/releases](https://github.com/kulikov0/whitelist-bypass/releases)
- Download `whitelist-bypass-vX.X.X.apk` (latest version)

**Step 2. Install**
1. Allow installation from unknown sources:
   - Settings → Security → Unknown sources → ON
   - Or: Settings → Apps → Browser → Install unknown apps → Allow
2. Open downloaded APK → Install

**Step 3. Launch App**
1. Open whitelist-bypass
2. Paste video call link (Telemost/VK)
3. Press **GO**

**Step 4. Configure System Proxy**

**Android 10+**:
1. Settings → Wi-Fi
2. Long press on your network → Modify Network
3. Advanced → Proxy: Manual
4. Host: `127.0.0.1`, Port: `1080`
5. Save

**Android 9 and below**:
1. Settings → Wi-Fi
2. Long press on network → Modify network
3. Show advanced settings → Proxy: Manual
4. Hostname: `127.0.0.1`, Port: `1080`

**Step 5. Verify**
- Open browser
- Go to [https://2ip.ru](https://2ip.ru) or [https://whoer.net](https://whoer.net)
- If it shows server IP — it works!

---

### Option 2: OlcRTC (via Yandex Telemost)

**Links**:
- Client: [https://github.com/Oleglog/Exclave_olcrtc](https://github.com/Oleglog/Exclave_olcrtc)
- Manager: [https://github.com/Oleglog/Olcrtc_manager](https://github.com/Oleglog/Olcrtc_manager)

**Instructions**:
1. Create a call in Yandex Telemost
2. Copy the call link
3. Paste into OlcRTC client
4. Connect

---

## 💻 Setup on Windows

### Desktop version whitelist-bypass

**Step 1. Download**
- GitHub Releases: [https://github.com/kulikov0/whitelist-bypass/releases](https://github.com/kulikov0/whitelist-bypass/releases)
- Download `whitelist-bypass-win-x64.exe` (or .msi)

**Step 2. Install**
1. Run installer
2. Accept license
3. Choose installation folder (default is fine)
4. Install

**Step 3. Launch**
- Open whitelist-bypass from Start menu or desktop

**Step 4. Configure**
1. Paste call link (Telemost/VK/WB Stream)
2. Press **Connect**

**Step 5. Configure System Proxy**

**Windows 10/11**:
1. Settings → Network & Internet → Proxy
2. Turn on "Use a proxy server"
3. Address: `127.0.0.1`, Port: `1080`
4. Save

**Step 6. Verify**
- Open browser → [https://2ip.ru](https://2ip.ru)
- If IP changed — it works!

---

## 🐧 Setup on Linux

### Desktop version (Electron)

**Step 1. Download**
1. Open website: **https://github.com/kulikov0/whitelist-bypass/releases**
2. Find latest release (v0.3.8 or newer)
3. In **Assets** section, download Linux file:
   - `.deb` (for Ubuntu/Debian)

---

**Step 2. Install**

Double-click the file → installs automatically.

---

**Step 3. Launch**
  1. Open applications menu
  2. Find **WhitelistBypass**
  3. Launch

---

**Step 4. Configure System Proxy**

**GNOME (Ubuntu, Fedora)**:
1. Open **Settings** → **Network** → **Network Proxy**
2. Method: **Manual**
3. HTTP/HTTPS/SOCKS Host: `127.0.0.1`, Port: `1080`
4. Click **Apply**

**KDE Plasma**:
1. Open **System Settings** → **Network** → **Proxy**
2. Select **Manual Proxy Configuration**
3. SOCKS Host: `127.0.0.1`, Port: `1080`
4. Click **Apply**

---

**Step 5. Verify**
```bash
curl ifconfig.me
```
- If it shows server IP — it works!

---

## 🍎 iOS

### Via AltStore

**Step 1. Install AltServer on PC**
- Download: [https://altstore.io](https://altstore.io)
- Install on Windows/Mac

**Step 2. Connect iPhone to PC**
- Open AltServer
- Click icon in tray → Install AltStore → Select device

**Step 3. On iPhone**
1. Settings → General → VPN & Device Management
2. Trust developer (your Apple ID)

**Step 4. Download whitelist-bypass.ipa**
- GitHub Releases: [https://github.com/kulikov0/whitelist-bypass/releases](https://github.com/kulikov0/whitelist-bypass/releases)
- Download `.ipa` file

**Step 5. Install via AltStore**
1. Open AltStore on iPhone
2. Press "+" → Select downloaded .ipa
3. Install

**Step 6. Configure SOCKS5 in App**

**Shadowrocket**:
1. Open Shadowrocket
2. + → SOCKS5
3. Server: `127.0.0.1`, Port: `1080`
4. Save → Connect

**NapsternetV**:
1. Open NapsternetV
2. Create new profile → SOCKS5
3. Server: `127.0.0.1`, Port: `1080`
4. Save → Connect

**Step 7. Verify**
- Open Safari → [https://2ip.ru](https://2ip.ru)
- If IP changed — it works!

---

## 📞 Where to Get Call Link

### Yandex Telemost
1. Go to [https://telemost.yandex.ru](https://telemost.yandex.ru)
2. Create new call
3. Copy link
4. Send to yourself in Telegram/email

### VK Calls
1. Open VK → Calls → Create group call
2. Copy link
3. Use in whitelist-bypass

---

## 🔄 How to Extend Connection Life

1. **Change calls**: when connection drops — create new call, update link
2. **Use IPv6**: if hosting provides IPv6, enable in settings (some operators don't block yet)
3. **Combine**: if Telemost is blocked — try VK Calls or WB Stream

---

## 🧪 Testing Operation

1. **Turn off Wi-Fi**, leave only mobile network
2. **Open** site that doesn't work without VPN (YouTube, Discord)
3. **Run** speedtest (expect 50-500 Kbps)
4. **Check** DNS leaks: [https://dnsleaktest.com](https://dnsleaktest.com)

---

## ❓ Common Issues

### "Can't connect to call"
- Check link (must be complete, with `https://`)
- Try different service (VK instead of Telemost)
- Recreate call

### "Proxy doesn't work"
- Check that whitelist-bypass is running
- Restart app
- Check that port `1080` is not occupied by another app

### "Speed is very low"
- This is normal for VoIP tunnels (50-500 Kbps)
- Try different call/service

### "Connection drops after 30 minutes"
- This is limitation of call services themselves
- Recreate call, update link
- Use IPv6 (if available)

---

## 📚 Sources

- whitelist-bypass GitHub: [https://github.com/kulikov0/whitelist-bypass](https://github.com/kulikov0/whitelist-bypass)
- OlcRTC Manager: [https://github.com/Oleglog/Olcrtc_manager](https://github.com/Oleglog/Olcrtc_manager)
- WDTT (WireGuard-over-VK-calls): [https://github.com/kiper292/wireguard-turn-android](https://github.com/kiper292/wireguard-turn-android)

> [!NOTE]
> **Continuation in file *BC-bypass-fast***
