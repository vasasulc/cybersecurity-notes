---
{"dg-publish":true,"permalink":"/hacking/snmp/","dg-note-properties":{}}
---

- Poskytuje obrovské množství informací a statistik o zařízeních v síti.
- Přístup v SNMP v1 a v2c je řízen tzv. **Community stringem** v čistém textu.
- Výchozí od výrobce bývají stringy `public` a `private` a často zůstávají nezměněny.

**Vytěžení dat (vyžaduje znalost stringu):**
`snmpwalk -v 2c -c public <IP> <OID>`

**Bruteforcing community stringů:**
Pro hádání stringů pomocí slovníku se používá nástroj `onesixtyone`:
`onesixtyone -c dict.txt <IP>`