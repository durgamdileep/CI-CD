# 🔒 Why Jenkins Should Not Run as Root on EC2

- Jenkins should not run as root on EC2 servers because it poses a **major security risk** — if Jenkins is compromised, an attacker would get **full root access** to the server.

### 1️⃣ Jenkins is exposed to the outside world

- 🌐 Jenkins usually has a **web interface (port 8080)**  
- 📝 It can execute scripts, build jobs, download code from Git, etc.  
- ⚠️ If Jenkins runs as root, any vulnerability in plugins or jobs gives **full system control** to an attacker  
- 💀 Risk: They could delete files, modify system configs, or even compromise other connected systems

### 2️⃣ Least Privilege Principle

- 🔑 Security best practice: always run services with the **minimum privileges needed**  
- 🤖 Jenkins doesn’t need full root access to do its job:  
  - 📂 Checkout code  
  - 🏗️ Build software  
  - 🧪 Run tests  
  - 🐳 Interact with Docker (via Docker group)  

- ✅ So running as **jenkins user** follows this principle


### 3️⃣ Safer Access to Docker

- 🐳 Jenkins can run Docker commands without being root by **adding jenkins to the docker group**  
- 🛡️ This gives just enough permission to manage containers, but **not full root access** to the entire server

### 4️⃣ Prevent Accidental System Damage

- ⚡ Jobs often execute scripts from SCM  
- ⚠️ If Jenkins runs as root and a script is buggy/malicious, it could:  
  - ❌ Delete /etc  
  - ❌ Format disks  
  - ❌ Break the server  

- 🏠 Running as **jenkins** limits the damage to only the Jenkins **home directory** and Docker containers

### 5️⃣ Industry Best Practices

- 🏢 On production EC2 servers: **never run Jenkins as root**  
- ⚠️ Plugins and jobs may be compromised — running as root is a **huge security risk**  
- ✅ Always run as **jenkins user + Docker group** for container access

---

### 6️⃣ Exception (rare)

- ⚙️ For initial setup, installation commands may require **sudo or root access**  
- 🚫 But Jenkins **service itself should never run as root**
