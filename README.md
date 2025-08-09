# *wsl-kali-setup-guide*
### *Turn your Windows machine into a Kali Linux playground with WSL 2 – complete setup and fixes included.*

<br>

# 🐧 Installing WSL and Kali Linux on Windows 10/11 (Full Guide)

This guide will walk you through setting up **Windows Subsystem for Linux (WSL)** from scratch until you have **Kali Linux** installed and running.  
It also includes troubleshooting for the **"WSL2 is not supported"** error.

---

## 📌 1. Check if WSL is Installed

Open **Command Prompt** or **PowerShell** and run:

```powershell
wsl --list --verbose
```

- If you see:
  ```
  Windows Subsystem for Linux has no installed distributions.
  ```
  → WSL is installed, but no Linux distro is installed yet.
- If you see:
  ```
  'wsl' is not recognized...
  ```
  → WSL is not installed, proceed to step 2.

---

## 📌 2. Install WSL (Core System)

Run **PowerShell as Administrator** and enter:

```powershell
wsl --install --no-distribution
```

This will install the WSL engine without any Linux distro.

---

## 📌 3. Enable Required Windows Features

### 3.1 Enable **Virtual Machine Platform**
```powershell
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

### 3.2 Enable **Windows Subsystem for Linux**
```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

---

## 📌 4. Enable Virtualization in BIOS

1. Restart your computer.
2. Enter your BIOS/UEFI settings (usually by pressing `F2`, `F10`, `Delete`, or `Esc` during boot).
3. Find and enable:
   - **Intel VT-x** (for Intel CPUs)
   - **AMD-V** (for AMD CPUs)
4. Save changes and exit BIOS.

---

## 📌 5. Set WSL 2 as the Default Version

Back in Windows, open **PowerShell (Admin)** and run:

```powershell
wsl --set-default-version 2
```

You can verify your WSL version with:
```powershell
wsl --version
```

---

## 📌 6. List Available Linux Distributions

```powershell
wsl --list --online
```

Example output:
```
NAME            FRIENDLY NAME
Ubuntu          Ubuntu
Debian          Debian GNU/Linux
kali-linux      Kali Linux Rolling
```

---

## 📌 7. Install Kali Linux

```powershell
wsl --install -d kali-linux
```

If successful, WSL will:
- Download Kali Linux from the Microsoft Store
- Set it up
- Ask you to create a **username** and **password**

---

## 📌 8. Launch Kali Linux

You can start Kali Linux in two ways:
- From Command Prompt:
  ```powershell
  wsl -d kali-linux
  ```
- From Windows Start Menu: Search for **"Kali Linux"** and open it.

---

## 📌 9. Troubleshooting

### ❌ Error: `WSL2 is not supported with your current machine configuration`
**Cause:** Virtual Machine Platform is not enabled, or virtualization is disabled in BIOS.

**Fix:**
1. Run:
   ```powershell
   dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
   dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
   ```
2. Enable virtualization in BIOS (Step 4).
3. Restart your PC and try again.

---

## 📌 10. Upgrading from WSL 1 to WSL 2 (Optional)

If Kali installs under WSL 1 and you want to upgrade:

```powershell
wsl --set-version kali-linux 2
```

---

## 📌 11. Useful Commands

- List installed distros:
  ```powershell
  wsl --list --verbose
  ```
- Set default distro:
  ```powershell
  wsl --set-default <DistroName>
  ```
- Remove a distro:
  ```powershell
  wsl --unregister <DistroName>
  ```

---

## ✅ Final Notes

- WSL 2 offers better performance and full Linux kernel support.
- Kali Linux on WSL is great for penetration testing, learning Linux, and development.
- Keep Windows updated for the latest WSL features.

---

**Author:**  *John Joshua Manalo Escarez (Haruki Akane)*

