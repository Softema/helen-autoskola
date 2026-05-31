# Audit webu heleN — zadání pro implementaci

> Senior design + dev review webu `uploads/index.html` (jednostránková SPA, dvojjazyčná CZ/UA, kontaktní formulář + analytika, trh ČR).
> Stav ke dni 31. 5. 2026. Legenda priorit: **🔴 musí mít** (právní povinnost / zásadní UX) · **🟡 mělo by mít** · **🟢 nice to have**.
> Stav: **CHYBÍ** · **JE** · **NEDOTAŽENÉ**.

---

## 1 · GDPR a právní povinnosti (ČR)

### 1.1 Cookie consent banner — **JE** 🔴
Implementováno (`#cookieConsent`, varianta E). Splňuje:
- granulární souhlas: nezbytné (zamčené) / analytické / marketingové (`#ckAnalytics`, `#ckMarketing`);
- odmítnutí stejně snadné jako přijetí — „Jen nezbytné" vedle „Přijmout vše" (stejná váha, vedle sebe);
- stav se ukládá do `localStorage` pod `helen.cookies` + timestamp;
- znovuotevření přes plovoucí tlačítko `#cookieFab`.

**Co dotáhnout:**
- [ ] **Napojit na reálné skripty.** Dnes banner jen ukládá volbu. Analytika (GA / Hotjar) se musí načítat **až po** souhlasu, ne při loadu. Implementovat „consent gate": GA4 spouštět přes `gtag('consent','update', …)` (Consent Mode v2), Hotjar inicializovat až ve větvi `prefs.analytics === true`. 🔴
- [ ] **Marketingová větev** — pokud reálně neběží žádné marketingové cookies, přepínač „Marketingové" odstranit (nemít prázdnou kategorii). Pokud poběží (FB Pixel apod.), napojit stejným gate. 🟡
- [ ] **Verzování souhlasu** — k uloženému stavu přidat `version` a při změně zásad si znovu vyžádat souhlas. 🟡
- [ ] **Expirace** — souhlas znovu vyžádat po 6–12 měsících (kontrola `ts`). 🟡
- [ ] Odkaz „Zásady ochrany soukromí" v banneru dnes míří na `data-nav="contact"` → po vytvoření samostatné stránky (1.2) přesměrovat tam. 🔴

### 1.2 Zásady zpracování osobních údajů (stránka) — **CHYBÍ** 🔴
Na webu není samostatná stránka ani modal s GDPR informacemi. Footer ani banner na ni reálně neodkazují.

**Co doplnit:**
- [ ] Vytvořit stránku/route `privacy` (stejný `data-nav` SPA mechanismus jako home/about/courses/contact) **a** sekci „Zásady cookies". 🔴
- [ ] Povinný obsah: totožnost a kontakt správce, účel a právní základ zpracování (kontaktní formulář = oprávněný zájem / souhlas; analytika = souhlas), kategorie údajů, doba uložení, příjemci/zpracovatelé (Google, Hotjar, hosting), práva subjektu (přístup, oprava, výmaz, námitka), kontakt na ÚOOÚ. 🔴
- [ ] Tabulka cookies (název, účel, doba platnosti, kategorie). 🟡
- [ ] Odkaz z patičky i z cookie banneru. 🔴

### 1.3 Kontaktní formulář — **NEDOTAŽENÉ** 🔴
`#contactForm` má povinná pole (`required` na name/phone/email/message), JS validaci (`validEmail`, `validPhone`), error stavy (`.form-row.error` → barva + text) a success stav (`#formSuccess`). Pod tlačítkem je informační text „Vaše údaje neukládáme nikam mimo tuto poptávku."

**Co doplnit:**
- [ ] **Souhlas / informační text s odkazem.** Stávající `.form-note` nezmiňuje a neodkazuje na zásady. Buď (a) přidat zaškrtávací checkbox „Souhlasím se zpracováním osobních údajů" s odkazem na stránku 1.2 a blokovat odeslání bez něj, nebo (b) ponechat informační režim, ale doplnit větu + odkaz: „Odesláním souhlasíte se [zpracováním osobních údajů](privacy)." U autoškoly (B2C, citlivý kontext) doporučuji **checkbox**. 🔴
- [ ] **Error stav odeslání.** Dnes handler synchronně skryje formulář a ukáže success — neřeší selhání odeslání na server. Doplnit stav „odeslání se nezdařilo, zkuste znovu / zavolejte". 🟡
- [ ] **Loading stav tlačítka** — viz 3.5. 🟡
- [ ] `aria-invalid="true"` na chybných polích a `aria-describedby` mířící na příslušný `.form-error` (dnes se text jen vizuálně zobrazí, screen reader vazbu nemá). 🟡
- [ ] `novalidate` na `<form>` je vhodné ponechat (vlastní hlášky), ale ujistit se, že JS validace pokrývá i `select` při povinnosti (dnes nepovinný — OK). 🟢

