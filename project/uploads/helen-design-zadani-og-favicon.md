# Zadání pro Claude Design — OG image + favicon heleN

Mám hotový design systém webu autoškoly heleN. Potřebuji od tebe finální exporty dvou grafických souborů přesně v brandových barvách.

## Brand hodnoty
- **Primární barva:** teal `#1B8A7A`
- **Pozadí:** krémová `#FDFCF8`
- **Text:** tmavá `#1B2B2A`
- **Sekundární text / akcent:** `#4A7A74`
- **Typografie:** serif (Georgia / Playfair Display) pro headliny, sans-serif pro kontakty

---

## 1. OG image — 1200 × 630 px

**Soubor:** `og-image.jpg` (nebo PNG), uložit do `/public/`

**Podklady:** Přikládám `og-image.svg` jako přesný layout. Exportuj nebo překresli 1:1 ve správných rozměrech.

**Obsah (zleva doprava, krémové pozadí):**
- Tenký teal pruh na levém okraji (14 px)
- Logo: teal kruh + písmeno „h" serifové bílé + vedle „heleN" serif bold + pod tím „AUTOŠKOLA BRNO" verzálky s letter-spacing
- Oddělovač — jemná teal linka
- Hlavní claim dvě řádky: **„Řídit se naučíte."** (serif bold, tmavá) / *„I když se bojíte."* (serif italic, teal)
- Podtitulek: „Kurzy skupiny B · individuální přístup · Brno"
- Druhý oddělovač
- Kontaktní řádek: `739 122 002 · HeleNautoskola@gmail.com · www.HeleNautoskola.cz`
- Vpravo dekorativní soustředné kruhy teal s nízkou opacity (ambient efekt)

**Technické požadavky:**
- Rozměr: přesně 1200 × 630 px
- Formát: JPG (kvalita 90+) nebo PNG
- Pozadí nesmí být průhledné
- Text musí být čitelný na všech platformách (žádné příliš tenké tahy)

---

## 2. Favicon sada

**Soubory (uložit do `/public/`):**

### favicon.svg
Vektorový zdrojový soubor. Přikládám hotové SVG — zkontroluj a případně uprav jen pokud je potřeba.
- Teal kruh `#1B8A7A` jako pozadí (vyplňuje celý viewport)
- Písmeno „h" — serifové (Georgia), bold, bílá `#FDFCF8`, centrované
- ViewBox: `0 0 512 512`

### favicon.ico
Rastrový soubor se dvěma vrstvami: 16 × 16 px a 32 × 32 px.
- Na 16 px: jen teal kruh + bílé „h" (zjednodušené, čitelné)
- Na 32 px: stejný motiv, detailnější

Jak vytvořit: otevři `favicon.svg` v Inkscape nebo Figma → exportuj jako PNG 32 × 32 → převeď na `.ico` přes [favicon.io](https://favicon.io/favicon-converter/) nebo RealFaviconGenerator.

### apple-touch-icon.png
- Rozměr: přesně 180 × 180 px
- Stejný motiv jako favicon.svg
- **Bez průhlednosti** — teal kruh jako plné pozadí (iOS přidá zaoblení samo)
- Formát: PNG-24

---

## Checklist před odevzdáním

- [ ] `og-image.jpg` — 1200 × 630 px, čitelný text, krémové pozadí
- [ ] `favicon.svg` — 512 × 512 viewBox, kruh + „h"
- [ ] `favicon.ico` — obsahuje 16 × 16 a 32 × 32 vrstvy
- [ ] `apple-touch-icon.png` — 180 × 180 px, bez průhlednosti

Všechny soubory patří do složky `/public/` v projektu.
