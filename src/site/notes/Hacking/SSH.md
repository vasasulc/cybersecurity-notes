---
{"dg-publish":true,"permalink":"/hacking/ssh/","dg-note-properties":{}}
---

- Síťový protokol, který defaultně běží na **portu 22**
- Poskytuje bezpečný vzdálený přístup k počítači
- Autentizace probíhá přes heslo nebo pomocí veřejného/soukromého klíče (bez hesla)
- Z pohledu útočníka je SSH spojení mnohem stabilnější než běžný reverse shell
- Často se využívá jako "jump host" pro enumeraci a útoky na další stroje v síti nebo pro přenos nástrojů
- **Základní syntaxe připojení:**
  `ssh username@<IP>`