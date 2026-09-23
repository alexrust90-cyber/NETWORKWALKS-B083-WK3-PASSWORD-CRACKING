### **1. Introduction**

As part of Week 3 of my Cybersecurity & Ethical Hacking internship with Networkwalks, I worked with **HexStrike-AI**, **MCP (Model Context Protocol)**, and **Claude Desktop** in a Kali Linux virtual machine.

The goal was to create a local environment where Claude Desktop could communicate with HexStrike through MCP and access security tools available in the authorized lab environment.

This document focuses on the **installation, configuration, connection, and verification process**. It is kept separate from the main Week 3 project report.

---

### **2. Objective**

The setup was designed to establish the following communication flow:

```text
Claude Desktop
      ↓
     MCP
      ↓
hexstrike_mcp.py
      ↓
HTTP connection
      ↓
HexStrike API Server
      ↓
Security tools
```

The purpose of this setup was to understand how an AI interface can communicate with security tooling through an MCP-based integration.

---

### **3. Tools and Technologies**

| Component | Purpose |
| --- | --- |
| Kali Linux | Cybersecurity testing environment |
| Claude Desktop | AI interface |
| HexStrike-AI | Security-tool integration platform |
| MCP | Communication protocol between the AI client and tools |
| `hexstrike_server.py` | HexStrike API server |
| `hexstrike_mcp.py` | MCP component used to connect Claude with HexStrike |
| Python 3 | Runtime environment |
| Python virtual environment | Isolated Python environment |
| Kali security tools | Tools available to the authorized lab environment |

---

### **4. Lab Scope**

All testing was performed in an authorized cybersecurity training environment.

The tools described in this document should only be used against systems, files, networks, and accounts for which the tester has explicit permission.

This guide documents the technical setup only. It does not provide authorization to test third-party systems.

---

### **5. Security and Privacy Considerations**

Before publishing this guide to a public repository, sensitive information should be removed from commands, configuration files, terminal output, and screenshots.

### Never publish:

* API keys
* Access tokens
* Authentication credentials
* Passwords
* Private SSH keys
* Session cookies
* Personal email addresses
* Personal usernames where unnecessary
* Private IP addresses
* Public IP addresses if they identify your environment
* VPN addresses or internal network information
* Machine-specific identifiers
* Claude or other service account information
* Full configuration files containing secrets
* Screenshots showing credentials or tokens

If a screenshot contains this type of information, **redact it before uploading it to GitHub**.

### Recommended replacement

For documentation, use placeholders such as:

```text
YOUR_API_KEY_HERE
YOUR_USERNAME
YOUR_PASSWORD
YOUR_PRIVATE_IP
YOUR_PUBLIC_IP
YOUR_PROJECT_PATH
```

Do not replace a real secret with another real secret. Use an obvious placeholder instead.

---

### **6. Prerequisites**

The lab environment requires:

* Kali Linux
* Internet connectivity
* Python 3
* Git
* `curl`
* `sudo` access
* Claude account
* Sufficient disk space
* A separate Python virtual environment for HexStrike

The exact installation commands can vary depending on the operating-system version and package availability.

---

### **7. Installing Claude Desktop**

The following section documents the installation method used in the lab environment.

 ***7.1 Add the package signing key***

```bash
curl -fsSL https://pkg.claude-desktop-debian.dev/KEY.gpg | sudo gpg --dearmor -o /usr/share/keyrings/claude-desktop.gpg
```

This downloads the repository's signing key and stores it in the system keyring.

 ***7.2 Add the package repository***

```bash
echo "deb [signed-by=/usr/share/keyrings/claude-desktop.gpg arch=amd64,arm64] https://pkg.claude-desktop-debian.dev stable main" | sudo tee /etc/apt/sources.list.d/claude-desktop.list
```

This adds the package repository to the system's APT sources.

***7.3 Update package information***

```bash
sudo apt update
```

***7.4 Install Claude Desktop***

```bash
sudo apt install claude-desktop
```

In the lab environment, the installed executable was:

```bash
claude-desktop-unofficial
```

It could be launched with:

```bash
claude-desktop-unofficial
```
---

### **8. Install HexStrike-AI**

Clone the project repository:

```bash
git clone https://github.com/0x4m4/hexstrike-ai.git
```

Move into the project directory:

```bash
cd ~/hexstrike-ai
```

This creates a local copy of the HexStrike-AI project.

---

### **9. Create a Python Virtual Environment**

Create a dedicated virtual environment:

```bash
python3 -m venv hexstrike-env
```

Activate it:

```bash
source hexstrike-env/bin/activate
```

The terminal prompt should indicate that the environment is active, for example:

```text
(hexstrike-env)
```

The virtual environment keeps the project's Python dependencies separate from the rest of the Kali installation.

---

### **10. Install Python Dependencies**

With the virtual environment activated:

```bash
pip3 install -r requirements.txt
```

