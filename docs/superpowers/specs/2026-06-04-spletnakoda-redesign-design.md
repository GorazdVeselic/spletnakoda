# spletnakoda.si — prenova (design spec)

**Datum:** 2026-06-04
**Avtor:** Gorazd Veselič (z asistenco Claude Code)

## Cilj

Osvežiti obstoječo statično vizitko spletnakoda.si v moderno, temno enostransko
(one-pager) predstavitveno stran z malo več vsebine. Ostane statičen HTML brez
build orodij — enostaven deploy (upload datotek).

## Smer

Hibrid, nagnjen k vizitki: minimalizem ostane, doda se nekaj sekcij in sodoben
videz. Temna tema (potrjeno).

## Struktura strani (sekcije)

1. **Sticky navigacija** — wordmark logo + sidra (Storitve, Tehnologije, O meni, Kontakt).
   Polprosojna z blur ozadjem. Skrita na mobilnih.
2. **Hero** — CSS wordmark `<?php Spletna ]{oda ?>` z gradientom, podnaslov
   "Innovative Web Solutions", kratek opis, dva gumba (Stopi v stik / Kaj ponujam),
   nežno animirano gradientno ozadje (blob krogi).
3. **Storitve** — 3 kartice: API & integracije / Cloud & DevOps / Razvoj & hosting.
4. **Tehnološki sklad** — vrstica oznak (chips): PHP, Laravel, MySQL, Redis, REST API,
   Docker, Kubernetes, AWS, Terraform, CI/CD, Linux, Vue/Next.js.
5. **O meni** — "20+ let" poudarek + kratek opis iz CV-ja (Senior Full-Stack / DevOps).
6. **Kontakt** — samo email (gorazd@spletnakoda.si). **Brez** lokacije in telefona.
7. **Footer** — copyright.

## Oblikovanje

- Temna paleta (#0a0e16 ozadje, modri/vijolični gradient brand barve).
- System font sklad (brez zunanjih font datotek → hitro).
- Subtilne animacije: lebdeči gradientni blobi, hover dvig kartic/gumbov.
- Polno odzivno (cards → 1 stolpec, nav skrit na <720px).

## Tehnične odločitve

- **Statičen HTML/CSS, brez JS odvisnosti.** Brez build orodij — deploy = upload datotek.
- **Dvojezičnost (SL/EN) prek dveh datotek + `hreflang`:** `index.html` (SL, koren) in
  `en/index.html` (EN). Vsaka ima svoj `canonical` ter `hreflang` povezave (`sl`, `en`,
  `x-default`) → oba jezika polno indeksirana. Preklopnik SL|EN so navadne povezave (brez JS).
  IDje sider se ujemajo z jezikom (SL: `#storitve`…, EN: `#services`…).
- **Skupni `style.css`** za obe strani (DRY). Polna višina zadnje sekcije prek razreda `.fill`
  (ne prek lokaliziranega IDja), višina menija prek CSS spremenljivke `--nav-h`.
- **Logo:** CSS wordmark v vsebini; originalni `spletnaKoda.png` ostane favicon + `og:image`.
  Wordmark se ne lomi (en line ali čisto 3 vrstice na ozkih zaslonih).
- **Anchor scroll fix:** `scroll-margin-top` na sekcijah, da sticky nav ne prekrije cilja;
  enoten offset → naslovi pristanejo na isti višini.
- **Mobilno (<720px):** meni skrit (ni klikabilnih sider), zato simetričen razmik in brez
  `.fill` praznega repa.
- **Analytics:** stari Universal Analytics (UA-…) je ukinjen (sunset 2023) — izpustimo;
  po želji se kasneje doda GA4.
- **Viri:** absolutne poti (`/style.css`, `/spletnaKoda.png`, `/favicon.ico`) → predpostavlja
  deploy v koren domene. Pozor na velike/male črke imen na Linux gostovanju.

## Izven obsega (YAGNI)

- Večstranska navigacija, blog, CMS, kontaktni obrazec z backendom.

## Datoteke

```
index.html            (SL)
en/index.html         (EN)
style.css             (skupni stil)
spletnaKoda.png
favicon.ico
robots.txt
```
