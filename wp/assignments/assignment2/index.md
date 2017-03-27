---
layout: web_publishing
subtitle: Zadanie 2
currentSite: wp
wpSite: assgnmt2
---

# Transformácia vybraného dokumentu do formátu DocBook

## Znenie zadania:
Predmetom 2. zadania je spracovanie vybraného dokumentu (ideálne bakalárskeho projektu) z pôvodného ľubovoľného (Word, OpenOffice, LaTeX, …) formátu do formátu DocBook a vygenerovanie cieľového tvaru v PDF. Výsledný dokument bude mať rozsah minimálne 10 a maximálne 15 strán. Do rozsahu sa nezapočítavajú úvodné strany (obsah, zoznamy obrázkov a tabuliek), použitá literatúra a prílohy.

## Požiadavky:
Požadované a kontrolné konštrukcie sú:
* štandardné členenie textu na kapitola, podkapitola, podpodkapitola, príloha, generovaný obsah,
* zvýraznenie slov, zvýraznenie členenia textu odrážkami alebo číslovaním,
* odkazy na iné časti vlastného dokumentu, prípadne odkazy na URL,
* poznámka pod čiarou,
* zoznam použitej literatúry a zdrojov vrátane ich citácie v texte,
* vloženie obrázku a tabuliek, odkazy na ne v texte; zoznam obrázkov a tabuliek v úvode alebo závere textu,
* vytvorenie registra pojmov (indexu) s pojmami hierarchicky usporiadanými do dvoch úrovni, napríklad „cykly, while“, „cykly, for“ (najmenej ako ukážku na 10-15 pojmoch na predvedenie práce s registrom).

## Riešenie:
Pre toto zadanie som sa rozhodol spracovať vybrané časti bakalárskeho projektu (BP1), tak aby riešenie spĺňalo obsahové aj ostatné kontrolované požiadavky.

### Vykonané zmeny:
* úprava titulnej strany - odstránenie pôvodného obrázku, zmena rozloženia a odsadenia nadpisov, zmena veľkosti písma, vykonané v súbore **thesis-tp-fo.xsl**
* názvy kapitol - zmeny v XSL súbore **thesis.xsl**, vďaka ktorým sa negeneruje názov kapitoly ako **Kapitola č.**, ale použije sa priamo názov a číslo kapitoly
* pridané zoznamy tabuliek a obrázkov - taktiež zmena v **thesis.xsl**, kde bolo potrebné pridať kľúčové slová `table` a `figure` v časti označenej menom **generate.toc**
* zmena anotácie

### Použité príkazy:
* členenie textu na kapitoly a podkapitoly pomocou `chapter` a `section`, subsection je jednoduché vnorenie príkazu v rámci section
* zvýraznenie slov pomocou `emphasis` v použitej literatúre a spolu s voliteľným parametrom `bold` aj v zozname v texte
* členenie odrážkami pomocou `itemizedlist` spolu s `listitem`
* odkazy v texte na literatúru (citácie), obrázky, tabuľku a iné kapitoly pomocou `xref`
* odkazy na URL pomocou `ulink`
* poznámka pod čiarou pomocou `footnote`
* generovanie zoznamu literatúry vďaka príkazu `bibliography`, v rámci použitej literatúry boli jednotlivé položky pridané pomocou `biblioentry` alebo `bibliomixed`
* vloženie obrázkov pomocou `figure` a vnorených príkazov `mediaobject` a `imageobject`
* vytvorenie tabuľky `table`
* register pojmov automaticky generovaný pomocou príkazu `index` spolu s použitím príkazov na označenie kľúčových slov `indexterm`, `primary`, `secondary`, `tertiary`
