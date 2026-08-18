📱 Configuring clients and connecting to our VPN

After we set up the server and configured the 3x-ui panel, it’s time to connect our devices. The biggest challenge for me was finding a decent client that works equally well everywhere.

In the end, I settled on the Happ (Proxy Utility) app. It’s open‑source, doesn’t drain the battery, and handles the VLESS + Reality protocol perfectly on Windows, Linux, and iOS.
📥 Step 1. Where to get and how to install the clients ↓

    🪟 Windows: Download the official release of Happ; here’s the link to their website, where you can download it for all devices: https://www.happ.su/main/ru.
    🍏 iOS (iPhone): Search for Happ (Proxy Utility) directly in the App Store (if you’re from Russia, you’ll need to change the region in the App Store; you can change it back later). The app is free.
    🐧 Linux: Download the version in the format; it’s also available on their website.

Step 2. Quick connection via QR code

You won't have to rewrite the keys or settings by hand at all. The 3x-ui panel does everything automatically.

    Go to the 3x-ui panel via a browser and open the Inbounds tab.
    Find the created connection and click on the QR code icon (or the Info button).
    Open the Happ app on your device:
        On the phone: Click the add configuration button and select "Scan QR code". Point the camera at the monitor.
        On PC: If the panel is open on the same computer, copy the text link vless://... from the panel, and in Happ click “Import from clipboard”.
    All complex encryption settings, ports, and Reality masking are imported instantly!

🛠️ Analysis of common bugs when connecting
❌ Problem 1: the QR code was scanned, but the internet is not working (Endless loading)

    What’s going on: Most likely, your server has blocked this port within its system, or you forgot to enable the connection in the panel itself.
    How to fix:
        Make sure that in the 3x-ui panel, the green status (Active) is displayed next to your client.
        Check whether port 51820 is open on the server. Enter the following command in the server’s terminal: sudo ufw allow 51820/tcp.

❌ Problem 2: On Windows, the internet drops out after closing Happ.

    What’s the issue: the app enables the system proxy server, and when the program is closed abruptly, Windows doesn’t have time to revert the settings.
How to fix: always turn off the VPN using the Disconnect / Stop button inside the app before closing the window itself. If the internet connection has already dropped, go to the Windows system settings -> “Network and Internet” -> “Proxy” and manually disable the “Use proxy server” toggle.

❌ Problem 3: on iOS (iPhone), the VPN turns off automatically in the background.

    What’s the issue: The power‑saving mode on the iPhone is too strict and kills heavy processes.
    How to fix: Go to the Happ settings and make sure that Xray Core is selected as the engine (it works natively and is as stable as possible in the background). Disable the strict battery‑saving mode for the app.

📈 How to check that everything is working?
After clicking the Connect button, open any browser and go to the website https://whatismyipaddress.com/. If you see your server’s address from Hostkey in the “Your IP” field, and the name of your home internet provider is missing from the “Provider” field — congratulations, you’re completely safe!
