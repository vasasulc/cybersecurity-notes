---
{"dg-publish":true,"permalink":"/hacking/netcat/","dg-note-properties":{}}
---

- Excelentní síťová utilita pro interakci s TCP/UDP porty
- Primární využití v pentestingu je připojování k shellům
- Lze ho využít k technice zvané **Banner Grabbing** pro identifikaci služby běžící na daném portu. **Příklad Banner Grabbingu (připojení na SSH port):** 
  `netcat <IP> 22` 
- **Alternativa: Socat** Podobná, ale pokročilejší utilita je [[Socat\|Socat]]. Na rozdíl od Netcatu umí Socat upgradovat shell na plně interaktivní TTY, což z něj dělá kritický nástroj pro stabilní reverse shelly.