This installs the Python packages required by the project.

After installation, the environment should contain the dependencies needed to run the HexStrike components.

---

### **11. Start the HexStrike API Server**

Start the server with:

```bash
python3 hexstrike_server.py
```

The server runs locally and listens on:

```text
http://localhost:8888
```

Here:

* `localhost` means the service is running on the same Kali machine.
* `8888` is the TCP port used by the HexStrike API server.

Keep this terminal running while using the MCP connection.

### Important

Do not replace `localhost` with your actual private or public IP address unless there is a specific reason to do so.

Using:

```text
http://localhost:8888
```

is preferable for a local setup because it avoids exposing the service unnecessarily.

---

### **12. Understanding the Main Components**

There are two important Python components in this setup.

### `hexstrike_server.py`

This starts the HexStrike API server.

It provides the local service that the MCP component communicates with.

### `hexstrike_mcp.py`

This provides the MCP connection between the AI client and the HexStrike API server.

The basic communication path is:

```text
Claude Desktop
      ↓
hexstrike_mcp.py
      ↓
http://localhost:8888
      ↓
hexstrike_server.py
      ↓
HexStrike tools
```

This separation makes it easier to understand which component is responsible for each part of the setup.

---

### **13. Test the HexStrike MCP Connection**

Before configuring Claude Desktop, the MCP component can be tested manually.

Use the Python interpreter from the HexStrike virtual environment:

```bash
/home/kali/hexstrike-ai/hexstrike-env/bin/python \
/home/kali/hexstrike-ai/hexstrike_mcp.py \
--server http://localhost:8888
```

A successful connection should show messages indicating that:

* The HexStrike API server was reached.
* The server health status was checked.
* The server version was detected.
* The MCP server started.
* The MCP server is ready to serve AI agents.

For example, output may contain messages similar to:

```text
Successfully connected to HexStrike AI API Server
Server health status: healthy
Server version: [VERSION]
Starting HexStrike AI MCP server
Ready to serve AI agents
```

The exact version number and output may change between releases.

---

### **14. Verify the Local Server**

The server can be checked from another terminal.

Check whether port `8888` is listening:

```bash
ss -lntp | grep 8888
```

You can also test the local health endpoint:

```bash
curl http://localhost:8888/health
```

A successful response should indicate that the HexStrike server is healthy.

The exact response can vary depending on the version installed.

### Why use `localhost`?

Using:

```text
localhost
```

keeps the communication local to the Kali machine.

This is preferable to exposing the API server to the wider network when external access is not required.

> **Security note:** Do not replace `localhost` with your real network address in public documentation unless the configuration specifically requires it.

---

### **15. Configure Claude Desktop's MCP Connection**

Claude Desktop needs to know where the MCP server is located and which Python environment should be used to start it.

The configuration file used in the lab was:

```text
~/.config/Claude/claude_desktop_config.json
```

Create or edit the configuration file:

```bash
nano ~/.config/Claude/claude_desktop_config.json
```

Use the following **public-safe configuration structure**:

```json
{
  "mcpServers": {
    "hexstrike-ai": {
      "command": "/home/kali/hexstrike-ai/hexstrike-env/bin/python",
      "args": [
        "/home/kali/hexstrike-ai/hexstrike_mcp.py",
        "--server",
        "http://localhost:8888"
      ]
    }
  }
}
```

### What each part means

#### `mcpServers`

Defines the MCP servers available to Claude Desktop.

#### `hexstrike-ai`

The local name assigned to this MCP connection.

This name can be changed if desired.

#### `command`

Specifies which Python interpreter should be used.

In this setup, it points to the Python executable inside the HexStrike virtual environment.

#### `args`

These are the arguments passed to Python.

They tell Python to:

1. Run `hexstrike_mcp.py`.
2. Connect to the local HexStrike API server.
3. Use port `8888`.

---

### **16. Validate the JSON Configuration**

Before starting Claude Desktop, check that the configuration file contains valid JSON:

```bash
python3 -m json.tool ~/.config/Claude/claude_desktop_config.json >/dev/null && echo "JSON is valid"
```

Expected result:

```text
JSON is valid
```

This helps detect missing commas, brackets, quotation marks, or other JSON formatting problems.

---

### **17. Restart Claude Desktop**

After modifying the MCP configuration, Claude Desktop should be completely closed and restarted.

To stop the running process:

```bash
pkill -f claude-desktop
```

Check whether any related process remains:

```bash
pgrep -af claude-desktop
```

Then start Claude Desktop again:

```bash
claude-desktop-unofficial
```

A restart is important because the MCP configuration is normally loaded when Claude Desktop starts.

---

### **18. Check the MCP Configuration**

The Claude Desktop diagnostic command can be used to check the configuration:

```bash
claude-desktop-unofficial --doctor
```

The diagnostic output should indicate that the MCP configuration is valid.

For example:

