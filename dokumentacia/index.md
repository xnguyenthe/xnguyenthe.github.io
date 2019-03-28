---
layout: documentation
title: Dokumentácia Zadanie 1
zadanie_html: zadanie1_znenie.html
---
## Znenie Zadania 1 ##

Vytvorte webovú prezentáciu (webové sídlo) o sebe. Zamerajte sa jednak na vaše profesné záujmy
(napr. projekty, ktoré riešite/riešili ste, čo vás v informatike najviac baví, fascinuje = váš developerský profil) a jednak vaše osobné záujmy, hobby.

V rámci developerského profilu vytvorte sekciu Webové publikovanie, kde budete publikovať
všetky tri vaše vypracované zadania z predmetu.

Využite pritom technológie Git + GitHub Pages + Jekyll + Markdown. Využite potenciál statického generátora Jekyll a jeho templatovacích možností.

Podrobné požiadavky na vypracovanie a odovzdanie zadania (priemerná úroveň kvality):
  - Sídlo musí obsahovať aspoň 5 podstránok, pri využití aspoň 3 rôznych rozložení (layout-ov)
  - V rámci šablon musí byť použité:
      - aspoň 5 premenných
      - kolekcie alebo dátové súbory
      - aspoň 5 filtrov alebo tagov
      - aspoň 1 plugin (okrem pagination)


## Riešenie ##
Táto stránka je dokumentácia k zadaniu.


###  Použité premenné ###

* page.url
* site.email
* page.title
* prednastavené premenné v súbore config.yml:
  * Name
  * author
  * defaults - urcenie front matter pre staticke subory

### Jekyll štruktúra stránky ###

Naše sídlo má 6 podstránok - Home, About, CV, Hobbies, Blog.

Blog je podstránka, ktorá obsahuje zoznam všetkých blogových priíspevkov.

### Použité rozloženia ###

Naša stránka má 4 rozloženia:
* dafault_wrapper - Obalujuce rozlozenie
* about - rozlozenie pre stranku O mne.
* documentation - rozlozenie pre dokumentaciu
* post - prispevky

### Použité tagy a filtre ###
* date_to_string
* sort
* for
* include
* assign
* if

### Použité pluginy ###
jekyll-YouTube
jekyll-email-protect

### Použité dátové súbory ###
Dátové súbory sme písali vo formáte yaml.

* books.yml
* language_skills.yml
* piano_pieces.yaml
* program_skills.yml
