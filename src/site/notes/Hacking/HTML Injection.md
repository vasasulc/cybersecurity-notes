---
{"dg-publish":true,"permalink":"/hacking/html-injection/","dg-note-properties":{"Created":"2026-05-02T13:21","Module":"Exploiting"}}
---

- nastane, když se nefiltrovaný uživatelský vstup objeví na stránce

```html
<style> body { background-image: url('https://academy.hackthebox.com/images/logo.svg'); } </style>
```