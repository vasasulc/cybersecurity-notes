---
{"dg-publish":true,"permalink":"/hacking/smb/","dg-note-properties":{}}
---

- Rozšířený protokol na Windows strojích, běží typicky na **portu 445**
- Slouží ke sdílení složek a souborů, které často obsahují citlivá data jako hesla
- Starší verze mohou být zranitelné na RCE exploity jako **EternalBlue**
  **Enumerace a připojení přes smbclient:** 
- Zjištění dostupných složek (shares) bez zadání hesla (`-N` potlačuje prompt na heslo):
- `smbclient -N -L \\\\<IP>`
- Připojení do konkrétní sdílené složky jako specifický uživatel: `smbclient -U <username> \\\\<IP>\\<share_name>` 
- *Uvnitř lze opět používat příkazy `ls`, `cd` a `get` pro stažení souborů.*