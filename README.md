# Schemasystem — Mise en Place

Schemaläggningssystem för svenska restauranger byggt enligt Visita / Gröna Riksavtalet 2025–2027. Just nu en single-file HTML-prototyp (vanilla JS, ingen backend, lagrar i `localStorage`).

## Restauranger som finns inbyggda

- **Speakers Corner** (org 556615-5098)
- **Tycho Brahe** (org 556407-5389)
- **Fellini** (org 556267-8820, sommarstängt 1 jul – 1 sep)

## Hur du kör den

Öppna `Schemasystem_Speakers_Corner.html` i en webbläsare (Chrome/Edge/Firefox). Det är allt — appen kör helt klient-side. Data sparas i webbläsarens `localStorage` under nyckeln `schemasystem_v1`.

## Flödet

1. **Personal** — anställda, anställningsform (HEL/DEL/TIM/EXT), lön, frånvaro
2. **Veckomall** — A/B-rotation (udda/jämna veckor)
3. **Bemanningsbehov** — hur många i servis/kök, per dag, per block (heldag/dag/kväll). Period 4/8/16 veckor.
4. **Schema** — AI genererar pass utifrån mall + behov, respekterar 11h vila och 13h-tak. Vy: vecka eller månad. Regelstatus + öppna pass + lönekostnad i samma vy.
5. **Exportera** — Excel (Caspeco-format), CSV, eller PDF-utskrift

## AI-algoritm i korthet

```
Lager 1: HEL → fyll till 100% av kontrakt
Lager 2: DEL → fyll till 50% av kontrakt
Lager 3: Resten → markeras som ÖPPET PASS (manuell tilldelning)
```

Hårda regler: avdelningsmatch, ingen dubbelbokning, 11h vila, max 13h per pass utan dispens.

Inte implementerat (planerat): peak-prioritering, OB-balansering, rättviseregler.

## Lönelogik

- **Påläggsfaktor:** ≈ 1,4342 (arbetsgivaravgift 31,42 % + semesterersättning 12 %)
- **OB-tillägg:** 27,59 kr/h vanligt, +24,31 kr/h extra natt 01–06 (totalt 51,90 kr/h natt)
- **Storhelg:** +100 % av timlönen utöver OB
- Källor: hrf.net/din-lon/ob-tillagg/, allabolag.se

## Status

Prototyp under utveckling. Mål: gå från manuella scheman till AI-stött system.

## Roadmap (utkast)

- [ ] Versionshantering via Git/GitHub
- [ ] Polish + buggfixar i nuvarande prototyp
- [ ] Riktig SMHI-väderintegration (idag demo-data)
- [ ] Peak-prioritering i AI-algoritmen
- [ ] OB-balansering mellan personal
- [ ] Ev. backend (databas, multi-user, auth)
