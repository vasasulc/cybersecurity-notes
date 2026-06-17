---
{"dg-publish":true,"permalink":"/hacking/cross-site-scripting-xss/","dg-note-properties":{"Created":"2026-05-02T13:32","Module":"Exploiting"}}
---

- Injectování JavaScript kódu, který se spustí na klientovi, abych mu např. ukradl cookies

- Stejný princip jako HTML Injection, ale pokročilejší

|Typ|Popis|
|---|---|
|Reflected XSS|Nastává, když se uživatelský vstup objeví na stránce po zpracování např. search result|
|Stored XSS|Nastává, když se uživatelský vstup uloží do back end databáze a ukáže se po vyhledání např. komentář nebo post|
|DOM XSS|Nastává, když se uživatelský vstup přímo ukáže v browseru a je zapsán do HTML DOM objektu např. vulnerable username|

```jsx
#"><img src=/ onerror=alert(document.cookie)> // ukáže cookie value
```
