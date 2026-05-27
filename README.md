# Raspberry Pi Homelab

Projects I'm building on my Raspberry Pi as I learn networking, Linux, and security.

---

## Project 1: SSH Hardening

### What I Did

Locked down SSH on my Pi. Generated an ED25519 keypair with a passphrase, deployed it, and disabled password auth entirely. Changed the SSH port from 22 to 2222, disabled root login, and set up fail2ban to ban IPs after 5 failed attempts. Had to troubleshoot fail2ban a bit since my Pi uses systemd for logging instead of traditional log files.

### Why It Matters

Key-based auth eliminates brute force credential attacks since the private key never crosses the network. Changing the port cuts out most automated scanner noise. Disabling root login enforces least privilege so even a successful attacker lands in an unprivileged session. fail2ban adds rate limiting at the IP level, making brute force attempts expensive and slow.

### What I'd Add Next

Port knocking to hide the SSH port entirely, alerting on fail2ban events so I don't have to check logs manually, and eventually SSH certificates instead of managing key files across machines.

---

## Project 2: Pi-hole + Unbound

### What I Did

Set up Pi-hole as a network-wide DNS sinkhole to block ads and trackers at the DNS level. Paired it with Unbound as a recursive DNS resolver so queries get resolved directly by talking to root DNS servers instead of forwarding to Google or Cloudflare. Had to configure Pi-hole to listen on `wlan0` since my Pi is on WiFi, and set Unbound's backend to `127.0.0.1#5335` as Pi-hole's upstream. Since my AT&T gateway doesn't let you change the DNS it hands out via DHCP, I configured DNS per device instead of at the router level.

### Why It Matters

Pi-hole blocks entire ad and tracking domains before they ever reach your device. It works on every app and every device pointed at it, not just one browser. Unbound removes the need to trust a third-party DNS provider with your query history since your Pi resolves domains itself by going straight to the authoritative nameservers. Together they give you ad blocking and DNS privacy across your whole network.

### What I'd Add Next

Setting up Pi-hole as the DHCP server so I don't have to manually configure DNS on each device. Adding more blocklists for better coverage.

---

## Project 3: WireGuard VPN

### What I Did

Installed WireGuard on my Pi so I can tunnel back into my home network from anywhere. Generated server and client keypairs, configured the tunnel on a `10.0.0.0/24` subnet, and set up iptables rules to NAT traffic through `wlan0`. Had to set up port forwarding on my AT&T gateway since WireGuard needs to be reachable from the internet on UDP port 51820. Created a client config and used `qrencode` to generate a QR code so I could scan it with the WireGuard app on my iPhone. The tunnel routes DNS through Pi-hole so I get ad blocking and private DNS even when I'm on cellular or public WiFi.

### Why It Matters

Without a VPN, any traffic on public WiFi is potentially visible to anyone else on that network. WireGuard encrypts everything between my phone and my Pi before it hits the internet. It also means I get Pi-hole's ad blocking everywhere, not just at home. WireGuard is a lot lighter and faster than something like OpenVPN because it has a much smaller codebase and runs in the kernel, which also means less battery drain on mobile.

### What I'd Add Next

Adding more client configs for my laptop and other devices. Setting up dynamic DNS so I don't have to worry if my public IP changes. Looking into kill switch settings on the client side so traffic can't leak if the tunnel drops.

---

*More projects coming.*