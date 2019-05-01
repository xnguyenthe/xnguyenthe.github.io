---
layout: documentation
title: Dokumentácia Zadania 3
---

## XML prezentácia ##

Analyzujte možnosti zápisu jednoduchej prezentácie v jazyku XML. Identifikujte základné súčasti prezentácie a navrhnite XML elementy pre ich označkovanie (metadátové, štrukturálne, inline). Dbajte na znovupoužiteľnosť a vyvarujte sa redundancií. Návrh elementov zrealizujte opísaním typu dokumentu pomocou vybraného jazyka (DTD, XSD, RELAX NG) spolu s vysvetlením účelu jednotlivých elementov. Vo vami navhrnutom jazyku vytvorte ukážkovú prezentáciu, ktorá bude demonštrovať možnosti tvorby prezentácií podľa definície typu dokumentu.

Navrhnite a vytvorte XSLT šablóny pre konverziu prezentácie z XML do XHTML+CSS a pre konverziu prezentácie z XML do PDF. Klaďte dôraz na znovupoužitie jednotlivých šablon pre viaceré výstupné formáty. Umožnite zadávanie parametrov transformácií.

Súčasťou požiadaviek na zadanie je vytvorenie správy o zadaní 3, v ktorej zdokumentujete splenie jednotlivých bodov zadania. Správa bude súčasťou vašej stránky o Webovom publikovaní na GitHube.

Hodnotenie (max 14 bodov):
* opis typu dokumentu + opis účelu navrhnutých elementov - možnosť výberu (práve jedného) z variantov:
  - DTD (max 3 body)
  - XML Schema (max 4 body)
  - RELAX NG (max 4+1 bodov)
* vytvorenie ukážkovej XML prezentácie demonštrujúcej možnosti definície typu dokumentu (max 2 body)
* základný návrh XSL transformácií, ich vhodnosť, parametrizácia (max 3 body)
* vytvorenie XSLT pre konverziu prezentácie z XML -> XHTML+CSS (max 3 body)
  - každý slide bude v samostatnom XHTML súbore
* vytvorenie XSLT pre konverziu prezentácie XML -> PDF (max 2 body)


## Riešenie ##

### Vypracované dokumenty ###
* _prezentacia.xml_ - XML súbor s ukážkovou prezentáciou
* _prezentacia_xslt.xsl_ - definovanie transformácií z XML do xhtml
* _parametrexhtml.xml_ - definovanie parametrov
* _styles.css_ - definovanie CSS štýlov pre html dokumenty
- medzi dokumentami sú aj obrázky, ktoré boli použité v prezentácii

### DTD definícia dokumentu ###
```
<!DOCTYPE presentation [
<!ELEMENT presentation (slide*)>
<!ELEMENT slide (layout_title | layout_content1 | layout_content2)>
<!ELEMENT layout_title (title, subtitle?, author?)>
<!ELEMENT title (#PCDATA)>
<!ELEMENT subtitle (#PCDATA)>
<!ELEMENT author (#PCDATA)>
<!ELEMENT layout_content1 (title, (figure | text_field) )>
<!ELEMENT figure (description?, image_data)>
<!ELEMENT description (#PCDATA)>
<!ELEMENT image_data EMPTY>
<!ATTLIST image_data fileref CDATA #REQUIRED>
<!ELEMENT text_field (#PCDATA | list | emphasis | link)* >
<!ELEMENT list (list | listitem)+ >                     
<!ATTLIST list type (bullet | ordered) "bullet">
<!ELEMENT listitem (#PCDATA | emphasis | link)* >
<!ELEMENT emphasis (#PCDATA)>
<!ATTLIST emphasis type (italic | bold | underline) "italic">
<!ELEMENT link (#PCDATA)>
<!ATTLIST link src CDATA #IMPLIED>
<!ELEMENT layout_content2 (title, text_field, figure )>
]>
```

#### Účel navrhnutých elementov ####
* presentation
  - root element definujúci prezentáciu
* slide
  - element definujúci slajdy, teda priesvitky prezentácie
  - slajdy môžu mať 3 rozloženia
* layout_title
  - definuje rozloženie pre titulné slajdy
* layout_content1
  - definuje slajdy pre obsah, ktorý bude mať rozloženie s 1 stĺpcom s nadpisom
  - stĺpec môže obsahovať _text_field_ (textový obsah) alebo _figure_ (obrázok)
* layout_content2
  - definuje slajdy pre obsah, ktorý bude mať rozloženie s 2 stĺpcami s nadpisom
  - stĺpec naľavo je vždy _text_field_ a stĺpec napravo vždy _figure_
* title
  - nadpis - či už na titulnom slajde alebo na obsahovom
* subtitle
  - podnadpis na titulnom slajde
* author
  - autor - iba na titulnom slajde
* figure
  - definuje element, ktorý obsahuje obrázok a popis k obrázku
* description
  - definuje popisok k obrázku
* image_data
  - tag obsahujúci atribút _fileref_ s referenciou na zdroj obrázku. tento element je prázdny
* text_field
  - definuje element, ktorý obsahuje text
* list
  - zoznam - môže byť typu bez poradia (atribút type="bullet") alebo typu poradový (atribút type="ordered")
  - umožňuje vnáranie zoznamov
