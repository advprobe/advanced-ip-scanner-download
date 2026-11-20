# Advanced IP Scanner 2.5.4594.1 Download for Windows 10/11

Advanced IP Scanner walks one subnet or a whole address range with ICMP echo requests and ARP lookups, then fills in hostname, MAC address and network adapter maker for every machine that answers. Open ports 135, 139, 445 and 3389 are checked on the way, so Windows hosts, shared folders and RDP endpoints are marked in the same table. Right-click actions start an RDP or Radmin session, send a Wake-on-LAN magic packet or shut a computer down with supplied credentials. The result list exports to CSV, HTML or XML, which makes two scans of the same range easy to diff.

The scan is a sequence rather than a single probe. An ICMP echo request decides whether an address is alive; the ARP table supplies the MAC address, but only for hosts on the same broadcast segment, because ARP does not cross routers. A reverse DNS or NetBIOS query fills the name column, and a short TCP connect attempt on the four ports above marks the services that answer. Each stage can fail on its own, so a host with a name but no MAC, or a MAC with no open ports, is normal rather than a bug.

<p align="center">
  <a href="https://download.advanced-ip-scanner.com/download/files/Advanced_IP_Scanner_2.5.4594.1.exe">
    <img src="https://img.shields.io/badge/DOWNLOAD-Advanced_IP_Scanner_2.5.4594.1-1B5E9B?style=for-the-badge&logo=windows&logoColor=white" alt="Download Advanced IP Scanner">
  </a>
</p>

| | |
|---|---|
| **Version** | 2.5.4594.1 |
| **Package** | `Advanced_IP_Scanner_2.5.4594.1.exe` — 20.1 MB |
| **Architecture** | x86 / x64 |
| **Platform** | Windows 10, Windows 11, Windows Server 2016+ |
| **License** | Freeware |

## Download

| Package | Size | Link |
|---|---|---|
| **Advanced IP Scanner 2.5.4594.1** | 20.1 MB | [Download](https://download.advanced-ip-scanner.com/download/files/Advanced_IP_Scanner_2.5.4594.1.exe) |

The link points at the file itself, so the browser saves the installer without an intermediate page. The executable on that host is the same one described here.

## Works with

- Windows 11 (x64)
- Windows 10 (x86 and x64)
- Windows Server 2016 / 2019 / 2022
- Remote subnets reachable through a routed VPN
- IPv4 ranges written as `192.168.1.0/24` or `192.168.1.1-192.168.1.254`

## SHA-256 checksum

```
26D5748FFE6BD95E3FEE6CE184D388A1A681006DC23A0F08D53C083C593C193B  Advanced_IP_Scanner_2.5.4594.1.exe
```

```powershell
Get-FileHash .\Advanced_IP_Scanner_2.5.4594.1.exe -Algorithm SHA256
```

If the digest differs, the download was tampered with or truncated; fetch it once more.

## Install

1. Download `Advanced_IP_Scanner_2.5.4594.1.exe` and run it as administrator.
2. Accept the licence, keep the default folder, and leave the Radmin Viewer component only if remote control is needed.
3. Finish the wizard and type a range in the **Scan** field, for example 192.168.1.0/24, then press **Scan**.
4. Silent install for a scripted rollout: `Advanced_IP_Scanner_2.5.4594.1.exe /VERYSILENT /NORESTART`.

## What it does

- Ping sweep with ARP resolution over a range, a subnet or several subnets
- MAC address and network adapter manufacturer shown for each host
- Shared folder, RDP and web interface detection on discovered machines
- Wake-on-LAN and remote shutdown from the result list
- Export to CSV, HTML and XML for before-and-after comparison

## Compatibility

The scanner is an IPv4 tool. Ranges are entered in CIDR notation or as a first-last pair, and interface selection limits the sweep to one adapter when a laptop has both Ethernet and Wi-Fi connected to different segments. IPv6-only networks are not enumerated, and a host reachable only over IPv6 stays invisible. Running the tool inside a VPN session works as long as the tunnel passes ICMP and the ARP-visible segment is the tunnel's own; a routed subnet behind the far end of the tunnel will show names and ports but no MAC addresses.

Windows targets answer differently depending on their firewall profile. The default Public profile blocks inbound echo requests, so a machine can be invisible to the sweep while still serving files. Domain and Private profiles usually allow echo, which is why scans on a work network find more hosts than scans on a guest network. Hosts with SMB disabled still show up if they answer ping, but the shared-folder flag and the RDP button will not work against them.

Ranges larger than a /22 take noticeably longer because the tool waits for timeouts on every silent address; splitting the sweep per floor or per VLAN is faster than one wide range.

## Troubleshooting

**Hosts missing from the list** — the target firewall drops ICMP. Add an inbound echo rule on the target, or accept that only pingable hosts appear.

**MAC address column empty** — the host is behind a router or on another VLAN, so ARP never sees it. Only the last hop before the target can report a MAC.

**Wake-on-LAN does nothing** — the magic packet is a broadcast on UDP 9 and stays inside the local segment. The target NIC must have wake enabled in BIOS and in the adapter properties, and the machine needs a wired connection in most cases.

**Remote shutdown returns "Access is denied"** — the account is not a local administrator on the target, or UAC remote restrictions strip the token. A domain admin account works; a local admin usually needs the token filter policy relaxed on the target.

**Shared folders do not open** — SMB1 is disabled on modern Windows and anonymous session enumeration is blocked by default, so the folder list can come back empty even when shares exist. Opening the host by name in Explorer with credentials is the reliable check.

## Alternatives

- **Angry IP Scanner** — cross-platform, Java-based, with a plugin model for custom probes.
- **Nmap** — service and version detection far beyond four ports, at the cost of a command line.
- **SoftPerfect Network Scanner** — deeper SNMP and WMI inventory, paid for business use.
- **Router ARP table** — free and always current for the local segment, though it lists only addresses that recently transmitted.

## FAQ

**Is Advanced IP Scanner free for business use?** — Yes, the freeware licence covers commercial networks as well as home ones.

**Does it install a service or a driver?** — No. It runs as a normal application and needs elevation only to read ARP data and send the shutdown and Wake-on-LAN packets.

**Why do some hosts show a name and others only an IP?** — Reverse DNS and NetBIOS are both optional. A host with no PTR record and no NetBIOS responder keeps its address only.

**Can it scan several subnets at once?** — Yes, ranges can be separated by commas or semicolons in the scan field, and each one is swept in turn.

**Does it store scan results between runs?** — The list lives in the session; export to CSV or XML before closing the window if the data is needed later.

## Disclaimer

The version, installer size and checksum above were recorded from the published build for offline reference. Advanced IP Scanner and Radmin are products of Famatech; their names belong to the rights holder. This page is an independent index, not connected to that company, and implies no endorsement.
