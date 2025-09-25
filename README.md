# 🔐 Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines  

In this tutorial, we observe network traffic to and from Azure Virtual Machines with **Wireshark** and experiment with **Network Security Groups (NSGs)** to control inbound and outbound traffic.  

---

## 🌐 Environments and Technologies Used  

- ☁️ Microsoft Azure (Virtual Machines, Virtual Network, NSGs)  
- 🧪 Wireshark (Packet Capture Tool)  
- 💻 Remote Desktop Protocol (RDP)  

---

## 🖥️ Operating Systems Used  

- 🪟 Windows 10 (21H2)  
- 🪟 Windows Server 2019  

---

## ⚙️ Steps  

### 1️⃣ Create a Virtual Network and Resource Group  
- Create a new **Resource Group** in Azure.  
- Deploy a **Virtual Network** with one subnet for the VMs.  

📸 *Screenshot Placeholder: Resource Group and VNet Setup*  

---

### 2️⃣ Deploy Two Virtual Machines  
- **VM1 (Client):** Windows 10  
- **VM2 (Server):** Windows Server 2019  
- Place both VMs in the same Virtual Network.  

📸 *Screenshot Placeholder: VM Deployment*  

---

### 3️⃣ Configure Network Security Groups (NSGs)  
- Create an **NSG** and attach it to the subnet or VM NICs.  
- Add inbound rules:  
  - ✅ Allow RDP (3389/TCP) from your public IP to the Client VM.  
  - ✅ Allow HTTP (80/TCP) between Client VM and Server VM.  
  - 🚫 Deny ICMP (Ping) traffic.  

📸 *Screenshot Placeholder: NSG Rules*  

**Example NSG Rules Table:**  

| 🔢 Priority | 🏷️ Rule Name  | 🔌 Port | 📡 Protocol | 🌍 Source    | 🎯 Destination | ⚡ Action |
|-------------|---------------|---------|-------------|--------------|----------------|----------|
| 100         | Allow-RDP     | 3389    | TCP         | My IP        | Client VM      | Allow    |
| 200         | Allow-HTTP    | 80      | TCP         | Client VM    | Server VM      | Allow    |
| 300         | Deny-ICMP     | Any     | ICMP        | Any          | Any            | Deny     |

---

### 4️⃣ Install and Run Wireshark on the Client VM  
- Download and install **Wireshark**.  
- Run Wireshark as **Administrator**.  
- Start a packet capture on the active network adapter.  

📸 *Screenshot Placeholder: Wireshark Running*  

---

### 5️⃣ Generate and Observe Traffic  
- **🔑 RDP:** Connect from your local computer into the Client VM and observe RDP packets.  
- **🌍 HTTP:** From Client VM, send an HTTP request to Server VM:  
  ```powershell
  curl http://<Server-Private-IP>
