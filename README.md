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

📸 
<img width="1180" height="528" alt="Screenshot 2025-09-30 152915" src="https://github.com/user-attachments/assets/18a9c131-4c32-4020-b55e-d4cadaeebdc0" />
<img width="1665" height="604" alt="Screenshot 2025-09-30 152955" src="https://github.com/user-attachments/assets/e62ef519-dff1-4028-a999-193970de3bfb" />

---

### 2️⃣ Deploy Virtual Machines   
- Place VM in the same Virtual Network.  

📸  
<img width="1161" height="523" alt="Screenshot 2025-09-30 163643" src="https://github.com/user-attachments/assets/eaf9a56f-b747-4e58-9b80-7cf16b4622fc" />

---

### 3️⃣ Configure Network Security Groups (NSGs)  
- Create an **NSG** and attach it to the subnet or VM NICs.  
- Add inbound rules:  
  - ✅ Allow RDP (3389/TCP) from your public IP to the Client VM.  
  - ✅ Allow HTTP (80/TCP) between Client VM and Server VM.  
  - 🚫 Deny ICMP (Ping) traffic.  

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

📸   
<img width="1305" height="696" alt="Screenshot 2025-09-30 164543" src="https://github.com/user-attachments/assets/5010d7e9-a7e3-4f57-a534-7b06ba329d02" />

---

### 5️⃣ Generate and Observe Traffic  
- **🔑 RDP:** Connect from your local computer into the Client VM and observe RDP packets.  
- **🌍 HTTP:** From Client VM, send an HTTP request to Server VM:  
  ```powershell
  curl http://<Server-Private-IP>
