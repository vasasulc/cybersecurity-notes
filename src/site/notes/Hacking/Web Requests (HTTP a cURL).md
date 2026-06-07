---
{"dg-publish":true,"permalink":"/hacking/web-requests-http-a-c-url/","dg-note-properties":{"Created":"2026-05-01T15:11","Module":"Enumeration"}}
---

## HTTP

### Request Methods

|Metoda|Popis|
|---|---|
|GET|žádá o specifický zdroj|
|POST|vytváří nové položky|
|PUT|aktualizuje položky|
|PATCH|aktualizuje pouze část položky|

### Status Codes

|Kód|Popis|
|---|---|
|1xx|Poskytuje informace a neovlivňuje request|
|2xx|Request se povedl|
|3xx|server redirectnul klienta|
|4xx|nesprávný request klienta|
|5xx|problém se serverem|

|Kód|Popis|
|---|---|
|200 OK|request byl úspěšný|
|301 Moved Permanently|URL požadovaného zdroje se trvale změnilo|
|302 Found|URL požadovaného zdroje se dočasně změnilo|
|400 Bad Request|Server nepochopil request kvůli nesprávnému syntaxu|
|401 Unauthorized|Server neví kdo si a nepustí tě, je potřeba autentizace|
|403 Forbidden|Klient k tomuto zdroji nemá přístup|
|404 Not Found|Server zdroj nemůže najít|
|405 Method Not Allowed|Daná metoda je zakázána a nemůže být použita|
|408 Request Timeout|Server čekal moc dlouho na request|
|500 Internal Server Error|Server se dostal do situace s kterou si neví rady|
|502 Bad Gateway|Server kontaktoval jiný server aby mohl požadavek zpracovat, ale dostal nesprávnou odpověď|
|504 Gateway Timeout|Server funguje jako brána a nestihl poslat response|

## cURL

- na zadávání web requestů

```bash
curl -i <URL>  # Vypíše odpověď i s HTTP hlavičkami
curl -X POST -d "user=admin&pass=123" <URL>  # Odeslání POST requestu s daty
curl -H "Authorization: Bearer <token>" <URL>  # Přidání vlastní hlavičky
curl -X POST <URL> -d '{"city_name":"HTB_City", "country_name":"HTB"}' -H 'Content-Type: application/json'
```

|Přepínač|Popis|
|---|---|
|`-v`|všechny detaily o request a response včetně headerů|
|`-I`|pošle HEAD request (ukáže pouze response header)|
|`-H`|určení request headerů např. Authorization, Content-Type|
|`-A`|explicitně určuje User-Agenta|
|`-i`|response header + response body|
|`-u`|poskytnutí credentials serveru pokud má basic HTTP auth|
|`-X`|typ metody např. POST, PUT, DELETE|
|`-d`|posílá data na server|
|`-b`|nastavení cookie|
|`-s`|tichý režim|

## CRUD API

- pro interakci s databází

|Operace|HTTP metoda|Popis|
|---|---|---|
|`Create`|`POST`|přidá data do databáze|
|`Read`|`GET`|přečte data v databázi|
|`Update`|`PUT, PATCH`|aktualizuje data v databázi|
|`Delete`|`DELETE`|vymaže data v databázi|

### URL Encoding

- převede nebezpečné znaky v URL např. mezeru do formátu %xx

- mezera = %20

- apostrof `'` = %27

- Uvozovka `"` = %22

![image 5.png\|image 5.png](/img/user/Hacking/Images/image%205.png)

### Formátování XML výstupu

```bash
curl -s http://10.129.42.190/nibbleblog/content/private/users.xml | xmllint  --format -
```