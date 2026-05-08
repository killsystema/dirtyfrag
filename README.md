# 💥 DirtyFrag — Linux Kernel Local Privilege Escalation

<div align="center">

![Linux](https://img.shields.io/badge/Platform-Linux-orange?style=for-the-badge\&logo=linux)
![Kernel](https://img.shields.io/badge/Kernel-5.x--6.x-red?style=for-the-badge)
![Exploit](https://img.shields.io/badge/Type-LPE-success?style=for-the-badge)
![License](https://img.shields.io/badge/License-GPLv2-blue?style=for-the-badge)

### Local Privilege Escalation (User ➜ Root)

DirtyFrag demonstrates Linux kernel privilege escalation techniques involving the ESP and rxrpc subsystems.

> Educational and authorized security research only.

</div>

---

# 📚 Table of Contents

* [Overview](#-overview)
* [Features](#-features)
* [Affected Systems](#-affected-systems)
* [Installation](#-installation)
* [Compilation](#-compilation)
* [Usage](#-usage)
* [How It Works](#-how-it-works)
* [Detection](#-detection)
* [Mitigation](#-mitigation)
* [FAQ](#-faq)
* [Disclaimer](#-disclaimer)
* [License](#-license)

---

# 🎯 Overview

DirtyFrag chains multiple Linux kernel attack surfaces to achieve:

* Arbitrary page cache modification
* Local privilege escalation
* User ➜ root transition

## Attack Paths

| Path          | Target        | Reliability |
| ------------- | ------------- | ----------- |
| ESP / AF_ALG  | `/usr/bin/su` | ⭐⭐⭐⭐⭐       |
| rxrpc / rxkad | `/etc/passwd` | ⭐⭐⭐⭐        |

---

# ⚡ Features

* Local privilege escalation research
* Kernel page cache corruption
* Namespace isolation support
* Multiple exploit paths
* Safe vulnerability scanner
* Automated mitigation mode
* Cross-distribution compatibility

---

# 🖥️ Affected Systems

| Kernel Version | Status                  |
| -------------- | ----------------------- |
| 5.0 → 5.15     | 🔴 Vulnerable           |
| 5.16 → 6.5     | 🟠 Partially Vulnerable |
| 6.6+           | 🟢 Patched              |

## Tested Distributions

* Ubuntu 20.04 / 22.04
* Debian 11 / 12
* Fedora 36+
* Arch Linux
* Kali Linux

---

# 📥 Installation

## Clone Repository

```bash
git clone https://github.com/yourusername/dirtyfrag.git
cd dirtyfrag
```

## Direct Download

```bash
wget https://github.com/yourusername/dirtyfrag/releases/latest/download/dirtyfrag
chmod +x dirtyfrag
```

---

# 🛠️ Compilation

## Debian / Ubuntu / Kali

```bash
sudo apt update
sudo apt install gcc make libc6-dev
```

## Fedora / RHEL

```bash
sudo dnf install gcc make glibc-devel
```

## Arch Linux

```bash
sudo pacman -S gcc make glibc
```

## Build

```bash
gcc -O0 -Wall -o dirtyfrag dirtyfrag.c -lutil
```

## Debug Build

```bash
gcc -O0 -Wall -g -o dirtyfrag dirtyfrag.c -lutil -DDIRTYFRAG_DEBUG
```

## Static Build

```bash
gcc -static -O0 -Wall -o dirtyfrag dirtyfrag.c -lutil
```

---

# 🚀 Usage

## Exploit

```bash
./dirtyfrag
```

## Scan System

```bash
./dirtyfrag --scan
```

## Apply Mitigation

```bash
sudo ./dirtyfrag --fix
```

## Verbose Mode

```bash
./dirtyfrag --verbose
```

---

# 🔬 Advanced Options

## Force Specific Path

```bash
./dirtyfrag --force-esp
./dirtyfrag --force-rxrpc
```

## Custom Brute Force

```bash
LPE_MAX_ITERS=50000000 ./dirtyfrag
```

## Reproducible Execution

```bash
LPE_SEED=0x12345678 ./dirtyfrag
```

---

# 🔧 How It Works

## Exploitation Flow

```text
User Namespace
        ↓
CAP_NET_ADMIN
        ↓
ESP / rxrpc Trigger
        ↓
Page Cache Corruption
        ↓
Privilege Escalation
        ↓
Root Shell
```

## Components

### ESP Path

* XFRM state manipulation
* ESN replay abuse
* splice() interaction
* `/usr/bin/su` corruption

### rxrpc Path

* rxkad authentication abuse
* fcrypt brute-force
* `/etc/passwd` corruption

---

# 🔍 Detection

## Check Kernel Version

```bash
uname -r
```

## Check Loaded Modules

```bash
lsmod | grep -E "esp[46]|rxrpc"
```

## Scan System

```bash
./dirtyfrag --scan
```

---

# 🛡️ Mitigation

## Immediate Response

```bash
sudo rmmod esp4 esp6 rxrpc
```

## Blacklist Modules

```bash
sudo bash -c 'cat > /etc/modprobe.d/dirtyfrag-blacklist.conf << EOF
install esp4 /bin/false
install esp6 /bin/false
install rxrpc /bin/false
EOF'
```

## Clear Page Cache

```bash
echo 3 | sudo tee /proc/sys/vm/drop_caches
```

## Reboot

```bash
sudo reboot
```

---

# ❓ FAQ

### Does this require root?

No. The escalation starts from an unprivileged user.

### Is this persistent after reboot?

No. Changes are lost after reboot.

### Is this legal?

Only for systems you own or are explicitly authorized to test.

### Does this work inside containers?

Partially. Depends on namespace and seccomp configuration.

---

# ⚠️ Disclaimer

This project is provided strictly for:

* Educational purposes
* Defensive security research
* Authorized penetration testing

The authors assume no liability for misuse or damages caused by this software.

---

# 📜 License

GNU General Public License v2.0

---

<div align="center">

⭐ Star the repository if this project helped your research.

Made for Linux security research 🔥

</div>
