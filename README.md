# 🌐 Oppgave 8 — EternalBlue, nettverksspor & analyse

## 📌 Formål
Dette prosjektet dokumenterer en laboratorieøvelse der jeg:
1) identifiserer **MS17-010 (EternalBlue)**-sårbarhet,
2) oppnår tilgang via **Metasploit** (SMB/psexec → reverse shell),
3) samler nettverksspor på Windows med **netsh trace** og konverterer **ETL → PCAPNG**, og
4) analyserer trafikk i **Wireshark** for å hente ut HTTP-kredentialer (brukernavn/passord) og **CSRF-token**.  
Alt er utført i et isolert testmiljø med uttrykkelig tillatelse.

---

## 🔍 Innhold
Repoet dekker:

- **Scope:** Isolert Kali (angriper) + Windows (offer) i labnett  
- **Metodikk:** Nmap-funn → Metasploit-tilgang → `netsh trace` → `etl2pcapng` → Wireshark-funn  
- **Etikk & lovverk:** Teknikker skal **kun** brukes kontrollert og med eksplisitt samtykke

---

## 🛠️ Verktøy brukt
- **Nmap** – detektere MS17-010 (EternalBlue)  
- **Metasploit Framework** – SMB/psexec med `windows/x64/shell_reverse_tcp`  
- **netsh trace** (Windows) – nettverksinnsamling til `.etl`  
- **etl2pcapng** – konvertering fra `.etl` til `.pcapng`  
- **Wireshark** – protokollanalyse (HTTP-felter, cookies, CSRF)

---

## 📊 Viktigste funn / observasjoner
- Vert sårbar for **MS17-010** kan gi rask laterale bevegelser via SMB.  
- **Reverse shell** etablert med psexec bekrefter praktisk utnyttbarhet.  
- **ETL → PCAPNG** muliggjør full HTTP-inspeksjon: POST-felter, cookies, og **CSRF-token** kan identifiseres i klartekst hvis trafikken ikke er kryptert.  
- **Sikkerhetsimplikasjoner:** Uoppdaterte systemer + ukryptert HTTP eksponerer legitimasjon.  
- **Mottiltak:** Patch MS17-010, deaktiver SMBv1, håndhev TLS, segmentér nettverk, strengere kontopolicy og overvåkning.

---

## 📑 Repo-struktur
```bash
oppgave8-eternalblue-trace2pcap/
│── README.md
│── LICENSE
│── LAB.md      