```text
[PASS] MCP config: valid JSON
MCP servers configured: 1
```

The exact diagnostic output can change between versions.

---

### **19. Verify the HexStrike MCP Server in Claude Desktop**

Open Claude Desktop and check the MCP/local-server settings.

The configured server should appear as:

```text
hexstrike-ai
```

Claude should then be able to detect the tools exposed through the HexStrike MCP connection.

In the lab environment, approximately **150 tools** were detected.

The exact number may differ depending on:

* HexStrike version
* Installed security tools
* MCP configuration
* Available dependencies
* Operating-system environment

Therefore, the number of tools should be treated as an example rather than a fixed requirement.

---

### **20. Normal Startup Procedure**

Once the configuration is complete, the normal workflow is simpler.

***Terminal 1 — Start HexStrike***

```bash
cd ~/hexstrike-ai
source hexstrike-env/bin/activate
python3 hexstrike_server.py
```

Leave this terminal running.

***Terminal 2 — Start Claude Desktop***

```bash
claude-desktop-unofficial
```

Claude Desktop can then launch the configured MCP component using the configuration file.

The communication path becomes:

```text
Claude Desktop
      ↓
MCP configuration
      ↓
hexstrike_mcp.py
      ↓
localhost:8888
      ↓
HexStrike API
      ↓
Security tools
```

---

### **21. Useful Verification Commands**

***Check the HexStrike directory***

```bash
ls ~/hexstrike-ai
```

***Check whether port 8888 is listening***

```bash
ss -lntp | grep 8888
```

***Check the local health endpoint***

```bash
curl http://localhost:8888/health
```

***Validate the Claude configuration***

```bash
python3 -m json.tool ~/.config/Claude/claude_desktop_config.json >/dev/null && echo "JSON is valid"
```

***Inspect only the HexStrike configuration section***

```bash
grep -A12 '"hexstrike-ai"' ~/.config/Claude/claude_desktop_config.json
```

---

### **22. Troubleshooting Checklist**

If Claude does not detect HexStrike, check the following in order:

***1. Is the HexStrike API running?***

```bash
ss -lntp | grep 8888
```

***2. Does the health endpoint respond?***

```bash
curl http://localhost:8888/health
```

***3. Is the MCP URL correct?***

It should point to:

```text
http://localhost:8888
```

***4. Is the Python path correct?***

Verify:

```bash
ls /home/kali/hexstrike-ai/hexstrike-env/bin/python
```

***5. Does the MCP script exist?***

```bash
ls /home/kali/hexstrike-ai/hexstrike_mcp.py
```

***6. Is the JSON configuration valid?***

```bash
python3 -m json.tool ~/.config/Claude/claude_desktop_config.json
```

***7. Was Claude Desktop restarted?***

After changing the configuration, completely close and restart Claude Desktop.

***8. Check the diagnostic output***

```bash
claude-desktop-unofficial --doctor
```

---

### **23. Final Result**

After completing the configuration, Claude Desktop was able to communicate with the HexStrike MCP server and access the security tools exposed through the integration.

The completed setup provided the following workflow:

```text
Claude Desktop
      ↓
MCP
      ↓
HexStrike MCP
      ↓
HexStrike API
      ↓
Authorized security tools
```

This setup was then used during the Week 3 practical exercises to explore AI-assisted security tooling and password-cracking workflows in the authorized lab environment.

### **24. Evidences Collected**

<img width="1919" height="900" alt="Screenshot_2026-09-22_18-48-44" src="https://github.com/user-attachments/assets/2e8bcc7b-2d90-4425-a3cc-2fbe5d062b8e" />
<img width="1919" height="900" alt="Screenshot_2026-09-22_18-25-49" src="https://github.com/user-attachments/assets/0f76fa19-14ea-4c81-9ac0-7e3acd5cdd5e" />
<img width="1919" height="900" alt="Screenshot_2026-09-22_21-01-42" src="https://github.com/user-attachments/assets/5d4b3e60-4dec-4576-92df-8a26d1bdb4b0" />
<img width="1919" height="900" alt="Screenshot_2026-09-22_21-09-23" src="https://github.com/user-attachments/assets/d6f80f95-7b58-47ef-a6af-7c1bffe662a3" />
<img width="1919" height="900" alt="Screenshot_2026-09-22_21-03-45" src="https://github.com/user-attachments/assets/dee08c95-4a94-43d6-9a36-5062ec4aef41" />

---

## Author

**Alexandra Rustamova**  
Cybersecurity Professional — B083, Networkwalks

**LinkedIn:** [Alexandra Rustamova](https://www.linkedin.com/in/alexandra-rustamova-631a1439a/)

---

## Project Information

**Program:** Cybersecurity & Ethical Hacking Internship — Networkwalks  
**Week:** 03  
**Topic:** Exploitation & Credential Attacks  
**Document:** HexStrike-AI + Claude Desktop Setup Guide
















