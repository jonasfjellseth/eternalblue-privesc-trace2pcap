# LAB: EternalBlue, nettverksspor & analyse

## Forutsetninger
- Kali (angriper) med `nmap`, `metasploit-framework`, `smbclient`.
- Windows offer-VM med lokal administrator-tilgang.
- `etl2pcapng` installert (for ETL → PCAPNG).
- Wireshark for analyse.
- Isolert testmiljø med eksplisitt samtykke (bruk kun i lab).

---

## Steg 1 — Finn MS17-010 (EternalBlue) med Nmap
<img width="869" height="660" alt="2  Nmap script scan" src="https://github.com/user-attachments/assets/cd3d52e7-d622-4d86-973a-2c1c56411dcb" />

*Kjør sårbarhetssøk mot offer-VM for å bekrefte MS17-010 (EternalBlue).*

---


## Steg 2 - Utnyttelse med Metasploit (psexec -> reverse shell)

<img width="866" height="594" alt="3  Msfconsole start" src="https://github.com/user-attachments/assets/5efd89a2-a52d-4808-b8be-14db8171163b" />

*Åpner Metasploit*

<img width="882" height="709" alt="4  Msfconsole search eternalblue model 10" src="https://github.com/user-attachments/assets/cac1ed8a-452d-45bc-a689-a218ebb3326c" />

*Søker etter relevant modul*

<img width="719" height="59" alt="5  Msfconsole use module 10" src="https://github.com/user-attachments/assets/9bbe9ecb-d1e8-4109-9d08-4a17f8f1203f" />

<img width="1042" height="1018" alt="6  Msfconsole show options set RHOSTS, set PAYLOAD" src="https://github.com/user-attachments/assets/372fffbb-1a44-492e-bbf9-21f9c249039b" />

*Setter opp angrep mot vert*

<img width="1038" height="399" alt="7  Msfconsole exploit, shell" src="https://github.com/user-attachments/assets/fa9c8316-4435-4c1a-a92b-f05e7d7b6b18" />

*Reverse shell etablert mot offer-VM*

## Steg 3 - Start nettverkssporing på Windows (netsh trace)

<img width="845" height="609" alt="9  mkdir, netsh trace start" src="https://github.com/user-attachments/assets/671a7799-7b34-414d-b29f-4b380e543e7b" />

*Start ETL-sporingen for å fange opp HTTP-trafikk og annen nettverksaktivitet*

## Steg 4 - Generere trafikk (innlogging i webapp)

<img width="790" height="461" alt="12  Futura Mnguyen credentials" src="https://github.com/user-attachments/assets/faebe1b1-d94b-49b0-9874-d0b2af6cd785" />

<img width="788" height="460" alt="13  Futura Mnguyen login side" src="https://github.com/user-attachments/assets/5a551666-32e9-467a-a030-dc4c6b48b307" />

*Logger inn med brukernavn/passord for å generere HTTP-POST og cookies/CSRF i klartekst*

## Steg 5 - Stopper trace og eksporterer ETL med SMB

<img width="861" height="382" alt="16  Overføring med SMB, network_trace etl i Oppgave8 kali" src="https://github.com/user-attachments/assets/40dd3025-cb67-4df0-8352-3788ef155094" />

*Bruker SMB til å overføre ETL filen fra vertsVM'en til kali maskinen.*

## Steg 6 - Konverterer ETL til pcapng

<img width="1091" height="97" alt="18  etl2pcapng convert til pcapng" src="https://github.com/user-attachments/assets/7ffdda6f-13f1-4102-ba07-d8f484c7c941" />

*Bruker programmet etl2pcapng for å bruke filen i Wireshark*

## Steg 7 - Analyserer filen i Wireshark (HTTP-credentials / CSRF)

<img width="1080" height="549" alt="20  Wireshark, filtrer http, brukernavn og passord" src="https://github.com/user-attachments/assets/3228b2f9-df0f-453a-ad78-6c0336369f4d" />

*Finner POST med login-credentials i klartekst*

