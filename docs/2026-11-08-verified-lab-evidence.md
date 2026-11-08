# Verified Lab Evidence — 2026-11-08

> **DIO / Santander Cybersecurity · Educational, isolated virtual lab**
>
> All activities in this report were performed on an intentionally vulnerable **Metasploitable 2** guest, using a **Kali Linux** guest on the same VirtualBox internal network. No public, third-party, or production targets were tested.

## Lab environment

| Component | Observed value |
| --- | --- |
| Virtualization | Oracle VirtualBox |
| Network mode | Internal Network (`dio-cyber-lab`) |
| Testing VM | Kali Linux 2026.3 — `192.168.77.10/24` |
| Target VM | Metasploitable 2 — `192.168.77.20/24` |
| Target type | Intentionally vulnerable training machine |
| Authentication tool | Medusa 2.3 |
| Reconnaissance tool | Nmap |
| Confirmed Medusa module | SSH |

The private IPv4 addresses were configured for this lab session. They were **not configured persistently**; the IP assignments may need to be restored after restarting either guest. The isolated network was used without a gateway to the host's household network.

## Evidence 1 — Network connectivity

From Kali, a four-packet ICMP connectivity check to the target completed successfully:

```bash
ping -c 4 192.168.77.20
```

**Observed result:** 4 packets transmitted, 4 received, **0% packet loss**, approximately **2.08 ms** average round-trip time. This confirms reachability from the testing VM to the lab target at the time of the test; it is not proof of vulnerability.

## Evidence 2 — Service discovery

A default TCP connect scan was executed **only** against the lab target:

```bash
nmap -sT 192.168.77.20
```

The screenshot of the scan shows the target reachable and services including:

| Port(s) | Reported service(s) | Observation |
| --- | --- | --- |
| 22 | ssh | Open |
| 23 | telnet | Open |
| 80 | http | Open |
| 139, 445 | netbios-ssn, microsoft-ds | Open |
| 3306 | mysql | Open |
| 5432 | postgresql | Open |
| 5900 | vnc | Open |

Other services were also present. Open ports indicate exposed services, **not confirmed exploitable vulnerabilities**.

## Evidence 3 — Limited SSH authentication test with Medusa

A two-line local wordlist was created for the exercise: one deliberately incorrect password and one known **default credential for the training machine**. The test used a single lab account, one worker, and stopped after the first valid authentication:

```bash
medusa -h 192.168.77.20 -u msfadmin -P senhas.txt -M ssh -t 1 -f
```

**Observed result (from the Kali terminal screenshot):**

- The first candidate was attempted and did not produce a success result.
- The second candidate produced `ACCOUNT FOUND` and `[SUCCESS]` for SSH authentication on `192.168.77.20`.
- The tool returned to the shell prompt without a reported runtime error.
- The run showed **2 candidates tested** and **1 confirmed valid login**.

This is a **controlled authentication demonstration**, not a claim of unauthorized access, privilege escalation, exploitation of an unknown vulnerability, or compromise of a real system.

## Security interpretation

The exercise illustrates a common authentication risk: leaving a well-known default account and password enabled can permit successful login attempts. The test does not, on its own, establish the presence or absence of brute-force protection, account lockout, or rate limiting at scale.

**Recommended defensive controls:**

1. Replace or disable default accounts/credentials before deploying services.
2. Use unique, high-entropy passwords and secure SSH configuration.
3. Restrict management services to approved network segments and users.
4. Monitor authentication failures and successes; alert on suspicious patterns.
5. Where supported, use MFA, rate limiting, lockout policies, or SSH public-key authentication.
6. Avoid exposing intentionally vulnerable machines to external networks.

## Scope, completeness, and next work

This report documents **one completed SSH authentication scenario**. The DIO challenge also describes FTP, DVWA web-login, and SMB/password-spraying scenarios. Those additional scenarios **have not been performed or evidenced in this repository** and must not be described as completed.

The original captures are available in the local project-session conversation and are **not yet uploaded into this GitHub repository**. Repositories should contain only sanitized screenshots; avoid posting personal host details or credentials from non-lab systems.

## Reproducibility note

The vulnerable VM and its credential are publicly known training materials. The actions above must only be reproduced in an environment you own or are explicitly authorized to test, using the same restricted internal-network topology.