### 1.4 Patička — **NEDOTAŽENÉ** 🔴
`.footer-bottom` obsahuje: „© 2026 Autoškola heleN · Helena Harvotová · IČO 12345678". V kontaktech adresa, telefon, e-mail.

**Co doplnit:**
- [ ] **Skutečné IČO** — `12345678` je placeholder. Doplnit reálné. 🔴
- [ ] Odkaz na **Zásady zpracování OÚ** a **Zásady cookies** (stránka 1.2). 🔴
- [ ] Doplnit, zda je firma plátce DPH / DIČ (pokud relevantní). 🟡
- [ ] Obchodní podmínky kurzů (storno, platby) — pro autoškolu prodávající službu doporučeno. 🟡
- [ ] Sjednotit právní formu názvu (OSVČ „Helena Harvotová" vs. „Autoškola heleN" jako značka). 🟢

### 1.5 Správce osobních údajů — **NEDOTAŽENÉ** 🟡
Totožnost správce lze odvodit z patičky (jméno + IČO + adresa), ale **není nikde explicitně označena** jako „Správce osobních údajů".

**Co doplnit:**
- [ ] Na stránce 1.2 uvést blok „Správcem osobních údajů je: [jméno/firma], IČO, sídlo, e-mail, telefon." 🔴 (v rámci 1.2)
- [ ] Pokud existuje pověřenec (DPO) — uvést; u malé autoškoly typicky není povinný. 🟢

---

## 2 · Přístupnost (WCAG 2.1 AA)

