---
layout: web_publishing
subtitle: Zadanie 3
currentSite: wp
wpSite: assgnmt3
---

# XML prezentácia

## Znenie zadania:
Analyzujte možnosti zápisu jednoduchej prezentácie v jazyku XML. Identifikujte základné súčasti prezentácie a navrhnite XML elementy pre ich označkovanie (metadátové, štrukturálne, inline). Dbajte na znovupoužiteľnosť a vyvarujte sa redundancií. Návrh elementov zrealizujte opísaním typu dokumentu pomocou vybraného jazyka (DTD, XSD, RELAX NG) spolu s vysvetlením účelu jednotlivých elementov. Vo vami navhrnutom jazyku vytvorte ukážkovú prezentáciu, ktorá bude demonštrovať možnosti tvorby prezentácií podľa definície typu dokumentu.

Navrhnite a vytvorte XSLT šablóny pre konverziu prezentácie z XML do XHTML+CSS a pre konverziu prezentácie z XML do PDF. Klaďte dôraz na znovupoužitie jednotlivých šablon pre viaceré výstupné formáty. Umožnite zadávanie parametrov transformácií.

## Riešenie:
Za pomoci XML som vytvoril jednoduchú ukážkovú prezentáciu, ktorá prezentuje rôzne typy slajdov. Súčasťou riešenia je aj XSL súbor popisujúci transformáciu vytvorenej XML prezentácie do jednotlivých súborov vo formáte XHTML. Na dodatočné formátovanie bolo použité CSS a vytvorená XML prezentácia je validná podľa vytvorenej schémy v RELAX NG.

### Typy slajdov:
* automaticky generovaná titulná strana z meta informácií XML prezentácie
* automaticky generovaný obsah prezentácie
* slajd s textovými odsekmi
* slajd s nečíslovaným zoznamom
* slajd s číslovaným zoznamom
* kombinácia zoznamov a odeskov textu
* slajd s obrázkom a jeho popisom

### Popis štruktúry XML prezentácie:
* základom je koreňový element `presentation`
* dôležitý a povinný element `info` obsahujúci meta informácie o prezentácii ako: názov prezentácie, podnadpis, autor, email, rok a organizáciu (elementy podnadpis, email a organizácie nie sú povinné)
* nasleduje element `slides`, ktorý musí obsahovať aspoň jeden element `slide`, ktorý predstavuje samotný slajd prezentácie
* každý slajd potom musí obsahovať element `title` nadpis slajdu a element `content` reprezentujúci obsah prezentácie
* element `content` môže obsahovať nasledujúce atribúty rozlišujúce typ zobrazeného obsahu: `text`, `list`, `image`
* jednotlivé odseky pri type obsahu `text` a `list` sú potom uzavreté v elemente `para`
* pre zoznamy je použitý element `list`, ktorý môže byť klasický (iba odrážky) alebo číslovaný, tieto možnosti sa nastavujú atribútom `type` elementu `list`, ktorý môže byť buď `unordered` alebo `ordered`. Jednotlivé položky zoznamu sú definované elementami `item`
* pri type obsahu `image` je súčasťou slajdu popis obrázku v elemente `caption` a samotný obrázok určený elementom `image`, ktorý má atribút `src` na špecifikovanie zdroja obrázku
* ak si používateľ praje, aby súčasťou prezentácie bol aj obsah prezentácie, stačí ak do elementu `content` uvedenie prázdny element `toc`, ten bude pri následnej transformácii autmaticky vygenerovaný
* prezentácia v XML sa nachádza v súbore **presentation.xml** a ako bolo spomínané je validná podľa vytvorenej schémy v RELAX NG, ktorá je definovaná v súbore **relax_schema.rng**
* na validáciu bol použitý **JING** validátor

### XSL transformácia:
* XSLT pre vytvorenú XML prezentáciu sa nachádza v súbore **presentation.xsl**
* pri jej tvorbe som sa snažil o "modulárny" prístup v tom zmysle, že v rámci XSL je vytvorených viacero šablón (template), ktoré sú aplikované podľa potreby a výskytu jednotlivých elementov v XML
* automaticky generované sú čísla strán slajdov, obsah a titulná strana prezentácie
* na transformáciu do XHTML bol využitý **SAXON** vezie 8 a vyššie
* po transformácii nám vzniknú samostatné XHTML súbory jednotlivých slajdov
* pri transformácii pomocou **SAXON** je možné uviesť parametre transformácie `color`, `font`, `paging`, ktorými má používateľ možnosť zmeniť základné nastavenia farby pozadia titulnej strany a nadpisov, zmeniť použitý font pre celú prezentáciu a vypnúť číslovanie strán, ktoré je defaultne zapnuté. Ak ich používateľ nezadá použíjú sa základné nastavenia.

### Ukážky slajdov:
* [**Titulná strana**][titlepage]{:target="_blank"}


[titlepage]: /assets/files/titlepage.xhtml
