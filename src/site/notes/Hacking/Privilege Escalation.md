---
{"dg-publish":true,"permalink":"/hacking/privilege-escalation/","dg-note-properties":{"Created":"2026-05-05T14:32","Module":"Post-Exploitation"}}
---

- k získání plného přístupu na serveru (root, admin) tím, že najdeme vulnerability

### Možnosti získání plného přístupu

> [!important]
> 
> Pokud zneužíváme writeable file pro privilege escalation, VŽDY používáme append (>>), abychom nepřepsali původní file a neprozradili se

- Podívat co všechno můžeme s příkazem sudo pomocí commandu `sudo -l`

- [https://gtfobins.github.io/](https://gtfobins.github.io/) nebo [https://lolbas-project.github.io/](https://lolbas-project.github.io/) (Windows) - list commandů, které můžeme zneužít se sudo

- můžeme použít např. skript z [https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite](https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite), ale dělá hodně ruchu

- pokud systém běží na staré verzi OS → podíváme se, jestli neexistuje nějaký kernel exploit

- Zneužít nainstalovaný SW na systému

- přidat scheduled task a spusti přes něj náš skript

- podívat se do souborů, jestli nemají nějaké exposed credentials

#### SSH klíče

- pokud můžeme číst `/root/.ssh/id_rsa` nebo `/home/user/.ssh/id_rsa`
    
    - klíč si zkopírujeme na náš stroj a spustíme command
    
    ```bash
    ssh root@10.10.10.10 -i id_rsa
    ```
    

- pokud můžeme psát do `/home/user/.ssh/authorized_keys`
    
    - vygenerujeme si klíč na našem stroji
    
    ```bash
    ssh-keygen -f key
    ```
    
    - `[key.pub](http://key.pub)` file dáme do souboru na serveru
    
    ```bash
    echo "ssh-rsa AAAAB...SNIP...M= user@parrot" >> /root/.ssh/authorized_keys
    ```
    
    - a přihlásíme se pomocí našeho private key
    
    ```bash
    ssh root@10.10.10.10 -i key
    ```
    

### Question 1

![image 7.png\|image 7.png](/img/user/Hacking/Images/image%207.png)

- `HTB{l473r4l_m0v3m3n7_70_4n07h3r_u53r}`

#### Question 2

![image 1 3.png\|image 1 3.png](/img/user/Hacking/Images/image%201%203.png)

![image 2 3.png\|image 2 3.png](/img/user/Hacking/Images/image%202%203.png)

![image 3 2.png\|image 3 2.png](/img/user/Hacking/Images/image%203%202.png)

- `HTB{pr1v1l363_35c4l4710n_2_r007}`