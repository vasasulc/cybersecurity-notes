---
{"dg-publish":true,"permalink":"/hacking/vim/","dg-note-properties":{}}
---

- Textový editor na Linux systémech, který se ovládá výhradně klávesnicí.
- Bývá nainstalován na většině kompromitovaných Linux systémů, takže jeho znalost je nutná pro úpravu souborů na cíli.

**Režimy (Módy):**
- **Normal mode:** Výchozí režim po otevření souboru, slouží pro čtení a navigaci.
- **Insert mode:** Režim pro psaní úpravu textu. Vstupuje se do něj klávesou `i`. Návrat zpět do Normal módu probíhá klávesou `ESC`.
- **Command mode:** Vstupuje se do něj z Normal módu stisknutím `:` a slouží k ukládání nebo zavírání.

**Příkazy v Command módu (`:`):**
- `:w` - Uložit soubor
- `:q` - Zavřít (Ukončit)
- `:q!` - Zavřít bez uložení
- `:wq` - Uložit a zavřít

**Klávesové zkratky v Normal módu:**
- `dd` - Vyjmout (Cut) celý řádek
- `yy` - Zkopírovat (Copy) celý řádek
- `p` - Vložit (Paste)