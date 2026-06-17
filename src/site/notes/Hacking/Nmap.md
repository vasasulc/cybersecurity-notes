---
{"dg-publish":true,"permalink":"/hacking/nmap/","dg-note-properties":{"Created":"2026-05-05T16:15","Module":"Recon"}}
---

- na skenování dostupných portů a grabování bannerů

```bash
nmap -sV --open -oA initial_scan <IP>
```

```Shell
nmap -p- --open -oA full_tcp_scan <IP>
```

```bash
nmap -sC -p 22,80 -oA script_scan <IP>
```

```bash
nmap -sV --script=http-enum <IP>
```

```shell
nmap -sV --script=banner <IP>
```
Banner Grabbing pro identifikaci služeb na portech
```shell
nmap --script smb-os-discovery.nse -p445 <IP>
```
Využije Nmap skript k vytažení přesné verze OS skrze službu [[Hacking/SMB\|SMB]]

| Přepínač (Switch) | Popis v kontextu zadání                                                                   |
| ----------------- | ----------------------------------------------------------------------------------------- |
| -sV               | Provede skenování pro zjištění verzí běžících služeb.                                     |
| --open            | Zajistí, že se ve výsledcích zobrazí pouze otevřené porty.                                |
| -oA               | Uloží výstup skenu ve všech formátech najednou (text, XML, greppable).                    |
| -v                | Zapne „verbose“ režim pro detailnější výpis informací během skenování.                    |
| -oG               | Uloží výstup ve formátu vhodném pro nástroj grep (greppable format).                      |
| -p-               | Příkaz pro skenování všech 65 535 dostupných portů.                                       |
| -sC               | Spustí skenování s využitím sady výchozích (default) Nmap skriptů.                        |
| -p                | Slouží ke specifikaci konkrétních portů, které se mají skenovat (např. -p 22,80)          |
| --script=         | Umožňuje spustit konkrétní vybraný skript (v textu použit http-enum pro hledání adresářů) |