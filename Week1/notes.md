# Week 1 - Day 1 Notes

## Goal

Today I set up my Network Detection and Response (NDR) learning environment and captured my first network traffic using Wireshark.

---

# What I Did

## 1. Set up Git and GitHub

* Initialized a local Git repository.
* Connected my local project to my GitHub repository.
* Pulled the existing repository successfully.

Commands used:

```powershell
git init
git remote add origin <repository-url>
git pull origin main --allow-unrelated-histories
```

---

## 2. Installed Wireshark

* Downloaded and installed the latest 64-bit version of Wireshark.
* Used the default installation settings.
* Verified that Wireshark opened successfully.

---

## 3. Identified My Active Network Adapter

At first, I wasn't sure which adapter to capture traffic from because Wireshark listed several interfaces.

To identify the correct one, I ran:

```powershell
ipconfig
```

Output showed:

* Wi-Fi had an IPv4 address.
* Wi-Fi had a Default Gateway.
* Ethernet was disconnected.

From this I learned:

* **Wi-Fi** = Active internet connection
* **Ethernet** = Not connected
* **Local Area Connection*** adapters = Virtual adapters created by Windows

I selected **Wi-Fi** in Wireshark.

---

## 4. Captured Network Traffic

I started a packet capture using the Wi-Fi adapter.

While capturing, I browsed the internet to generate traffic.

After several minutes I stopped the capture and saved it as:

```
Week1/captures/day1_first_capture.pcapng
```

---

# Applying Filters

I applied the display filter:

```
tcp
```

This displayed only TCP traffic.

---

# What I Saw

Most packets contained:

* TCP
* TLSv1.3
* Port 443
* ACK
* Application Data

Example:

```
192.168.0.101  →  2.17.161.59
TCP
58055 → 443
```

---

# What These Mean (Simple Explanation)

## TCP

TCP is a reliable communication protocol.

It makes sure data reaches the other computer correctly.

I think of TCP like sending a package that requires a signature before delivery is confirmed.

---

## ACK

ACK means:

> "I received your data."

It is simply an acknowledgement between two computers.

---

## TLSv1.3

TLS encrypts internet traffic.

Wireshark can see that encrypted data is being exchanged, but it cannot read the contents.

This is normal for HTTPS websites.

---

## Port 443

Port 443 is used for secure HTTPS websites.

Whenever I visit a website like GitHub or Google, I will usually see traffic going to port 443.

---

## Source and Destination

Example:

```
Source:
192.168.0.101
```

This is my computer.

```
Destination:
2.17.161.59
```

This is a server on the internet.

---

# Problems I Encountered

## Problem 1

I didn't know which network adapter to choose.

### Solution

I used:

```powershell
ipconfig
```

to find the adapter with:

* IPv4 Address
* Default Gateway

This confirmed Wi-Fi was my active adapter.

---

## Problem 2

PowerShell returned:

```
tshark : The term 'tshark' is not recognized
```

### Cause

Windows could not find the TShark executable because it was not in the system PATH.

---

## Problem 3

After running TShark using its full path, I received:

```
The file "day1_first_capture.pcapng" doesn't exist.
```

### Cause

I was running the command from the wrong folder.

My capture file was actually located in:

```
Week1/captures/day1_first_capture.pcapng
```

Using the correct file path fixed the issue.

---

# What I Learned

* How to identify the active network adapter.
* The difference between Wi-Fi, Ethernet, and virtual adapters.
* How to capture network traffic using Wireshark.
* How to apply display filters.
* What TCP traffic looks like.
* What ACK packets are.
* Why HTTPS traffic appears as TLS Application Data.
* That encrypted traffic cannot be read without the proper keys.
* How to use TShark from the command line.
* Why file paths are important when opening capture files.

---

# Commands Used

```powershell
ipconfig
```

```powershell
git init
```

```powershell
git remote add origin <repository-url>
```

```powershell
git pull origin main --allow-unrelated-histories
```

```powershell
& "C:\Program Files\Wireshark\tshark.exe" -v
```

```powershell
& "C:\Program Files\Wireshark\tshark.exe" -r ".\Week1\captures\day1_first_capture.pcapng"
```

```powershell
& "C:\Program Files\Wireshark\tshark.exe" -r ".\Week1\captures\day1_first_capture.pcapng" -Y tcp
```

---

# Key Takeaways

* My active network adapter was **Wi-Fi**.
* I successfully captured my first network traffic.
* Most internet traffic today is encrypted using TLS.
* TCP provides reliable communication between devices.
* TShark is the command-line version of Wireshark.
* Correct file paths and understanding error messages are important troubleshooting skills.

---

# Next Steps

* Learn about DNS traffic.
* Capture ICMP (ping) packets.
* Learn how TCP connections are established.
* Analyze more packet captures using both Wireshark and TShark.
* Continue building confidence reading network traffic.
