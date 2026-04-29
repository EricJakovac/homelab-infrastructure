# Multi-node Linux Home Lab i Infrastruktura

## Pregled projekta
Ovaj projekt dokumentira razvoj lokalne R&D infrastrukture namijenjene testiranju kontejneriziranih okruženja, mrežnih servisa i kompatibilnosti različitih Linux distribucija. Lab je izgrađen na **VMware Workstation** platformi i simulira rad u profesionalnom podatkovnom centru.

## Mrežna arhitektura
Infrastruktura se sastoji od četiri specijalizirana čvora povezana unutar virtualne NAT mreže (`192.168.10.0/24`).

| Naziv VM-a | OS | IP adresa | RAM/Disk | Uloga |
| :--- | :--- | :--- | :--- | :--- |
| **SRV-MAIN** | Ubuntu 24.04 LTS | `192.168.10.100` | 4GB / 20GB | Docker Engine, Glavni server |
| **CLI-ALPINE**| Alpine Linux (Virtual) | `192.168.10.129` | 768MB / 8GB | Lagani mrežni klijent |
| **CLI-DEBIAN**| Debian 13 | `192.168.10.102` | 2GB / 10GB | Stabilni SysAdmin klijent |
| **SRV-DNS** | Pi-hole (Docker) | `192.168.10.100` | (Kontejner) | DNS Ad-blocker za cijelu mrežu |

## Tehnologije i vještine
* **Virtualizacija:** VMware Workstation (alokacija resursa, Snapshoti, virtualno umrežavanje).
* **Linux administracija:** Upravljanje korisnicima i grupama (`sudoers`), upravljanje paketima (`apt`, `apk`), rad u terminalu.
* **Mreže:** Konfiguracija statičkih IP adresa, rješavanje problema s DNS rezolucijom, SSH upravljanje.
* **Kontejnerizacija:** Docker Engine, Docker Compose, perzistencija podataka (Volumes).

## Ključne implementacije

### 1. Podešavanje i optimizacija Alpine Linuxa
Alpine je odabran zbog minimalne potrošnje resursa. Riješeni izazovi:
* Omogućavanje `community` repozitorija u `/etc/apk/repositories`.
* Ručna instalacija i konfiguracija `sudo` ovlasti za korisnike.

### 2. Stabilnost Debian sustava
Konfiguriran kao stabilno CLI okruženje za administraciju.
* Implementacija statičkog umrežavanja putem `/etc/network/interfaces`.
* Troubleshooting DNS-a kroz `/etc/resolv.conf`.

### 3. Docker servisi (Pi-hole)
Pi-hole radi kao primarni DNS servis unutar Docker kontejnera.
* **Perzistencija:** Podaci se čuvaju u lokalnim volumenima radi sigurnosti.
* **Mapiranje portova:** Eksponiranje DNS (53) i Web Admin (80) portova prema lokalnoj mreži.

## Screenshots

---
**Autor:** Eric Jakovac
**Datum kreiranja:** 28.04.2026.
