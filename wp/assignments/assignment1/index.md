---
layout: web_publishing
subtitle: Zadanie 1
currentSite: wp
wpSite: assgnmt1
---

# Osobná webová prezentácia na GitHub pages

## Znenie zadania:
Vytvorte webovú prezentáciu (webové sídlo) o sebe. Zamerajte sa jednak na vaše profesné záujmy (napr. projekty, ktoré riešite/riešili ste, čo vás v informatike najviac baví, fascinuje = váš developerský profil) a jednak vaše osobné záujmy, hobby.

V rámci developerského profilu vytvorte sekciu Webové publikovanie, kde budete publikovať všetky tri vaše vypracované zadania z predmetu.

Využite pritom technológie Git + GitHub Pages + Jekyll + Markdown. Využite potenciál statického generátora Jekyll a jeho templatovacích možností.

## Požiadavky:
* Sídlo musí obsahovať aspoň 5 podstránok, pri využití aspoň 3 rôznych rozložení (layout-ov)

* V rámci šablon musí byť použité:
  * aspoň 5 premenných
  * kolekcie alebo dátové súbory
  * aspoň 5 filtrov alebo tagov
  * aspoň 1 plugin (okrem pagination)

***
## Riešenie:

Riešením tohto zadania je práve táto webová stránka.
### Obsahuje tieto podstránky:
* Home
* O mne
  * CV
  * Projekty
* Webové publikovanie
  * Zadania 1 - 3
* Galéria
* Blog
  * Jednotlivé príspevky

### Layout-y:
* základný layout **default.html**
  * je využívaný na všetkých podstránkach a ostatné layout-y od neho dedia
  * v úvode sa include-je hlavička **header.html** obsahujúca základné meta informácie a tiež CSS, JS potrebný pre Bootstrap a použitý plugin
  * nasleduje navigačný panel stránky, v ktorom sa include-jú jednotlivé tab-y v `if/else` podľa toho na ktorej stránke sa aktuálne nachádzame, kvôli prepínaniu **active** stavu jednotlivých tab-ov (nefungovala funkcionalita Bootstrap-u)
  * následne je využitá premenná `content` pre zahrnutie obsahu stránky použivajúcej tento layout
  * ďalej je zahrnutý informačný panel informujúci o dátume posledného build-u stránky a počte slov na stránke
  * include päty **footer.html**
  * na záver je pridaný JS pre použitý plugin, ktorý sa však použije iba na stránke obsahujúcej tento plugin
* layout pre galériu **gallery_layout.html**
  * v úvode je rozdelený na polovicu, v ľavej časti sa nachádza základný popis o galérii, motivácii fotiť a použitej technike
  * v pravej časti sa potom nachádza Google mapa zobrazujúca oblasti kde  boli odfotené fotografie v galérii
    * používateľ môže pridať ďalšie body na mape jednoduchým pridaním záznamu do súboru **locations.yml** nachádzajúceho sa v priečinku **_data/gallery_points**
  * nasledujú samotné fotografie s popisom v pravej časti
    * galérie sú pridávané pomocou `for` cyklu, prechádzaním súboru **galleries.yml** obsahujúceho informácie o galérii ako: názov, popis a názov súboru obsahujúceho samotné fotografie s použitím plugin-u
      * tento súbor (v mojom prípade **nature.md** a **cars.md**) sa musí nachádzať v priečinku **_includes** a potom sa pomocou príkazu `include` pridá na stránku
* layout **personal.html**
  * je určený pre podstránky **O mne**, **CV** a **Projekty**
  * v ľavej časti sa nachádza navigačný panel pre prepínanie medzi sekciami, prepínanie **active** stavu jednotlivých tab-ov riešené podobne ako v **default.html** layout-e
  * pravá časť obsahuje obsah stránky, v prípade, že sa nachádzame na stránke **O mne** sa pridá aj profilová fotografia
* layout **post.html**
  * je určený pre blogové príspevky
  * obsah príspevku je organizovaný v jumbotron-e
* layout **web_publishing**
  * tento layout je určený pre potreby tohto predmetu
  * základnou myšlienkou je prehľadné prezeranie zadaní, ktoré sú organizované v tab-och obdobne ako v internetových prehliadačoch
  * taktiež písanie jednotlivých zadaní v **Markdown-e**

### Premenné:
* interné premenné Jekyll-u: `content`, `site.data`, `site.time`, `page.content`, `page.layout`, `page.permalink`, `page.date`
* vlastné premenné:
  * definované v **_config.yml**: `site_name`, `owner`, `nick`, `email`, `profile_photo_path`, `navbar`, `maps`
  * v rámci Front Matter:
    * `currentSite` - dôležitá premenná pre prepínanie **active** stavu príslušných prvkov spomínaných vyššie, obsahuje ju každá stránka
    * `subtitle` - podnázov stránky použitý v samotnej stránke, ale aj ako názov v tab-e prehliadača
    * `wpSite` - obdobne ako `currentSite`, ale určená pre sekciu Webového publikovania
  * premenné použité v rámci príkazu `include` na "inject-ovanie" definovaných premenných v **navbar_active.html**, **pills_active.html**, **tabs_active.html**
  * premenná **music** použitá s príkazom `assign` pre priradenie zotriedeného zoznamu pesničiek v blogu

### Dátové súbory:
* použité súbory v **YAML** formáte
  * **locations.yml** - obsahujú svetové koordináty miest pre plugin
  * **galleries.yml** - definované galérie (spomínané vyššie)
  * **music_sk.yml** - zoznam obľúbených slovenských pesničiek, použité v blogu

### Filtre a tagy
* filtre: `append`, `date_to_long_string`, `number_of_words`, `date_to_string`, `sort`
* tagy: `if/else/elsif/endif`, `for/endfor`, `slider/endslider`, `include`, `google_map`, `assign`

### Plugin-y:
* plugin [**Jekyll Ideal Image Slider**][ideal]{:target="_blank"} použitý na tvorbu jednoduchej galérie
* plugin [**Jekyll Maps**][maps]{:target="_blank"} pre pridanie Google Maps na stránku
* plugin [**Jekyll Youtube**][youtube]{:target="_blank"} pre embedovanie Youtube videí


[ideal]: https://github.com/jekylltools/jekyll-ideal-image-slider
[maps]: https://github.com/ayastreb/jekyll-maps
[youtube]: https://github.com/dommmel/jekyll-youtube
