# \# Raspberry Pi Homelab

# 

# Projects I'm building on my Raspberry Pi as I learn networking, Linux, and security.

# 

# \---

# 

# \## Project 1: SSH Hardening

# 

# \### What I Did

# 

# Locked down SSH on my Pi. Generated an ED25519 keypair with a passphrase, deployed it, and disabled password auth entirely. Changed the SSH port from 22 to 2222, disabled root login, and set up fail2ban to ban IPs after 5 failed attempts. Had to troubleshoot fail2ban a bit since my Pi uses systemd for logging instead of traditional log files.

# 

# \### Why It Matters

# 

# Key-based auth eliminates brute force credential attacks since the private key never crosses the network. Changing the port cuts out most automated scanner noise. Disabling root login enforces least privilege so even a successful attacker lands in an unprivileged session. fail2ban adds rate limiting at the IP level, making brute force attempts expensive and slow.

# 

# \### What I'd Add Next

# 

# Port knocking to hide the SSH port entirely, alerting on fail2ban events so I don't have to check logs manually, and eventually SSH certificates instead of managing key files across machines.

# 

# \---

# 

# \## Project 2: Pi-hole + Unbound

# 

# \### What I Did

# 

# Set up Pi-hole as a network-wide DNS sinkhole to block ads and trackers at the DNS level. Paired it with Unbound as a recursive DNS resolver so queries get resolved directly by talking to root DNS servers instead of forwarding to Google or Cloudflare. Had to configure Pi-hole to listen on `wlan0` since my Pi is on WiFi, and set Unbound's backend to `127.0.0.1#5335` as Pi-hole's upstream. Since my AT\&T gateway doesn't let you change the DNS it hands out via DHCP, I configured DNS per device instead of at the router level.

# 

# \### Why It Matters

# 

# Pi-hole blocks entire ad and tracking domains before they ever reach your device. It works on every app and every device pointed at it, not just one browser. Unbound removes the need to trust a third-party DNS provider with your query history since your Pi resolves domains itself by going straight to the authoritative nameservers. Together they give you ad blocking and DNS privacy across your whole network.

# 

# \### What I'd Add Next

# 

# Setting up Pi-hole as the DHCP server so I don't have to manually configure DNS on each device. Adding more blocklists for better coverage. Eventually when I set up WireGuard VPN I'll route that traffic through Pi-hole too so I get ad blocking and private DNS even when I'm away from home.

# 

# \---

# 

# \*More projects coming.\*