### 2.1 Barevné kontrasty — **NEDOTAŽENÉ** 🟡
Tokeny v `:root`. Rizikové kombinace k ověření / opravě:
- [ ] **`--muted` `#737373` na krémové** — na `--cream` ~4,7:1 (těsně projde), ale na tmavších plochách `--cream-2 #F4F1E8` / `--cream-3` klesá pod **4,5:1**. Používá se na drobném textu (`.form-note`, `.ck-od`, `.contact-list .label`, popisky). Ztmavit na cca `#6A6A6A`–`#666`. 🟡
- [ ] **`--green-deep` `#4E9E32` na krémové** ~3,0:1 — **nevyhovuje** pro běžný text. Týká se `.ck-req` („Vždy") a `.success-icon`/odškrtnutí. Pro text použít tmavší odstín (např. `#3C7A26`) nebo zvětšit/zvýraznit jinak než barvou. 🔴
- [ ] Ověřit **placeholder** texty v inputech (`--cream-2` pozadí) — výchozí placeholder bývá pod 4,5:1; nastavit explicitní barvu ≥ `#6A6A6A`. 🟡
- [ ] Ověřit světlé texty na `--ink` (hero-sub `rgba(253,252,248,.7)`, badge `.8`) — pravděpodobně OK, ale potvrdit ≥ 4,5:1. 🟢
- [ ] Stavy `:hover`/`:active` u ghost tlačítek nesmí kontrast zhoršit. 🟢

### 2.2 Fokus stavy — **NEDOTAŽENÉ** 🔴
Jediný navržený focus je na inputech (`.form-row …:focus` → modrý prsten). Tlačítka, odkazy, navigace, přepínač jazyka, burger, cookie přepínače, FAB **nemají navržený focus** — spoléhají na nekonzistentní výchozí outline prohlížeče.

**Co doplnit:**
- [ ] Globální `:focus-visible` styl pro všechny interaktivní prvky — viditelný prsten (např. `outline: 2px solid var(--teal); outline-offset: 2px;` nebo `box-shadow: 0 0 0 3px rgba(0,100,173,.4)`), sladěný se stylem inputů. 🔴
- [ ] Na tmavých plochách (hero, footer, banner C) použít světlou variantu prstenu, aby byl vidět. 🔴
- [ ] Vlastní cookie přepínače (`.ck-tg input`) mají `opacity:0` input — ověřit, že `:focus-visible` prsten je vidět na `.track`/`.knob`. 🔴
- [ ] Pořadí fokusu při otevření cookie banneru přesunout dovnitř dialogu a vrátit zpět po zavření; přidat trap (`role="dialog"` už je). 🟡

### 2.3 Chybové stavy formulářů — **JE** (drobnost) 🟡
`.form-row.error` mění **rámeček + pozadí + zobrazí textovou hlášku** → neopírá se jen o barvu. Dobré.
- [ ] Doplnit ikonu (např. `ti-alert-circle`) k hlášce pro jednoznačnost a `aria-invalid`/`aria-describedby` (viz 1.3). 🟡

### 2.4 Alternativní texty — **JE (zatím N/A)** 🟡
V designu nejsou žádné `<img>` — vizuály jsou ikonové fonty (Tabler `<i>`) a CSS gradientové placeholdery (avatar instruktorky, mapa). Texty popisků jsou vždy vedle ikon.

**Co hlídat při implementaci:**
- [ ] Reálná **fotka instruktorky** (dnes `.avatar` gradient s „h") → `alt="Helena Harvotová, instruktorka autoškoly"`. 🟡
- [ ] **Mapa** (`.map-placeholder`) → pokud se nahradí embedem/obrázkem, doplnit `alt`/`title` a `iframe title`. 🟡
- [ ] Dekorativní ikony nechat bez popisu (`aria-hidden="true"` na `<i class="ti …">`, zejm. tam, kde stojí samostatně). 🟢
- [ ] Logo jako odkaz na úvod má textový obsah „helen" — OK. 🟢

### 2.5 Touch targets (min. 44×44 px) — **NEDOTAŽENÉ** 🟡
- [ ] **Cookie přepínače** `.ck-tg` 44×26 px — rozšířit klikací plochu na ≥44 px výšky (např. padding na `<label>` nebo zvětšit). 🟡
- [ ] **Přepínač jazyka** `.lang-toggle button` (`padding:.35rem .65rem`, ~30 px) — zvětšit na ≥44 px. 🟡
- [ ] **Odkazy v navigaci a patičce** — drobné, na mobilu zvětšit klikací plochu (`padding`/`min-height`). 🟡
- [ ] Burger 44×44 ✓, `.ck-fab` 48×48 ✓, `.btn` ~48 px ✓. 🟢

### 2.6 Další (nad rámec zadání, ale AA) 🟡
- [ ] **Skip-link** „Přeskočit na obsah" před headerem. 🟡
- [ ] `prefers-reduced-motion` — vypnout animace stránek (`pageIn`) a transitiony banneru. 🟡
- [ ] Jazykový přepínač mění `<html lang>` (JS `applyLang` to dělá ✓) — ověřit, že `lang` sedí i na UA obsahu. 🟢
- [ ] Cookie dialog: zavření klávesou Esc není u consent banneru nutné (nesmí jít „odkliknout pryč" bez volby) — ponechat. 🟢

---

## 3 · Technické prvky pro implementaci

### 3.1 Favicon — **CHYBÍ** 🔴
V `<head>` není žádná ikona.
- [ ] Doplnit sadu: `favicon.svg`, `favicon.ico` (32px), `apple-touch-icon.png` (180×180), `site.webmanifest`. Motiv: značka „h" v teal kruhu na krémové (lze odvodit z `#__bundler_thumbnail`). 🔴
```html
<link rel="icon" href="/favicon.ico" sizes="32x32">
<link rel="icon" href="/favicon.svg" type="image/svg+xml">
<link rel="apple-touch-icon" href="/apple-touch-icon.png">
<link rel="manifest" href="/site.webmanifest">
```

### 3.2 OG image / meta preview — **CHYBÍ** 🔴
V `<head>` je jen `charset`, `viewport`, `title`. Chybí description i veškerá OG/Twitter meta.
- [ ] Doplnit: `meta description` (CZ), `og:title`, `og:description`, `og:image`, `og:url`, `og:type=website`, `og:locale=cs_CZ`, `twitter:card=summary_large_image`. 🔴
- [ ] **OG image 1200×630** — návrh: krémové pozadí, vlevo serifový headline „Řídit se naučíte. I když se bojíte.", logo heleN, teal akcent; vpravo prostor pro motiv. (Můžu vyrobit hotový obrázek.) 🔴
- [ ] `lang`/`og:locale` varianta pro UA, pokud poběží i ukrajinské sdílení. 🟢

### 3.3 Stránka 404 — **CHYBÍ** 🟡
SPA řeší obsah přes `data-nav`; pro přímý vstup na neexistující URL není fallback.
- [ ] Navrhnout a implementovat 404: krémové pozadí, serifový nadpis (v duchu značky, např. „Tahle cesta nikam nevede."), tlačítko „Zpět domů" + telefon. Dvojjazyčně. 🟡
- [ ] Na hostingu nastavit, aby neznámé cesty vracely 404 (a/nebo rewrite na SPA + JS 404 stav). 🟡

### 3.4 Prázdné stavy — **JE / N/A** 🟢
Web nemá datově řízené seznamy. Výchozí stav formuláře = prázdný formulář; po odeslání `#formSuccess`. Reset přes `#resetForm`. Pokrytí dostatečné.
- [ ] Jediné doplnění: kdyby přibyl dynamický obsah (recenze, termíny), navrhnout prázdný stav. 🟢

### 3.5 Loading stavy — **CHYBÍ** 🟡
`form submit` skryje formulář okamžitě, bez async/loadingu.
- [ ] Při odeslání: tlačítko `.form-submit` do stavu `disabled` + spinner/„Odesílám…", po odpovědi success/error. Přidat `.btn.is-loading` styl (spinner z `ti-loader-2` + `@keyframes spin`). 🟡
- [ ] Zamezit dvojímu odeslání. 🟡

### 3.6 Mobilní breakpointy — **JE** (ověřit) 🟡
Hojně použité `@media` (900/800/700/500/480 px), `clamp()`, mobilní menu (`.mobile-menu`). Většina komponent pokryta.
- [ ] **Cookie banner** na ≤480 px se roztáhne přes šířku (řešeno) — vizuálně potvrdit, že nepřekrývá obsah a respektuje `safe-area-inset` (iOS notch): přidat `padding-bottom: env(safe-area-inset-bottom)`. 🟡
- [ ] `.ck-fab` vlevo/vpravo dole ať nekoliduje s mobilním menu a sticky CTA. 🟢
- [ ] Projít reálná zařízení 360/390/414 px — tabulky cen, ceník, footer grid. 🟡

### 3.7 Tiskový styl — **CHYBÍ** 🟢
- [ ] `@media print`: skrýt header/nav/footer/cookie/FAB, rozbalit všechny SPA „pages", černý text na bílé, zobrazit kontakt a ceník. Užitečné pro tisk ceníku. 🟢

---

## Souhrn priorit

**🔴 Musí mít (právní / zásadní):**
1. Stránka „Zásady zpracování OÚ + cookies" (1.2) a propojení z patičky i banneru.
2. Reálné IČO v patičce (1.4) + explicitní označení správce (1.5).
3. Souhlas se zpracováním OÚ u formuláře (1.3).
4. Napojení cookie banneru na reálný consent gate analytiky (1.1).
5. Globální navržené `:focus-visible` stavy (2.2).
6. Kontrast `--green-deep` na text (2.1).
7. Favicon (3.1) a OG/meta (3.2).

**🟡 Mělo by mít:**
Loading + error stav formuláře (3.5/1.3), `aria-invalid`/`describedby` (1.3), touch targety přepínačů a jazyka (2.5), kontrast `--muted` (2.1), 404 (3.3), skip-link + reduced-motion (2.6), verzování/expirace souhlasu (1.1), obchodní podmínky (1.4), safe-area na banneru (3.6).

**🟢 Nice to have:**
Tiskový styl (3.7), ikona u chybové hlášky (2.3), prázdné stavy pro budoucí dynamický obsah (3.4), DIČ/právní forma (1.4).

---

### Co umím rovnou dodat jako design (řekněte)
- Stránku **Zásady zpracování OÚ + cookies** v layoutu webu (SPA route `privacy`).
- **OG image** 1200×630 a **favicon** sadu.
- Návrh **404** stránky.
- **Focus-visible** stavy + **loading** stav tlačítka jako hotové CSS do `index.html`.
- Doplnění **souhlasu** do formuláře.