* listitem
  - definuje podčasti zoznamu
  - môže obsahovať text, zvýraznený text a linky
* emphasis
  - zvýraznený text
  - typy zvýraznených textov sú italic, bold a underline
* link
  - uzaviera text, ktorý má byť linkom (odkazom)
  - atribút _src_ odkazuje na zdroj linku

### Základný návrh XSL transformácií ###

#### parametre ####

```
<xsl:param name="slide.width" select="1200"/>
<xsl:param name="slide.height" select="500"/>
```

#### transformácie ####

```
<xsl:template match="//slide">
<xsl:template match="//layout_title">
<xsl:template match="//layout_content1">
<xsl:template match="//layout_content2">
<xsl:template match="//text_field">
<xsl:template match="//figure">
<xsl:template match="//list">
<xsl:template match="//emphasis[@type]">
<xsl:template match="//link">
```

### XML -> XHTML ###
Použitie druhej verzie XSL
`<xsl:transform version="2.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">`

Referencia na súbor s paramatrami

```
<!--import parametrov-->
<xsl:include href="parametrexhtml.xml"/>
```

Predpis pre transformáciu jednotlivých slajdov a ich generovanie do oddelených súborov HTML.
Použitie parametrov definovaných v oddelenom súbore.
```
<!-- template for generating each slide onto a separate page -->
<xsl:template match="//slide">
    <xsl:result-document href="xhtml/s_{count(preceding-sibling::slide)}.html" method="xhtml">

      <html xmlns="http://www.w3.org/1999/xhtml">
        <head>
          <meta charset="utf-8"/>
          <link rel="stylesheet" href="styles.css" type="text/css"/>
        </head>
        <body class="presentation">
          <section class="container" align="center" style="width:{$slide.width}px; height:{$slide.height}px;">
            <xsl:apply-templates/>

            <section class="navigation" style="position: absolute; top: {$slide.height - 10}px; left: 10px;">
              <xsl:call-template name="navigation"/>
            </section>
          </section>
        </body>

      </html>
    </xsl:result-document>
</xsl:template>
```

Vytvorenie navigácie pre prepojenie jednotlivých html súborov. Tento template je volaný vyššie.
```
<!--template for creation of Navigation-->
<xsl:template name="navigation">
      <xsl:if test="count(preceding-sibling::slide) &gt; 0">
        <a href="s_{count(preceding-sibling::slide) - 1}.html">Back</a>
      </xsl:if>

      - <xsl:value-of select="count(preceding-sibling::slide)"/> -

      <xsl:if test="count(following-sibling::slide) &gt; 0">
        <a href="s_{count(preceding-sibling::slide) + 1}.html">Next</a>
      </xsl:if>
</xsl:template>
```

Transformácia pre titulný slajd:
```
<!-- title_slide -->
<xsl:template match="//layout_title">
  <!--ak parent (slide) je prvy slide, dajme mu section attribute title_slide-->
  <section class="title_slide">
    <!--xsl:if test="ancestor::node() = //slide[1]" >
      <xsl:attribute name="class">
        first_title_slide
      </xsl:attribute>
    </xsl:if-->

      <section class="title-slide-title">
        <h2> <xsl:value-of select="./title"/> </h2>
      </section>
      <section class="title-slide-subtitle">
        <h4> <xsl:value-of select="./subtitle"/> </h4>
      </section>
      <section class="title-slide-author">
        <author> <xsl:value-of select="./author"/> </author>
      </section>

  </section>
</xsl:template>
```

Transformácia pre zoznam. Umožňuje vnáranie.
```
<!--template for list - allows nesting -->
<xsl:template match="//list">
  <xsl:choose>
    <xsl:when test="self::list/@type = 'ordered' ">
      <ol>
        <xsl:for-each select="listitem">
          <li> <xsl:apply-templates /> </li>
        </xsl:for-each>
      </ol>
    </xsl:when>
    <xsl:otherwise>
      <ul>
        <xsl:for-each select="listitem">
          <li> <xsl:apply-templates /> </li>
        </xsl:for-each>
      </ul>
    </xsl:otherwise>
  </xsl:choose>
</xsl:template>
```

Transformácia pre zvýraznený text. Tiež umožňuje vnáranie, teda použitie viacerých typov zvýraznení naraz.
```
<!-- template for emphasis - allows nested emphasises as well -->
    <!--without attribute => default value is type="italic" -->
  <xsl:template match="//emphasis[@type]">
    <xsl:choose>
      <xsl:when test=" @type = 'bold' ">
        <b><xsl:apply-templates /></b>
      </xsl:when>
      <xsl:when test=" @type = 'underline' ">
        <u><xsl:apply-templates /></u>
      </xsl:when>
      <xsl:otherwise> <!-- italic -->
        <i><xsl:apply-templates /></i>
      </xsl:otherwise>
    </xsl:choose>
  </xsl:template>
  ```

Transformácie sa robili pomocou programu _Saxon_. Použili sme verziu 9. Príkaz pre transformáciu vyzeral nasledovne:
`java -jar C:\DocBook\saxon\saxon9he.jar prezentacia.xml prezentacia_xslt.xsl`
