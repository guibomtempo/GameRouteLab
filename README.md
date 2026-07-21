\# 🎮 GameRouteLab



> Multi-Cloud Game Network Optimization Laboratory using WireGuard, TunnlTo and Cloud VPS.



!\[Status](https://img.shields.io/badge/status-active-brightgreen)

!\[Ubuntu](https://img.shields.io/badge/Ubuntu-24.04-orange)

!\[WireGuard](https://img.shields.io/badge/WireGuard-Enabled-blue)

!\[Cloud](https://img.shields.io/badge/Multi--Cloud-Oracle%20%7C%20Google-success)



\---



\# 📖 About



GameRouteLab is a personal laboratory created to study and improve network routes for online games.



The goal is to compare different cloud providers, evaluate latency, jitter and packet loss, and determine which route provides the best gaming experience.



The project currently uses:



\- Oracle Cloud

\- Google Cloud Platform

\- WireGuard

\- TunnlTo

\- Ubuntu Server

\- Linux Networking

\- iptables

\- Prometheus (future)

\- Grafana (future)



\---



\# 🎯 Goals



\- Build VPN gateways close to game servers

\- Reduce latency

\- Reduce jitter

\- Reduce packet loss

\- Compare multiple cloud providers

\- Create automatic route selection

\- Build a monitoring dashboard



\---



\# 🌍 Current Infrastructure



```

&#x20;                    Internet

&#x20;                        │

&#x20;                        │

&#x20;              ┌─────────┴─────────┐

&#x20;              │                   │

&#x20;              │                   │

&#x20;       Oracle Cloud         Google Cloud

&#x20;       VPSoracle            VPSgoogle

&#x20;       Frankfurt            Belgium

&#x20;              │                   │

&#x20;              └─────────┬─────────┘

&#x20;                        │

&#x20;                 WireGuard VPN

&#x20;                        │

&#x20;                    TunnlTo

&#x20;                        │

&#x20;                   Gaming PC

&#x20;                        │

&#x20;                   Lineage II

```



\---



\# 🖥 Current Nodes



| Name | Provider | Region | Purpose |

|-------|----------|---------|---------|

| VPSoracle | Oracle Cloud | Frankfurt | VPN Gateway |

| VPSgoogle | Google Cloud | Belgium | VPN Gateway |



\---



\# 📦 Repository Structure



```

GameRouteLab/



docs/

servers/

client/

scripts/

monitoring/

benchmark/

assets/

```



\---



\# 🔧 Technologies



\- Ubuntu Server 24.04

\- WireGuard

\- TunnlTo

\- iptables

\- iproute2

\- vnStat

\- MTR

\- iperf3

\- Python

\- Prometheus

\- Grafana



\---



\# 🚀 Bootstrap



\## Update System



```bash

sudo apt update

sudo apt upgrade -y

```



\---



\## Install Packages



```bash

sudo apt install \\

wireguard \\

iptables \\

curl \\

wget \\

git \\

vim \\

net-tools \\

vnstat \\

mtr \\

iperf3 \\

fail2ban \\

python3 \\

python3-pip \\

python3-venv -y

```



\---



\## Enable IP Forward



```bash

sudo nano /etc/sysctl.conf

```



```

net.ipv4.ip\_forward=1

```



Apply:



```bash

sudo sysctl -p

```



\---



\# WireGuard Server Example



```

\[Interface]



Address = 10.60.0.1/24

ListenPort = 443

PrivateKey = SERVER\_PRIVATE\_KEY



PostUp = iptables -A FORWARD -i wg0 -j ACCEPT

PostUp = iptables -A FORWARD -o wg0 -j ACCEPT

PostUp = iptables -t nat -A POSTROUTING -o ens4 -j MASQUERADE



PostDown = iptables -D FORWARD -i wg0 -j ACCEPT

PostDown = iptables -D FORWARD -o wg0 -j ACCEPT

PostDown = iptables -t nat -D POSTROUTING -o ens4 -j MASQUERADE



\[Peer]



PublicKey = CLIENT\_PUBLIC\_KEY

AllowedIPs = 10.60.0.2/32

PersistentKeepalive = 25

```



\---



\# Client Example



```

\[Interface]



PrivateKey = CLIENT\_PRIVATE\_KEY

Address = 10.60.0.2/24

DNS = 1.1.1.1



\[Peer]



PublicKey = SERVER\_PUBLIC\_KEY

Endpoint = SERVER\_IP:443



AllowedIPs = 10.60.0.0/24



PersistentKeepalive = 25

```



\---



\# Security



Never commit:



\- private keys

\- client keys

\- cloud credentials

\- SSH private keys



Use:



```

\*.key

\*.pem

\*.conf

.env

```



inside `.gitignore`.



\---



\# Split Tunnel



Only game traffic is routed through VPN.



```

Game Server

&#x20;     │

&#x20;     │

&#x20;WireGuard Tunnel

&#x20;     │

&#x20;     │

&#x20;Internet

```



Everything else uses the local ISP.



\---



\# Benchmark



Metrics collected:



\- Ping

\- Jitter

\- Packet Loss

\- Route Stability

\- Throughput

\- CPU Usage

\- Memory Usage



Tools:



\- ping

\- mtr

\- iperf3

\- vnStat



\---



\# Future Roadmap



\## Phase 1



✅ Oracle Cloud



\## Phase 2



✅ Google Cloud



\## Phase 3



⬜ Benchmark



\## Phase 4



⬜ Prometheus



\## Phase 5



⬜ Grafana Dashboard



\## Phase 6



⬜ Automatic Best Route Selection



\## Phase 7



⬜ Multi-region deployment



\## Phase 8



⬜ AWS



\## Phase 9



⬜ Azure



\## Phase 10



⬜ Hetzner



\---



\# Lessons Learned



\## Oracle Cloud



Works well with WireGuard.



\---



\## Google Cloud



Requires opening UDP 443 in the VPC firewall.



Linux firewall alone is \*\*not enough\*\*.



\---



\## TunnlTo



Fully compatible with WireGuard configuration files.



\---



\## WireGuard



Very lightweight and excellent for game routing.



\---



\# Author



Created by Guilherme Bomtempo



Project: \*\*GameRouteLab\*\*



```

Optimizing routes.

Reducing latency.

Learning networking.

```



