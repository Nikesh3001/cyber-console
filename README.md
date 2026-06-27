# FRIDAY Cyber Console

> *"Control is an illusion" — Elliot Alderson*

A comprehensive cybersecurity command-line console and WebSocket-powered web interface for penetration testing, security auditing, and reconnaissance. Inspired by the fsociety toolkit from Mr. Robot.

## Overview

FRIDAY Cyber Console consolidates 30+ offensive and defensive security tools into a single, interactive REPL environment. It supports both a terminal-based CLI and a browser-based WebSocket UI, making it suitable for both headless servers and interactive pentesting sessions.

### Key Capabilities
- **Reconnaissance**: Port scanning, DNS enumeration, WHOIS lookups, Shodan search, banner grabbing, traceroute
- **Exploitation**: Web vulnerability scanning (Nikto), SQL injection testing (SQLMap), brute-force attacks (Hydra), directory busting (Gobuster), web fuzzing (FFUF)
- **Web Security**: HTTP security header analysis, SSL/TLS certificate inspection
- **System Security**: Firewall status, open ports, running services, security updates, best-practices audit
- **Network Tools**: SSH command execution, file hashing (MD5/SHA1/SHA256), hash type identification
- **Metasploit Integration**: Full msfconsole command execution, payload generation (msfvenom), resource script execution, database status
- **Reporting**: Generate HTML/PDF security assessment reports

## Quick Start

