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

# \*More projects coming.\*

