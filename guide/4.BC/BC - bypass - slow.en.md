# 📞 Bypassing Whitelists via Video Calls (Slow but Reliable Method)

## ⚠️ Quick Warning
This method is for **emergency use only**, not for daily browsing. Speed will be low, ping will be high. But when everything else is blocked — this is one of the few working options. Enough to check social media.

## 🔍 What Are Whitelists?
When your ISP enables **whitelist mode**, everything is blocked by default. Only approved sites are accessible:
- Government portals, banks
- Yandex, VK, Mail.ru
- Social networks and search engines from the official registry

Regular VPNs (WireGuard, OpenVPN) don't work — their IPs aren't in the whitelist, connections get dropped.

### 💡 How It Works
The idea is to route traffic through services that **are already whitelisted** — video calls:
- **Yandex Telemost**
- **VK Calls** (via VK TURN servers)
- **WB Stream**

Traffic is tunneled inside a video call. For the ISP's DPI systems, it looks like regular VoIP traffic, not a VPN tunnel.

---

## 🛠️ whitelist-bypass (kulikov0)

### What Is It
Open-source tool that creates a SOCKS5 proxy through a video call. Traffic goes through VK/Yandex media relays, so it bypasses whitelists.

### Real-World Numbers

| Parameter | Value |
|-----------|-------|
| Speed | 50-500 Kbps |
| Ping | 300-800ms |
| Lifetime | 1-3 hours |
| Good for | Text, email, messengers |
| Not for | YouTube, torrents, streaming |

---

## 📱 Android Setup

### Option 1: whitelist-bypass.apk

**Step 1. Download APK**
- Go to GitHub: [https://github.com/kulikov0/whitelist-bypass/releases](https://github.com/kulikov0/whitelist-bypass/releases)
- Download `whitelist-bypass-vX.X.X.apk` (latest version)

**Step 2. Install**
1. Allow installation from unknown sources:
   - Settings → Security → Unknown Sources → ON
   - Or: Settings → Apps → Browser → Install unknown apps → Allow
2. Open downloaded APK → Install

**Step 3. Launch App**
1. Open whitelist-bypass
2. Paste video call link (Telemost/VK)
3. Press **GO**

**Step 4. Configure System Proxy**

**Android 10+**:
1. Settings → Wi-Fi
2. Long press your network → Modify Network
3. Advanced → Proxy: Manual
4. Host: `127.0.0.1`, Port: `1080`
5. Save

**Android 9 and below**:
1. Settings → Wi-Fi
2. Long press network → Modify Network
3. Show Advanced → Proxy: Manual
4. Proxy Host: `127.0.0.1`, Proxy Port: `1080`

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

## 💻 Windows Setup

### Desktop Version (whitelist-bypass)

**Step 1. Download**
- GitHub Releases: [https://github.com/kulikov0/whitelist-bypass/releases](https://github.com/kulikov0/whitelist-bypass/releases)
- Download `whitelist-bypass-win-x64.exe` (or .msi)

**Step 2. Install**
1. Run installer
2. Accept license
3. Choose install folder (default is fine)
4. Install

**Step 3. Launch**
- Open whitelist-bypass from Start Menu or Desktop

**Step 4. Configure**
1. Paste call link (Telemost/VK/WB Stream)
2. Press **Connect**

**Step 5. Configure System Proxy**

**Windows 10/11**:
1. Settings → Network & Internet → Proxy
2. Turn ON "Use a proxy server"
3. Address: `127.0.0.1`, Port: `1080`
4. Save

**Step 6. Verify**
- Open browser → [https://2ip.ru](https://2ip.ru)
- If IP changed — it works!

---

## 🐧 Linux Setup

### Desktop Version (Electron)

**Step 1. Download**
```bash
cd ~/Downloads
wget https://github.com/kulikov0/whitelist-bypass/releases/latest/download/whitelist-bypass-linux-x64.tar.gz
```

**Step 2. Extract**
```bash
tar -xzf whitelist-bypass-linux-x64.tar.gz
cd whitelist-bypass
```

**Step 3. Launch**
```bash
./whitelist-bypass
```

**Step 4. Configure System Proxy**

**GNOME (Ubuntu, Fedora)**:
1. Settings → Network → Network Proxy
2. Method: Manual
3. HTTP/HTTPS/SOCKS Host: `127.0.0.1`, Port: `1080`
4. Apply

**KDE Plasma**:
1. System Settings → Network → Proxy
2. Manual Proxy Configuration
3. SOCKS Host: `127.0.0.1`, Port: `1080`
4. Apply

**Step 5. Verify**
```bash
curl ifconfig.me
```
- If it shows server IP — it works!

---

## 🍎 iOS Setup

### Via AltStore

**Step 1. Install AltServer on PC**
- Download: [https://altstore.io](https://altstore.io)
- Install on Windows/Mac

**Step 2. Connect iPhone to PC**
- Open AltServer
- Click tray icon → Install AltStore → Select device

**Step 3. On iPhone**
1. Settings → General → VPN & Device Management
2. Trust developer (your Apple ID)

**Step 4. Download whitelist-bypass.ipa**
- GitHub Releases: [https://github.com/kulikov0/whitelist-bypass/releases](https://github.com/kulikov0/whitelist-bypass/releases)
- Download `.ipa` file

**Step 5. Install via AltStore**
1. Open AltStore on iPhone
2. Tap «+» → Select downloaded .ipa
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

## 📞 Where to Get Call Links

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

## 🔄 How to Extend Connection Lifetime

1. **Rotate calls**: when connection drops — create new call, update link
2. **Use IPv6**: if your host provides IPv6, enable it (some ISPs don't block it yet)
3. **Combine services**: if Telemost is blocked — try VK Calls or WB Stream

---

## 🧪 Testing

1. **Disable Wi-Fi**, use mobile data only
2. **Open** a site that doesn't work without VPN (YouTube, Discord)
3. **Run** speedtest (expect 50-500 Kbps)
4. **Check** DNS leaks: [https://dnsleaktest.com](https://dnsleaktest.com)

---

## ❓ Troubleshooting

### "Can't connect to call"
- Check link (must be complete, with `https://`)
- Try different service (VK instead of Telemost)
- Recreate the call

### "Proxy not working"
- Make sure whitelist-bypass is running
- Restart the app
- Check if port `1080` isn't used by another app

### "Speed is very low"
- This is normal for VoIP tunnels (50-500 Kbps)
- Try different call/service

### "Connection drops after 30 minutes"
- This is a limitation of the call services themselves
- Recreate call, update link
- Try IPv6 (if available)

---

## 📚 Sources

- whitelist-bypass GitHub: [https://github.com/kulikov0/whitelist-bypass](https://github.com/kulikov0/whitelist-bypass)
- OlcRTC Manager: [https://github.com/Oleglog/Olcrtc_manager](https://github.com/Oleglog/Olcrtc_manager)
- WDTT (WireGuard-over-VK-calls): [https://github.com/kiper292/wireguard-turn-android](https://github.com/kiper292/wireguard-turn-android)
