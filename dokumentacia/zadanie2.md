---
layout: documentation
title: Dokumentácia Zadania 2
---

## Transformácia vybraného dokumentu do formátu DocBook ##

Predmetom 2. zadania je spracovanie vybraného dokumentu (ideálne bakalárskeho projektu) z pôvodného ľubovoľného (Word, OpenOffice, LaTeX, …) formátu do formátu DocBook a vygenerovanie cieľového tvaru v PDF. Výsledný dokument bude mať rozsah minimálne 10 a maximálne 15 strán. Do rozsahu sa nezapočítavajú úvodné strany (obsah, zoznamy obrázkov a tabuliek), použitá literatúra a prílohy.

Požadované a kontrolné konštrukcie sú:
  * štandardné členenie textu na kapitola, podkapitola, podpodkapitola, príloha, generovaný obsah,
  *  zvýraznenie slov, zvýraznenie členenia textu odrážkami alebo číslovaním,
  *  odkazy na iné časti vlastného dokumentu, prípadne odkazy na URL,
  *  poznámka pod čiarou,
  *  zoznam použitej literatúry a zdrojov vrátane ich citácie v texte,
  *  vloženie obrázku a tabuliek, odkazy na ne v texte; zoznam obrázkov a tabuliek v úvode alebo závere textu,
  *  vytvorenie registra pojmov (indexu) s pojmami hierarchicky usporiadanými do dvoch úrovni, napríklad „cykly, while“, „cykly, for“ (najmenej ako ukážku na 10-15 pojmoch na predvedenie práce s registrom).


## Riešenie ##

### Štruktúra dokumentu ###

* Analýza
  * Čo je to jazyk
  * ...
  * Čo je to neurónová sieť
    * neurón
    * ...
  * ...
  * Slovenčina vs. Angličtina
    * abeceda
    * ...
* Návrh riešenia
* Zaver
  * Zoznam obrazkov
* dodatok
* Slovnik
* Bibliografia

Pri riešení sme upravovali zadanú šablónu. Členenie dokumentu je uvedené hore. Pri riešení sme použili nasledovné:
  - zvýraznenie slov
  - členenie textu  odrážkami a číslovaním
  - generované odkazy na iné časti dokumentu a odkazy na obrázky v texte
  - poznámka pod čiarou
  - zoznam zdrojov (bibliografia)
  - generované citácie v texte
  - obrázky
  - tabuľka
  - slovník pojmov

Použité elementy:
  - chapter
  - section
  - para
  - title
  - appendix
  - footnote + footnoteref
  - glossary + glossdiv + glossentry + glossdef + glossterm
  - emphasis
  - orderedlist + listitem
  - itemizedlist
  - xref
  - figure + mediaobject + imageobject + imagedata
  - bibliography + bibliomixed + bibliomisc + abbrev
  - informtable + tgroup + tbody + row + entry

Použité atribúty:
  - id
    * `<figure id="fig10">`
  - role
    * `<emphasis role="bold">`
  - linkend
    * `<xref linkend="cit5"/>`
    * `<footnoteref linkend="poznamka1"/>`
  - fileref
    * `<imagedata fileref="img/figure09.jpg"/>`
  - align
    * `<imagedata align="center" fileref="img/figure01.jpg"/>`
  - cols
    * `<tgroup align="center" cols="3">`

Obsah sa generoval automaticky. Ďalej sme upravili súbor thesis-tp-fo.xsl aby sme odstránili obrázok z titulnej strany. Súbor thesis.xsl sme neupravili.
