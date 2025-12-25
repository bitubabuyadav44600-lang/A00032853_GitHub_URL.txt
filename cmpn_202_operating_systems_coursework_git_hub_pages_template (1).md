# CMPN202 Operating Systems Coursework Journal

**Student Name:** Bitu Babu Yadav  
**Student ID:** A00032853  
**Module:** CMPN202 – Operating Systems  
**Submission:** GitHub Pages Journal (7 Weeks)

---

## Project Overview
This journal documents the design, deployment, security configuration, and performance evaluation of a Linux-based server system administered remotely from a workstation. The project follows a structured, week-by-week approach aligned with the CMPN202 coursework brief.

**System Summary:**
- Server OS: *(to be filled)*
- Workstation OS: *(to be filled)*
- Virtualisation Platform: VirtualBox
- Network Type: Isolated internal network

---

## Table of Contents
- [Week 1 – System Planning & OS Selection
- [Week 2 – Security Planning & Testing Methodology
- [Week 3 – Application Selection & Installation
- [Week 4 – Core Deployment & Foundational Security
- [Week 5 – Advanced Security & Automation
- [Week 6 – Performance Evaluation & Optimisation
- [Week 7 – Security Audit & System Evaluation
---

## Week 1 – System Planning & OS Selection
### Objectives
The objective of this week was to plan the system architecture, select suitable operating systems, and document the base system configuration using command-line tools as required by the assessment brief.

### System Architecture
Two virtual machines were deployed using VirtualBox:
- **Server VM:** Ubuntu Server (headless, no GUI)
- **Workstation VM:** Ubuntu Desktop (used for SSH access)

The machines communicate over an **isolated internal network**, ensuring all administration is performed remotely and securely.

*(Insert architecture diagram screenshot here)*

### Distribution Selection Justification
Ubuntu Server LTS was selected due to long-term support, strong security update mechanisms, extensive documentation, and built-in AppArmor support. Debian was considered as an alternative but requires more manual configuration. CentOS was rejected due to lifecycle changes.

### Network Configuration
- VirtualBox Adapter: Internal Network
- Server IP: Static (documented)
- Workstation IP: Static (documented)

### Mandatory CLI Evidence
The following commands were executed on the server via SSH to document system specifications:
```bash
uname -a
free -h
df -h
ip addr
lsb_release -a
```
Screenshots show the terminal prompt with `username@hostname` as required.

---

## Week 2 – Security Planning & Testing Methodology
### Objectives
This week focused on planning security controls and defining a structured performance testing methodology.

### Security Configuration Checklist
Planned security measures include:
- SSH key-based authentication
- Disabling SSH password login
- Firewall-based access control
- Mandatory access control (AppArmor)
- Automatic security updates
- Least-privilege user management

### Threat Model
| Threat | Risk | Mitigation |
|------|------|-----------|
| Brute-force SSH | High | SSH keys + fail2ban |
| Vulnerable packages | Medium | Automatic updates |
| Network intrusion | High | Firewall IP restriction |

### Performance Testing Plan
Performance will be evaluated using remote monitoring tools over SSH, measuring CPU, memory, disk I/O, and network usage under baseline and load conditions.

------|-----------|---------------------|
| Brute-force SSH attacks | High | SSH key-based authentication and fail2ban |
| Unpatched vulnerabilities | Medium | Automatic security updates |
| Unauthorised network access | High | Firewall IP-based access control |

### Security Controls Planned
- Disable SSH password authentication
- Restrict SSH access to workstation IP only
- Enforce least-privilege user access
- Enable mandatory access control

### Testing Methodology
Performance and security testing will be conducted using:
- CPU, memory, disk, and network monitoring tools
- Baseline measurements before optimisation
- Comparative testing after security and performance tuning

This structured methodology ensures reliable and repeatable results.

------|------|------------|
| Brute-force SSH | High | SSH keys + fail2ban |
| Unpatched software | Medium | Automatic updates |
| Unauthorised access | High | Firewall rules |

### Testing Methodology
- Performance metrics to be measured
- Tools to be used

---

## Week 3 – Application Selection & Installation
### Objectives
To select representative applications for performance testing and install them using secure SSH-based administration.

### Application Selection Matrix
| Application | Workload Type | Justification |
|------------|--------------|---------------|
| stress-ng | CPU/RAM | Generates controlled system load |
| sysbench | CPU/Memory | Benchmarking and comparison |
| iperf3 | Network | Measures bandwidth and latency |

### Installation Commands
All applications were installed via SSH:
```bash
sudo apt update
sudo apt install stress-ng sysbench iperf3
```

### Expected Resource Usage
- stress-ng: High CPU and memory utilisation
- sysbench: Predictable benchmarking load
- iperf3: Network throughput stress

### Monitoring Strategy
System metrics are collected using tools such as `top`, `htop`, `free`, `vmstat`, and `iftop` during tests.

------------|--------|----------------|
| stress-ng | Synthetic load testing | CPU & RAM |
| sysbench | Benchmarking | CPU & Memory |
| iperf3 | Network testing | Network throughput |

### Installation
Applications were installed securely via SSH using the package manager:
```bash
sudo apt update
sudo apt install stress-ng sysbench iperf3
```

### Expected Performance Impact
- **stress-ng:** High CPU and memory utilisation under load
- **sysbench:** Consistent benchmarking results for comparison
- **iperf3:** Measurement of network bandwidth and latency

These tools provide quantitative data required for later optimisation analysis.

------------|--------|----------------|
| *(App 1)* | CPU test | CPU |
| *(App 2)* | Memory test | RAM |
| *(App 3)* | Network test | Network |

### Installation Commands
```bash
sudo apt install <package-name>
```

### Expected Performance Impact
*(Brief explanation per application)*

---

## Week 4 – Core Deployment & Foundational Security
### Objectives
To deploy the server securely and implement mandatory foundational security controls.

### SSH Key-Based Authentication
```bash
ssh-keygen -t ed25519
ssh-copy-id user@server-ip
```
Password authentication and root login were disabled in `/etc/ssh/sshd_config`.

### Firewall Configuration (UFW)
```bash
sudo ufw default deny incoming
sudo ufw allow from <workstation-ip> to any port 22
sudo ufw enable
sudo ufw status verbose
```

### User and Privilege Management
```bash
sudo adduser adminuser
sudo usermod -aG sudo adminuser
```

### Evidence
Screenshots demonstrate SSH access, firewall rules, and configuration changes, all performed remotely.

---

## Week 5 – Advanced Security & Automation
### Objectives
To implement advanced security controls and develop automation scripts for verification and monitoring.

### Mandatory Access Control (AppArmor)
```bash
sudo aa-status
```
AppArmor profiles were enforced and verified.

### Automatic Security Updates
```bash
sudo apt install unattended-upgrades
sudo dpkg-reconfigure unattended-upgrades
```

### fail2ban Configuration
```bash
sudo apt install fail2ban
sudo systemctl enable fail2ban
sudo systemctl status fail2ban
```

### Security Baseline Script (Server)
`security-baseline.sh` verifies SSH, firewall, updates, AppArmor, and fail2ban status. Each command includes explanatory comments.

### Monitoring Script (Workstation)
`monitor-server.sh` connects via SSH and records CPU, memory, disk, and network statistics.

---

## Week 6 – Performance Evaluation & Optimisation
### Objectives
To evaluate system performance under load and apply optimisations supported by quantitative data.

### Baseline Testing Commands
```bash
sysbench cpu run
free -h
```

### Load Testing
```bash
stress-ng --cpu 4 --timeout 60s
```

### Network Testing
```bash
iperf3 -s
iperf3 -c <server-ip>
```

### Optimisations Applied
1. Disabled unnecessary services using `systemctl disable`
2. Tuned workload parameters to reduce CPU overhead

Performance improvements were verified using before-and-after measurements and visualised in graphs.

------|--------------------|-------------------|
| CPU Utilisation |  |  |
| Memory Usage |  |  |
| Network Throughput |  |  |

*(Insert charts and tables here)*

### Optimisations Applied
1. Reduced unnecessary background services to free system resources
2. Tuned application parameters to improve CPU and memory efficiency

These optimisations resulted in measurable performance improvements.

-------|--------|-------|
| CPU usage | | |
| RAM usage | | |

### Visualisations
*(Insert graphs/screenshots)*

### Optimisations Applied
1. *(Optimisation 1)*
2. *(Optimisation 2)*

---

## Week 7 – Security Audit & System Evaluation
### Objectives
To audit the system security posture and evaluate overall configuration effectiveness.

### Lynis Audit
```bash
sudo apt install lynis
sudo lynis audit system
```
Initial and improved scores were documented after remediation.

### Network Scan (Isolated Network Only)
```bash
nmap <server-ip>
```

### Service Audit
```bash
systemctl list-units --type=service --state=running
```
All active services were reviewed and justified.

### Final Evaluation
The system demonstrates secure remote administration, effective performance tuning, and compliance with all mandatory assessment requirements.

---

## Conclusion
This project demonstrates secure remote administration, performance monitoring, and optimisation of a Linux server system. Security controls were balanced with performance requirements, supported by quantitative evidence and structured testing.

---

## Repository Structure
```
/docs
  index.md
  week1.md
  week2.md
  week3.md
  week4.md
  week5.md
  week6.md
  week7.md
/images
/scripts
```

---

## Declaration
I confirm that this work is my own and complies with university academic integrity regulations.

