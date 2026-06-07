---
{"dg-publish":true,"permalink":"/hacking/web-enumeration-gobuster/","dg-note-properties":{"Created":"2026-05-01T16:19","Module":"Enumeration"}}
---

# Web enumeration

## Gobuster

- pro nacházení skrytých filů a directories na web serveru

### Directory/File enumeration

- `dir` - directory brute-forcing mode

- `dns` - sudbdomain enumeration mode

- `-u` - url

- `-w` - wordlist

- `-d` - doména

```bash
gobuster dns -d <doména> -w <Cesta k wordlistu>
gobuster dir -u <URL> -w <Cesta k wordlistu>
```

## Web Enumeration tips

### Banner grabbing / Web Server headers

- můžeme použí curl na grabnutí banneru, který nám řekne info o serveru

- `-I` - pošle HEAD request, dostanem zpátky pouze hlavičku

- `-L` - následuje přesměrování např. po přihlášení

```bash
curl -IL <URL>
```

### Whatweb

- vypíše nám verzi serveru, co používá atd.

```bash
whatweb <URL nebo IP adresa>
```

### **Certificates**

- Certifikáty můžou odhalit informace jako emailové adresu nebo jméno firmy

### **Robots.txt**

- říká web crawler botům jaké fily můžou použít pro indexing, může odhalit soukromé soubory

### **Source Code**

- dev může zapomenout heslo v html komentáři

![image.png](/img/user/Hacking/Images/image.png)

### Question 1

- Try running some of the web enumeration techniques you learned in this section on the server above, and use the info you get to get the flag.

![image 1.png](/img/user/Hacking/Images/image%201.png)

![image 2.png](/img/user/Hacking/Images/image%202.png)

![image 3.png](/img/user/Hacking/Images/image%203.png)

![image 4.png](/img/user/Hacking/Images/image%204.png)

- `HTB{w3b_3num3r4710n_r3v34l5_53cr375}`