---
layout: "default"
title: "Soveltamisohjeet"
description: ""
page: "soveltamisohjeet"
modelversion: "1.0-dev"
status: "Keskeneräinen"
---
# Soveltamisprofiili

{:.no_toc}

1. 
{:toc}

## Johdanto

Tämän dokumentin vaatimukset ja suositukset muodostavat maankäyttörajoitusten loogisen tietomallin soveltamisprofiilin maankäyttörajoitus-aineistoille. Soveltamisprofiili kuvaa ne maankäyttörajoitukset ja lisävaatimukset, joita tulee noudattaa maankäyttörajoitusten tietomallin UML-kielisen kuvauksen ja sen sanallisen dokumentaation soveltamisessa maankäyttörajoitusten tietoaineistojen kuvaamiseen.

## Koodistot


### Käsittelytapahtuman laji

<!--Lisää sisäiset linkit vielä -->
{% include clause_start.html type="req" id="prof-tjs/vaat-maankayttorajoituskasittelytapahtuma" %}
Luokan AbstraktiKasittelytapahtumanLaji sijaan tulee käyttää tarkentavaa luokkaa MaankayttorajoitustenKasittelytapahtumanLaji.
{% include clause_end.html %}

## Maankäyttörajoituksen lajien arvot

Seuraavat **Maankäyttörajoituksen laji**-koodiston arvojen soveltamisohjeet huomioidaan vain ```voimaantuloTapa```-attribuutin arvon ollessa ```Päätöksellä annettu maankäyttörajoitus```. ```Automaattinen maankäyttörajoitus``` ja ```Voimassa olevan maankäyttöpäätöksen rajoitus``` tapauksissa maankäyttörajoituksen lajin ```arvo```-attribuutin arvo generoidaan automaattisesti kaavatietomallista tietojärjestelmässä ennalta määriteltyjen sääntöjen mukaisesti. Maankäyttörajoituksen ```voimaantuloTapa``` -attribuutin kanssa mahdolliset esiintyvät ```rajoituksenLaji```-attribuutin arvot on esitelty luvussa [Elinkaarisäännöt-sivulla](https://ym-rakennettu-ymparisto.github.io/maankayttorajoitusten-tietomalli/1.0-dev/looginenmalli/elinkaarisaannot.html#sallitut-maankäyttörajoituksen-voimaantulotavat-maankäyttörajoituksen-lajeille). 


### Asemakaavan rakennuskielto

**Koodi:** http://uri.suomi.fi/codelist/rytj/RY_MaankayttorajoituksenLaji/code/01

<!--Lisää sisäiset linkit vielä -->
{% include clause_start.html type="req" id="prof-mkp/vaat-asemakaavan-rakennuskielto" %}
Ilmaisee, että kyseinen maankäyttörajoitus koskee asemakaavan rakennuskieltoa.
{% include clause_end.html %}

<!--Lisää sisäiset linkit vielä -->
{% include clause_start.html type="req" id="prof--mkp/vaat-asemakaavan-rakennuskielto-arvot" %}
```arvo```-attribuutin arvona saa esiintyä TekstiArvo, joka kuvaa asemakaavan rakennuskiellon informatiivisen sisällön tietojärjestelmissä tai rekistereissä.
{% include clause_end.html %}

### Asemakaavan toimenpiderajoitus

**Koodi:** http://uri.suomi.fi/codelist/rytj/RY_MaankayttorajoituksenLaji/code/02

<!--Lisää sisäiset linkit vielä -->
{% include clause_start.html type="req" id="prof-mkp/vaat-asemakaavan-toimenpiderajoitus" %}
Ilmaisee, että kyseinen maankäyttörajoitus koskee asemakaavan toimenpiderajoitusta.
{% include clause_end.html %}

<!--Lisää sisäiset linkit vielä -->
{% include clause_start.html type="req" id="prof--mkp/vaat-asemakaavan-toimenpiderajoitus-arvot" %}
```arvo```-attribuutin arvona saa esiintyä TekstiArvo, joka kuvaa asemakaavan toimenpiderajoituksen informatiivisen sisällön tietojärjestelmissä tai rekistereissä.
{% include clause_end.html %}

### Rakennusjärjestyksen erityisharkinta-alue

**Koodi:** http://uri.suomi.fi/codelist/rytj/RY_MaankayttorajoituksenLaji/code/07

<!--Lisää sisäiset linkit vielä -->
{% include clause_start.html type="req" id="prof-mkp/vaat-erityisharkinta-alue" %}
Ilmaisee, että kyseinen maankäyttörajoitus koskee Rakennusjärjestyksen erityisharkinta-aluetta 
{% include clause_end.html %}

<!--Lisää sisäiset linkit vielä -->
{% include clause_start.html type="req" id="prof--mkp/vaat-erityisharkinta-alue-arvot" %}
```arvo```-attribuutin arvona saa esiintyä nolla tai useampi TekstiArvo, jotka kuvaavat rakennusjärjestyksen erityisharkinta-alueen informatiivisen sisällön tietojärjestelmissä tai rekistereissä.
{% include clause_end.html %}

