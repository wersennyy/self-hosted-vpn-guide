# ⚡ Quick Bypass Methods (September 2026)
## 🎯 What Works Right Now

Three working methods. Ranked from best to simplest:

**🥇 1st Place: VLESS + XHTTP (CDN)**
- Setup: 10 minutes
- Speed: 50-200 Mbps
- Lifetime: 5-10 hours
- Bypasses whitelists: ✅

**🥈 2nd Place: Hysteria2**
- Setup: 7 minutes
- Speed: 100-300 Mbps
- Lifetime: 4-8 hours
- Bypasses whitelists: ✅

**🥉 3rd Place: AmneziaWG**
- Setup: 5 minutes
- Speed: 50-150 Mbps
- Lifetime: 2-4 hours
- Bypasses whitelists: ⚠️ (not always)

**❌ Dead Methods**: WireGuard, OpenVPN, VLESS+Reality, Shadowsocks

---

## 1️⃣ VLESS + XHTTP via CDN (Best)

### What Is It

Traffic goes through a Russian CDN (Yandex, VK, Selectel). The ISP thinks you're visiting a Russian site — IP is whitelisted, no blocking.

### How to Install

1. **Download script**:
```bash
wget https://raw.githubusercontent.com/ServerTechnologies/proxy-via-russian-cdn/main/install.sh
```

2. **Run**:
```bash
bash install.sh
```

3. **Answer questions**:
   - Which CDN? (choose Yandex / VK / Selectel)
   - Domain? (enter any, can be free)
   - Server IP? (enter your VPS IP)

4. **Done!** Script does everything automatically.

### Lifetime

5-10 hours. If stops working — run script again with new CDN.

---

## 2️⃣ Hysteria2 (Fast)

### What Is It

Works over new QUIC protocol (like HTTP/3). ISPs haven't learned to block this yet.

### How to Install

1. **Run one command**:
```bash
bash <(curl -fsSL https://raw.githubusercontent.com/HyNetwork/hysteria/main/scripts/install.sh)
```

2. **Answer questions**:
   - Port? (press Enter, keep 443)
   - Domain? (enter any)
   - Masquerade? (type `yes`)

3. **Done!**

### Lifetime

4-8 hours.

---

## 3️⃣ AmneziaWG (Simple)

### What Is It

Regular WireGuard, but with anti-blocking protection. Masks as normal traffic.

### How to Install

1. **Run one command**:
```bash
wget https://raw.githubusercontent.com/bivlked/amneziawg-installer/main/install.sh
bash install.sh
```

2. **Done!** Script configures everything.

### Lifetime

2-4 hours. Then need to recreate server.

---

## 🧩 What Should a Beginner Choose?

**Advice**:
- **First time**: use AmneziaWG (easiest)
- **Want long-term**: use VLESS + XHTTP (CDN)
- **Need speed**: use Hysteria2

**Ideal**: install all three. If one dies — switch to another.

---

## 📊 Simple Comparison

| Method | Speed | Lifetime | Whitelists | Difficulty |
|--------|-------|----------|------------|------------|
| VLESS+XHTTP | 50-200 Mbps | 5-10 h | ✅ | Hard |
| Hysteria2 | 100-300 Mbps | 4-8 h | ✅ | Medium |
| AmneziaWG | 50-150 Mbps | 2-4 h | ⚠️ | Easy |

---

## 📚 Links

- VLESS + XHTTP: [https://github.com/ServerTechnologies/proxy-via-russian-cdn](https://github.com/ServerTechnologies/proxy-via-russian-cdn)
- Hysteria2: [https://github.com/HyNetwork/hysteria](https://github.com/HyNetwork/hysteria)
- AmneziaWG: [https://github.com/bivlked/amneziawg-installer](https://github.com/bivlked/amneziawg-installer)