### Prerequisites
- Python 3.10+
- Required Python packages (install via `pip install -r requirements.txt`)
- External tools (optional, for full functionality):
  - [Nmap](https://nmap.org/download.html) — Port scanning
  - [Nikto](https://github.com/sullo/nikto) — Web server scanner
  - [SQLMap](https://sqlmap.org/) — SQL injection testing
  - [Hydra](https://github.com/maaaaz/thc-hydra-windows) — Brute-force login
  - [Gobuster](https://github.com/OJ/gobuster) — Directory/file busting
  - [FFUF](https://github.com/ffuf/ffuf) — Web fuzzing
  - [Whois](https://learn.microsoft.com/en-us/sysinternals/downloads/whois) — Domain registration lookup
  - [Metasploit Framework](https://www.metasploit.com/) — Exploitation framework

### Installation

```bash
# Clone the repo
git clone https://github.com/Nikesh3001/cyber-console.git
cd cyber-console

# Install Python dependencies
pip install -r requirements.txt
```

### Usage

**CLI Console:**
```bash
python cyber.py
```

**Web UI:**
```bash
start start_cyber_web.bat
# Or directly:
python cyber_server.py
# Then open http://localhost:8081
```

## CLI Console Commands

### Reconnaissance
| Command | Description |
|---------|-------------|
| `nmap <target> [ports] [type]` | Port scan with nmap (quick/full/stealth/udp) |
| `shodan <query>` | Search Shodan for internet-connected devices |
| `shodan-host <ip>` | Get detailed Shodan information for an IP |
| `dns <domain>` | DNS record lookup (A, AAAA, MX, NS, TXT, CNAME, SOA) |
| `subdomain <domain>` | Subdomain enumeration via DNS brute force |
| `whois <domain>` | WHOIS lookup for domain registration info |
| `banner <host> <port>` | Grab service banner from a host:port |
| `traceroute <target>` | Network traceroute to target |

### Exploitation
| Command | Description |
|---------|-------------|
| `nikto <target> [port] [--ssl]` | Web vulnerability scan with Nikto |
| `sqlmap <url> [data]` | SQL injection testing with SQLMap |
| `hydra <target> <svc> <usr> <pwd>` | Brute-force login with Hydra |
| `gobuster <url> [wordlist]` | Directory/file brute-force |
| `ffuf <url> [wordlist]` | Web fuzzing with FFUF |

### Web Security
| Command | Description |
|---------|-------------|
| `headers <url>` | Analyze HTTP security headers |
| `ssl <host> [port]` | Check SSL/TLS certificate details |
| `jina <url>` | Read webpage content via Jina AI |
| `semantic <query>` | AI-powered semantic search |

### System Security
| Command | Description |
|---------|-------------|
| `firewall` | Check firewall status |
| `ports [target]` | Scan common open ports |
| `services` | List running services |
| `listeners` | List listening ports |
| `updates` | Check security updates |
| `best-practices` | Run security audit |

### Network Tools
| Command | Description |
|---------|-------------|
| `ssh <host> <cmd> [user] [pass]` | Execute command via SSH |
| `hash <file>` | Calculate file hashes (MD5, SHA1, SHA256) |
| `hash-id <hash>` | Identify hash type |

### Metasploit Integration
| Command | Description |
|---------|-------------|
| `msf <command>` | Run msfconsole command |
| `msfvenom <payload> <lhost> <lport>` | Generate payload |
| `msf-script <path>` | Execute resource (.rc) script |
| `msf-db` | Check Metasploit database status |

### Built-in Dev Tools
| Command | Description |
|---------|-------------|
| `git <args>` | Run any git command |
| `python <code>` | Execute Python code inline |
| `pip <args>` | Run pip commands |

### Meta Commands
| Command | Description |
|---------|-------------|
| `report [targets...]` | Generate HTML/PDF security report |
| `tools` | List all registered tools |
| `check` | Check which tools are installed |
| `help` | Show help |
| `quit / exit / bye` | Exit console |

## Web UI

The Web UI provides a full terminal experience in the browser, complete with:

- Real-time output via WebSocket
- Command history (arrow keys)
- Tab autocompletion
- API key authentication
- Dark terminal theme (fsociety style)
- Persistent session management

### Features
- **WebSocket Protocol**: Bidirectional communication for real-time command execution
- **CORS Protection**: Restricted to configured origins
- **Security Headers**: CSP, X-Frame-Options, X-Content-Type-Options
- **API Authentication**: Optional API key via `FRIDAY_CYBER_API_KEY` env var

## Architecture

```
cyber.py (Entry Point — CLI)
     |
     ├── process_command() — Command dispatcher
     ├── COMMANDS dict — Maps command names to handlers
     │
     ├── SecurityTool (security.py)
     │   ├── nmap_scan() — Port scanning
     │   ├── nikto_scan() — Web vuln scanning
     │   ├── sqlmap_scan() — SQL injection
     │   ├── hydra_brute() — Brute force
     │   ├── gobuster_scan() — Dir busting
     │   ├── ffuf_fuzz() — Web fuzzing
     │   ├── dns_lookup() — DNS records
     │   ├── subdomain_enum() — Subdomain enum
     │   ├── whois_lookup() — WHOIS
     │   ├── banner_grab() — Banner grabbing
     │   ├── traceroute() — Network trace
     │   ├── shodan_*() — Shodan API
     │   ├── ssl_check() — SSL/TLS
     │   ├── msf_*() — Metasploit
     │   └── check_*() — System checks
     │
     └── InternetTools (internet.py)
         ├── jina_read() — Jina AI reader
         └── semantic_search() — AI search

cyber_server.py (Web UI — FastAPI)
     ├── GET / — Static HTML
     ├── GET /api/tools — Tool listing
     ├── POST /api/command — REST command execution
     └── WS /ws/cyber — WebSocket terminal
```

## Security Considerations

- **Rate Limiting**: All network scans and brute-force operations are rate-limited to prevent abuse
- **SSRF Protection**: Internal/private addresses are blocked from external scanning
- **Origin Validation**: WebSocket connections are restricted to allowed origins
- **Authentication**: Optional API key authentication for all endpoints
- **Audit Logging**: All console sessions should be authorized and logged

## License

MIT

---

*Built with reference to cybersecurity frameworks and tools. Use only on systems you own or have explicit permission to test.*
