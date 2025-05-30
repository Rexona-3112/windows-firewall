
# 🔐 Cyber Security Internship — Task 4: Setup and Use a Firewall on Windows


## 🛠 Tools Used

- Windows Defender Firewall with Advanced Security
- PowerShell (for testing)
- Telnet Client
- TCP Listener using .NET (PowerShell)

---

## 📌 Task Breakdown

### ✅ Step 1: Enable Telnet Client

To test blocking port 23 (used by Telnet), I enabled the Telnet client:

```cmd
dism /online /Enable-Feature /FeatureName:TelnetClient
````

---

### ✅ Step 2: Create Inbound Rule to Block Port 23

1. Open **Windows Defender Firewall with Advanced Security**.
2. Navigate to **Inbound Rules**.
3. Click on **New Rule...**

   * Type: `Port`
   * Protocol: `TCP`
   * Port: `23`
   * Action: `Block the connection`
   * Profile: `All (Domain, Private, Public)`
   * Name: `Block Telnet Port 23`

---

### ✅ Step 3: Create Dummy TCP Listener on Port 23 (PowerShell)

To simulate a service listening on port 23:

```powershell
$listener = [System.Net.Sockets.TcpListener]23
$listener.Start()
```

> ⚠ Keep the PowerShell window open — this makes port 23 active on localhost.

---

### ✅ Step 4: Test Telnet Connection

#### 🔹 Before Blocking

```cmd
telnet 127.0.0.1 23
```

**Result:** Connection successful (blank screen appears) ✅

#### 🔹 After Blocking

```cmd
telnet 127.0.0.1 23
```

**Result:**

```
Connecting To 127.0.0.1...Could not open connection to the host, on port 23: Connect failed
```

> 🎯 Firewall rule successfully blocks the connection!

---

### ✅ Step 5: Remove the Test Rule

After testing:

* Open **Firewall > Inbound Rules**
* Right-click on `Block Telnet Port 23`
* Click **Delete**

---


## 📚 What I Learned

* How to create and manage firewall rules on Windows
* How to test open ports using Telnet and PowerShell
* The significance of port-specific access control
* Practical importance of blocking legacy, insecure protocols (like Telnet)
