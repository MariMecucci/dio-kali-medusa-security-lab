# Authentication Security Lab | Kali Linux + Medusa

> **DIO / Santander Cybersecurity — Educational Project**  
> **Status:** Isolated lab, network validation, service discovery, and a controlled SSH authentication demonstration **completed**. Other challenge scenarios remain optional follow-up work.

An educational cybersecurity case study focused on authentication weaknesses and defensive controls. The lab uses **Kali Linux 2026.3**, **Medusa 2.3**, and **Metasploitable 2** inside a private, isolated **Oracle VirtualBox Internal Network**. It does **not** assess a real company or public service.

## Verified practical results — November 8, 2026

| Check | Verified observation |
| --- | --- |
| Internal network | `dio-cyber-lab`; no bridged network on the target |
| Kali Linux | `192.168.77.10` |
| Metasploitable 2 | `192.168.77.20` |
| Connectivity | 4/4 ICMP replies, **0% loss** |
| Service discovery | Nmap confirmed accessible SSH, Telnet, HTTP, SMB and other lab services |
| Authentication test | Medusa 2.3; **two SSH password candidates**, one valid training credential reported as `[SUCCESS]` |
| Real-world targets tested | **None** |

**[Read the full verified lab report](docs/2026-11-08-verified-lab-evidence.md)** · **[See transcribed terminal evidence](evidence/verified-terminal-excerpts.md)** · **[DIO submission guide](docs/dio-submission.md)**

> These are **observations from an intentionally vulnerable training machine**, not evidence of an external compromise or a production security assessment. The account used a known lab default password; no private or leaked credentials were used.

## Architecture

```text
Windows host
└── Oracle VirtualBox
    └── Internal Network: dio-cyber-lab (isolated from external networks)
        ├── Kali Linux 2026.3 — 192.168.77.10/24
        │   ├── Nmap
        │   └── Medusa 2.3
        └── Metasploitable 2 — 192.168.77.20/24
            └── Deliberately vulnerable SSH, HTTP, SMB, etc.
```

**Isolation requirement:** Never bridge the Metasploitable guest to a household or public network, forward ports to it, or run tests on systems without explicit authorization. At the time of the demonstrated tests, both VMs used the internal lab network. IP addresses were assigned temporarily and may need to be reapplied after restart.

## Technical workflow

- [x] Prepare Kali Linux and a Metasploitable 2 VirtualBox guest.
- [x] Isolate both guests in the VirtualBox internal network `dio-cyber-lab`.
- [x] Assign test-only private addresses and verify connectivity.
- [x] Perform an Nmap TCP connect scan against the isolated test target.
- [x] Prepare a two-candidate training wordlist and run a limited Medusa SSH authentication check.
- [x] Document actual observed outcomes and defensive mitigations.
- [x] Publish selected, clearly labeled terminal evidence transcribed from actual screenshots.
- [x] Prepare a submission summary and links for DIO.
- [ ] **User action:** paste the repository URL in DIO's **Entregar Projeto** form.
- [ ] **Optional only:** add sanitized screenshots if requested by the evaluator (not presently in the repo).
- [ ] **Not executed:** FTP, DVWA web login and SMB/password-spraying scenarios.

## Tools and capabilities demonstrated

| Tool / concept | Demonstrated use |
| --- | --- |
| VirtualBox | Virtual machine configuration and internal network isolation |
| Kali Linux | Authorized lab testing environment |
| Metasploitable 2 | Intentionally vulnerable test target |
| Linux networking | Manual static IPv4 address configuration and ICMP reachability checks |
| Nmap | TCP service enumeration on a specified training host |
| Medusa | Limited SSH authentication test using a small local wordlist |
| GitHub | Evidence-backed technical documentation |

## Findings and mitigations

**Finding:** A known default password on the deliberately vulnerable lab machine permitted a successful SSH authentication attempt. This confirms the weakness of retaining default credentials in this specific training scenario; it does **not** prove a broader brute-force bypass.

**Recommended defenses:** remove default credentials, enforce strong unique secrets or SSH key authentication, restrict access to administrative services, monitor authentication events, and apply rate limiting/MFA where appropriate.

## Scope and limitations

- Educational, authorized exercise in a controlled network.
- No production systems, third-party endpoints, real employee accounts, or leaked password lists.
- Only the **SSH** authentication scenario has been verified; FTP, DVWA and SMB outcomes are not claimed.
- Test accounts on Metasploitable 2 are part of its public, intentionally vulnerable training image.
- Screenshots were captured during the lab session; **only selected observations transcribed from them are currently in the repository**. The transcriptions are not raw machine-generated log files.
- No persistence, privilege escalation, lateral movement, or exfiltration was performed.

## Submission

The repository documentation and verified SSH adaptation are ready for submission. Use the [DIO submission guide](docs/dio-submission.md) for the project link and concise description. **DIO decides whether this adapted scenario satisfies its evaluation criteria.**

## Learning context

Based on the DIO challenge **“Simulando um Ataque de Brute Force de Senhas com Medusa e Kali Linux”** from the Santander Cybersecurity learning path. This is an original learning artifact, not an official DIO repository.

---

*Evidence-led documentation · isolated training environment · no real-world targets tested.*
