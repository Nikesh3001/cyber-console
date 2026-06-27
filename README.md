# FRIDAY Cyber Console

A standalone cybersecurity toolkit with CLI and Web UI for penetration testing and security auditing.

## Features

### CLI Console (`tools/cyber.py`)
Run with: `python cyber.py`

Categories:
- **RECON**: nmap, shodan, dns, subdomain, whois, banner, traceroute
- **EXPLOIT**: nikto, sqlmap, hydra, gobuster, ffuf
- **WEB**: headers, ssl, jina, semantic
- **SYS**: firewall, ports, services, listeners, updates, best-practices
- **NET**: ssh, hash, hash-id
- **METASPLOIT**: msfconsole, msfvenom, msf-script, msf-db
- **DEV**: git, python, pip
- **META**: report, tools, check, help

### Web UI (`web/cyber_server.py`)
FastAPI + WebSocket terminal at `http://localhost:8081`

Run with: `start_cyber_web.bat` or `python web/cyber_server.py`

## Requirements
- Python 3.10+
- External tools (install separately): nmap, nikto, sqlmap, hydra, gobuster, ffuf, whois
- Metasploit Framework (via WSL or native install)

## Installation
```bash
pip install -r requirements.txt
```

## Project Structure
```
cyber/
├── tools/
│   ├── cyber.py        # Main CLI console
│   ├── security.py     # Security tools (nmap, nikto, etc.)
│   ├── internet.py     # Internet/web tools (shodan, jina, etc.)
│   └── report.py       # Report generation
├── web/
│   ├── cyber_server.py # FastAPI WebSocket server
│   └── cyber_static/   # Frontend (HTML/JS/CSS)
├── start_cyber_web.bat # Windows launcher
└── requirements.txt
```