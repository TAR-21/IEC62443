# IEC 62443-4-1 / 4-2 Compliance Guideline  
### (Draft for **Red Hat Device Edge** & **Red Hat Edge Manager**)

---

## 1. Purpose

This guideline describes how Red Hat Device Edge (RHEL for Edge / bootc / rpm-ostree) and  
Red Hat Edge Manager (RHEM) can be aligned with IEC 62443-4-1 and IEC 62443-4-2 for use in industrial and OT environments.

---

## 2. Alignment with IEC 62443-4-1 (Secure Development Lifecycle)

All Red Hat products, including Device Edge components, follow the **Red Hat Secure Development Lifecycle (RH-SDLC)**, which aligns closely with IEC 62443-4-1.

### 2.1 Secure Development Process Management
- Application of RH-SDLC across product development  
- Security training and standardized development processes  
- Security reviews for every major release  

### 2.2 Security Requirements Definition
- Definition of threat models, cryptographic requirements, and governance policies  
- Alignment with FIPS, CIS, Common Criteria, and industry best practices  

### 2.3 Secure Architecture and Design
- **Immutable OS architecture (rpm-ostree / bootc)**  
- **SELinux** mandatory access control  
- Secure OTA and device lifecycle management via **RHEM**  

### 2.4 Secure Implementation
- Compiler hardening (stack protection, RELRO, PIE, etc.)  
- FIPS 140 validated crypto modules  
- Code reviews and static/dynamic analysis  

### 2.5 Security Testing
- Continuous integration and testing by Red Hat QE  
- Dedicated testing for Edge images and bootc-based systems  

### 2.6 Vulnerability Management
- 24/7 monitoring by Red Hat Product Security  
- CVE issuance, RHSA advisory publication  
- Rapid patch delivery via OTA through Edge Manager  

### 2.7 Documentation
- Security configuration guides for Device Edge and Edge Manager  
- Reference architectures for secure edge deployments  

> **Most 4-1 requirements are fulfilled by Red Hat’s SDLC.  
> Users do not need to implement their own SDLC.**

---

## 3. IEC 62443-4-2 Technical Requirements for Edge Devices  
### (Design Guideline for Device Edge & Edge Manager)

RHEL for Edge is not certified for 62443-4-2 by itself.  
However, **proper design + RHEM** can satisfy the majority of SR requirements.

---

## 3.1 IAC – Identification & Authentication (SR 1.x)

### Device Side
- Local account control, password complexity rules  
- Enforced SSH key authentication  
- Least privilege enforcement via sudo  

### Management Side (RHEM)
- Certificate-based device identity and onboarding  
- RBAC for administrators  
- Per-device trust establishment  

---

## 3.2 UC – Use Control (SR 1.4 / 1.5)
- SELinux enforcing for process/file isolation  
- sudoers to restrict permitted actions  
- cgroups and SELinux for container isolation  

---

## 3.3 SI – System Integrity (SR 3.x)

### Device Side
- **Immutable OS (rpm-ostree / bootc)**  
- Secure Boot + kernel/bootloader signature verification  
- `rpm --verify` for integrity checks  
- auditd for integrity monitoring  

### Edge Manager Side
- OTA updates signed and verified  
- Signature validation during `bootc pull`  
- Automatic rollback on failure  

---

## 3.4 DP – Data Protection (SR 4.x)
- LUKS2 full disk encryption  
- FIPS-compliant TLS / SSH  
- Clevis/Tang for automatic unlock (unattended restart capable)  

---

## 3.5 RE – Resource Availability (SR 2.x)
- systemd automatic service restart  
- Optional live patching via kpatch  
- Device health monitoring via RHEM  
- Insights for Edge for risk and performance analysis  

---

## 3.6 TR – Traceability (SR 6.x)
- auditd and journald  
- Central log aggregation (RHEM / Elasticsearch / Loki)  
- OTA update history tracking via RHEM  

> **RHEM enhances auditability and traceability required by 62443-4-2.**

---

# 4. Summary of 4-1 / 4-2 Alignment

| Item | 4-1 (SDLC) | 4-2 (Technical) | Device Edge / RHEM Position |
|------|------------|------------------|------------------------------|
| Identification & Authentication | ✓ | ✓ | Device certificates, RBAC |
| Access Control | ✓ | ✓ | SELinux, sudo, RBAC |
| Encryption | ✓ | ✓ | LUKS2, TLS (FIPS) |
| System Integrity | ✓ | ✓ | Immutable OS, signed OTA |
| Logging & Audit | ✓ | ✓ | auditd + centralized logs |
| Vulnerability Handling | ✓ | △ | RHSA + OTA patching |
| Availability | — | ✓ | systemd, kpatch, Insights |
| OTA Integrity | — | ✓ | bootc signed images |

---

# 5. Recommended User Actions

## 5.1 Mandatory / Strongly Recommended
### Device Level
- Enable **SELinux enforcing**  
- Enforce **SSH key authentication**  
- Enable **Secure Boot**  
- Use **LUKS2 encryption**  
- Adopt **rpm-ostree / bootc immutable OS**  

### OTA / Management Level
- Use **signed OTA images via RHEM**  
- Store and monitor audit logs centrally  

---

## 5.2 Optional (Environment Dependent)
- kpatch (live kernel patching)  
- IdM / Active Directory integration  
- Centralized monitoring & logging  
- Insights for Edge adoption  
- HA clustering for mission-critical workloads  

---
