# Úprava obsahu

_Started 2026-05-30 19:34 UTC_

---

## User

budeme upravovat toto

## Assistant

_[tool: read_file]_

_[tool: list_files]_

_[tool: list_files]_

## User

Můžeš mi navrhnout vzhled cookies lišty?

## Assistant

_[tool: list_files]_

_[tool: read_file]_

_[tool: grep]_

_[tool: read_file]_

_[tool: copy_starter_component]_

_[tool: read_file]_

Mám dobrý přehled o vašem design systému (krémová, inkoustová tmavá, teal #0064AD, Playfair Display + DM Sans, pilulkové buttony, hravý tón „pro strašpytlíky"). Místo dlouhého vyptávání vám rovnou navrhnu několik variant cookies lišty na plátně, ať máte z čeho vybírat.

_[tool: write_file]_

Design systému rozumím. Postavím vám plátno s několika variantami cookies lišty v duchu značky (hravý tón „bez stresu", teal, krémová, pilulkové buttony, Tabler ikony).

_[tool: done]_

_[tool: fork_verifier_agent]_

Hotovo — na plátně máte **4 varianty cookies lišty** v duchu značky:

- **A · Spodní lišta (světlá)** — klasická krémová lišta přes celou šířku, tři akce + odkaz na nastavení.
- **B · Rohová karta** — kompaktní karta v rohu s hravým tónem („pár drobků").
- **C · Spodní lišta (inkoust)** — tmavá varianta laděná podle hero sekce.
- **D · Detailní nastavení** — panel s přepínači (nezbytné / analytické / marketingové) pro granulární souhlas.

Všechny používají vaše barvy, Playfair + DM Sans, pilulkové buttony a Tabler ikony. Texty mají odlehčený tón „bez stresu" v souladu s autoškolou pro strašpytlíky.

Můžete artboardy přetahovat, přejmenovat nebo otevřít na celou obrazovku. Řekněte mi, **která varianta vás oslovila** — tu pak doladím a rovnou napojím na funkční logiku (uložení souhlasu, otevírání nastavení) přímo do `index.html`.

## User

můžeme udělat kombinaci textu B a vzhledu D?

## Assistant

_[tool: str_replace_edit]_

Jasně — vezmu hravý text z B (pillík „Sušenky", nadpis „Pár drobků pro lepší web", lehčí tón) a posadím ho do panelu s přepínači z D. Přidám to jako novou variantu E, ať máte srovnání.

_[tool: str_replace_edit]_

Pill styluju jen v `.barB` — musím selektor zobecnit, aby fungoval i v panelu E.

_[tool: done]_

_[tool: fork_verifier_agent]_

Přidal jsem **variantu E** — hravý text z B (pillík „Sušenky", nadpis „Pár drobků pro lepší web", lehčí tón) v panelu s přepínači z D. Akce jsem sjednotil na **„Jen nezbytné"** a **„Přijmout vše"** a dole nechal odkaz na zásady.

Najdete ji jako poslední artboard na plátně. Až řeknete, že sedí, můžu ji napojit na funkční logiku přímo do `index.html`.

## User

yes to se mi líbí

## Assistant

_[tool: read_file]_

_[tool: grep]_

Skvělé! Napojím variantu E na funkční logiku přímo do `index.html` — uložení souhlasu do `localStorage`, tlačítka „Přijmout vše" / „Jen nezbytné", přepínače a zobrazení jen při první návštěvě. Mrknu na konec souboru, kam to vložit.

_[tool: grep]_

Web je dvojjazyčný (CZ/UA) přes `.lang` / `.lang-cz` / `.lang-ua`. Cookies lištu udělám taky dvojjazyčnou, ať to ladí. Mrknu na vzor použití v markupu.

_[tool: read_file]_

Rozumím vzoru i18n. Teď to napojím přímo do `uploads/index.html` — variantu E s dvojjazyčnými texty (CZ/UA), uložením do `localStorage`, fungujícími přepínači a plovoucím tlačítkem pro pozdější změnu. Nejdřív vložím CSS.Vkládám CSS cookies lišty před `</style>`:

_[tool: str_replace_edit]_

_[tool: read_file]_

Teď vložím markup po `</footer>` (před skripty):

_[tool: grep]_

_[tool: str_replace_edit]_

_[tool: str_replace_edit]_

Teď přidám logiku do JS před uzavírací `</script>`:

_[tool: done]_

_[tool: fork_verifier_agent]_

Hotovo — varianta E je teď napojená přímo v `uploads/index.html` jako funkční cookies lišta:

- **Zobrazí se** automaticky ~1 s po první návštěvě, pak už ne (souhlas se ukládá do `localStorage`).
- **Tlačítka** — „Jen nezbytné" / „Přijmout vše". Jakmile sáhnete na přepínač, pravé tlačítko se chytře přepne na **„Uložit výběr"**.
- **Přepínače** — nezbytné (vždy), analytické, marketingové.
- **Plovoucí tlačítko se sušenkou** vlevo dole pro pozdější změnu nastavení.
- **Dvojjazyčné** (CZ/UA) — řídí se přepínačem jazyka na webu.

Pustil jsem verifikaci, že se panel objeví a tlačítka/ukládání fungují. Kdybyste chtěl jiné texty, propojit odkaz „Zásady" na samostatnou stránku, nebo měnit prodlevu zobrazení, řekněte.

## User

Verifier agent check completed

## Assistant

Verifikace prošla ✓ — panel se zobrazí, přepínače i tlačítka fungují, souhlas se ukládá a vše běží i v ukrajinské jazykové verzi. Cookies lišta je hotová a napojená v `uploads/index.html`. Kdyby bylo potřeba cokoli doladit, dejte vědět.

## User

Dej ji na pravou stranu webu

## Assistant

_[tool: str_replace_edit]_

_[tool: done]_

Hotovo — cookies lišta i plovoucí tlačítko se sušenkou jsou teď vpravo dole. Na mobilu se panel roztáhne přes celou šířku. Kdyby měl být užší/širší nebo výš, řeknu.

## User

<pasted_text name="Pasted text (42 lines)">
Jsem zkušený webdesignér a vývojář. Mám hotový kompletní design systém a layouty firemního prezentačního webu. Web sbírá osobní údaje přes kontaktní formulář a používá analytiku (Google Analytics / Hotjar). Cílový trh je pouze ČR.
Potřebuji, abys prošel celý design jako senior designer s vývojářskou praxí a identifikoval vše, co chybí nebo je nedotažené – s důrazem na to, aby výstup byl okamžitě použitelný jako podklady pro implementaci v kódu.

1. GDPR a právní povinnosti (ČR)
Zkontroluj a navrhni, zda design obsahuje:

Cookie consent banner – musí umožnit granulární souhlas (nezbytné / analytické / marketingové cookies), odmítnutí musí být stejně snadné jako přijetí, stav souhlasu musí být uložitelný
Zásady zpracování osobních údajů – samostatná stránka nebo modal, odkaz v patičce i v cookie banneru
Kontaktní formulář – checkbox souhlasu se zpracováním OÚ (nebo jasný informační text), validace povinných polí, stav po odeslání (success / error)
Patička – musí obsahovat: název firmy, IČO, sídlo, kontakt, odkaz na GDPR/OÚ, případně obchodní podmínky
Správce OÚ – kde na webu je uvedeno, kdo je správcem dat


2. Přístupnost (WCAG 2.1 AA – standard pro ČR)

Barevné kontrasty – zkontroluj všechny kombinace textu a pozadí (minimálně 4,5:1 pro běžný text, 3:1 pro velký)
Fokus stavy – jsou viditelné a navržené pro všechny interaktivní prvky (tlačítka, linky, inputy, checkboxy)?
Chybové stavy formulářů – jsou vizuálně odlišené, neopírají se pouze o barvu?
Alternativní texty – jsou v designu označeny obrázky, které potřebují alt text?
Touch targets – jsou klikatelné prvky minimálně 44×44px?


3. Technické prvky potřebné pro implementaci
Zkontroluj, zda design pokrývá:

Favicon – je definovaný?
OG image / meta preview – jak má vypadat náhled při sdílení na sociálních sítích?
404 stránka – je navržená?
Prázdné stavy – co se zobrazí, když formulář ještě nebyl odeslán / nenačetla se data?
Loading stavy – zejména u tlačítka odeslání formuláře
Mobilní breakpointy – jsou všechny komponenty navrženy i pro mobil?
Tiskový styl – není nutný, ale u firemního webu občas žádoucí


4. Co chci jako výstup
Pro každý bod výše:

Stav – chybí / je / je ale nedotažené
Co přesně doplnit nebo upravit – popis dostatečně konkrétní pro implementaci
Priorita – musí mít (právní povinnost nebo zásadní UX) / mělo by mít / nice to have

Výstup chci jako strukturovaný checklist, který předám vývojáři (Claude Code) jako zadání k implementaci.
</pasted_text>

## Assistant

_[tool: grep]_

_[tool: grep]_

_[tool: grep]_

Tohle je audit — musím si projít skutečný stav kódu, ne hádat. Projdu hlavičku (meta/favicon/OG), formulář, patičku, focus stavy, alt texty a kontrasty.

_[tool: read_file]_

Žádný favicon, OG, ani meta description; focus styl jen u inputů. Teď formulář a patička.

_[tool: read_file]_

_[tool: read_file]_

Teď začátek formuláře (souhlas se zpracováním OÚ, povinná pole) a CSS chybových stavů.

_[tool: update_todos]_

Mám kompletní obrázek o stavu kódu. Sestavím z toho strukturovaný checklist pro vývojáře (Claude Code) — Markdown, ať se dá rovnou použít jako zadání. Každý bod: **stav / co doplnit / priorita**, s odkazy na konkrétní selektory a tokeny v `index.html`.

_[tool: write_file]_

_[tool: update_todos]_

_[tool: show_to_user]_

Hotovo. Prošel jsem **reálný kód** `index.html` (ne odhady) a sepsal strukturovaný checklist → **`Audit a checklist — helen web.md`**, připravený k předání Claude Code. Každý bod má **stav / co konkrétně doplnit / prioritu** (🔴/🟡/🟢) s odkazy na konkrétní selektory a tokeny.

Nejdůležitější zjištění:

**🔴 Musí mít (právní/zásadní):**
- **Chybí stránka „Zásady zpracování OÚ + cookies"** — banner i patička na ni reálně neodkazují (odkaz v banneru míří na kontakt).
- **IČO v patičce je placeholder** `12345678`; správce OÚ není explicitně označen.
- **Formulář nemá souhlas se zpracováním OÚ** (jen informační věta bez odkazu).
- **Cookie banner zatím jen ukládá volbu** — není napojen na reálný consent gate (GA/Hotjar se musí spustit až po souhlasu).
- **Focus stavy** jsou navržené jen u inputů — tlačítka, odkazy, přepínače spoléhají na default prohlížeče.
- **Kontrast `--green-deep` na text** ~3:1 nevyhovuje; **favicon a OG/meta zcela chybí**.

**Co je dobře:** cookie banner (granulární, odmítnutí = přijetí, uložitelný stav), validace formuláře a chybové stavy se neopírají jen o barvu, success stav, mobilní breakpointy.

Klidně rovnou navrhnu kterýkoli chybějící kus — stránku zásad, OG image + favicon, 404, nebo hotové CSS pro focus-visible a loading stav tlačítka. Řekněte, čím začít.

## User

Mám hotové SVG soubory pro web autoškoly heleN. Potřebuji z nich vyrobit finální exporty pro produkci. Přikládám tři soubory: og-image.svg, favicon.svg a helen-design-zadani-og-favicon.md se specifikací.
Co potřebuji vyexportovat:
Z og-image.svg vyrob og-image.jpg — rozměr 1200 × 630 px, kvalita 90+, bez průhlednosti, krémové pozadí #FDFCF8. Pokud nemůžeš exportovat JPG, dodej PNG.
Z favicon.svg vyrob tři soubory:

favicon.ico se dvěma vrstvami 16 × 16 a 32 × 32 px
apple-touch-icon.png přesně 180 × 180 px, bez průhlednosti, teal kruh #1B8A7A jako plné pozadí
favicon.svg zkontroluj a potvrď že je správně (viewBox 0 0 512 512, kruh + písmeno „h")

Všechny výstupní soubory patří do složky /public/.

## Assistant

_[tool: read_file]_

_[tool: read_file]_

Mrknu na specifikaci a oba SVG soubory.

_[tool: read_file]_

_[tool: run_script]_

Oba SVG jsou v pořádku. **`favicon.svg` odpovídá specifikaci** — viewBox `0 0 512 512`, plný teal kruh `#1B8A7A`, bílé serifové „h" (Georgia, bold). Teď vyrobím rastrové exporty do `public/`.

_[tool: run_script]_

Canvas v sandboxu používá `convertToBlob`. Upravím helper.

_[tool: image_metadata]_

_[tool: image_metadata]_

_[tool: view_image]_

Vyexportováno. Ověřím rozměry, průhlednost a vzhled.

_[tool: view_image]_

_[tool: image_metadata]_

OG image vyšla skvěle — serifové fonty, teal, layout 1:1, 1200×630, bez průhlednosti, 78,5 KB. Mrknu na favicon (apple-touch a ico).

_[tool: run_script]_

apple-touch-icon je perfektní (teal pozadí, bílé „h"). Metadata tool `.ico` nepodporuje (není v jeho seznamu formátů), takže si platnost ověřím přečtením bytů.

_[tool: present_fs_item_for_download]_

Vše ověřeno a hotovo. Soubory v `public/`:

| Soubor | Stav |
|---|---|
| **og-image.jpg** | 1200×630, JPEG q95 (78,5 KB), krémové pozadí, **bez průhlednosti** ✓ — layout 1:1 dle SVG, serif claim čitelný |
| **favicon.svg** | ověřeno — viewBox `0 0 512 512`, teal kruh `#1B8A7A` + bílé serifové „h" ✓ (zkopírováno beze změny) |
| **favicon.ico** | platný ICO, **dvě vrstvy 16×16 a 32×32** (PNG-in-ICO, podporuje prohlížeč i Windows) ✓ |
| **apple-touch-icon.png** | přesně 180×180, teal `#1B8A7A` jako plné pozadí, plně neprůhledné ✓ |

Drobná poznámka: `apple-touch-icon.png` má alfa kanál, ale **žádný průhledný pixel** (plně opaque) — iOS i tak funguje správně a zaoblení si přidá samo.

Doporučené `<head>` napojení:
```html
<link rel="icon" href="/favicon.ico" sizes="32x32">
<link rel="icon" href="/favicon.svg" type="image/svg+xml">
<link rel="apple-touch-icon" href="/apple-touch-icon.png">
<meta property="og:image" content="/og-image.jpg">
<meta property="og:image:width" content="1200">
<meta property="og:image:height" content="630">
```Hotové exporty máte ke stažení výše. 👆

