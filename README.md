# Authentication Security Lab | Kali Linux + Medusa

> **DIO / Santander Cybersecurity — Educational Project**  
> **Status:** Environment preparation · **Execution evidence:** Not yet collected

An educational cybersecurity case study focused on authentication weaknesses and defensive controls. The lab will use **Kali Linux**, **Medusa**, and intentionally vulnerable test systems in a **private, isolated VirtualBox network**.

This repository documents a training exercise—not a penetration test against any real company or public service. All users, passwords and targets used in demonstrations will be created for the lab.

## Project objective

Understand how weak passwords and poorly configured authentication services can enable repeated login attempts, and document practical mitigation measures.

The DIO challenge covers the preparation of a Kali Linux and Metasploitable 2 lab and controlled scenarios involving **FTP**, a vulnerable web login (**DVWA**), and **SMB** authentication. The exact experiments and results will be documented after execution.

## Planned architecture

```text
Windows host
└── Oracle VirtualBox
    └── Isolated lab network (internal network)
        ├── Kali Linux — authorized testing machine
        └── Metasploitable 2 — intentionally vulnerable target
            └── DVWA (if configured for the web-login scenario)
```

**Isolation rule:** The vulnerable target must not be exposed to the household network or public internet. No bridged adapter, router port forwarding, or external target testing. The lab network configuration will be verified before any test.

## Tools and concepts

| Component | Role |
| --- | --- |
| Oracle VirtualBox | Virtualization and network isolation |
| Kali Linux | Security testing environment |
| Metasploitable 2 | Deliberately vulnerable practice target |
| Medusa | Authentication test tool used only against lab services |
| FTP / SMB / DVWA | Educational authentication scenarios |
| GitHub | Versioned documentation and evidence |

## Planned workflow

- [ ] Verify virtual machines, resource allocation, and isolated networking.
- [ ] Capture the lab topology and assigned private IP addresses.
- [ ] Identify enabled services **only on the lab target**.
- [ ] Prepare small lists of fictional test accounts and passwords.
- [ ] Run limited, authorized authentication tests in the isolated lab.
- [ ] Capture evidence of observed results, including unsuccessful attempts.
- [ ] Explain root causes, limitations, and defensive mitigations.
- [ ] Review the documentation and submit the GitHub repository to DIO.

## Evidence and findings

**Not yet executed.** Screenshots, tool output, service versions, and conclusions will be added only after they have been observed and validated in the lab. No sample output will be presented as a real result.

## Defensive perspective

The final analysis will assess password policy, multi-factor authentication where supported, login throttling and lockouts, monitoring and alerting, service exposure, and secure configuration. Controls will be discussed in the context of each tested protocol.

## Scope and limitations

- This is an **authorized educational lab**, not a commercial security assessment.
- Metasploitable 2 is intentionally unsafe; it must stay isolated.
- No real identities, leaked credential lists, company systems, or internet-facing services.
- Findings will describe the lab only, not claims about real-world organizations.

## Learning context

Based on the DIO challenge **“Simulando um Ataque de Brute Force de Senhas com Medusa e Kali Linux”** from the Santander Cybersecurity learning path. This repository is an original learning artifact and is not an official DIO repository.

---

*Documentation will evolve as each practical activity is completed.*
