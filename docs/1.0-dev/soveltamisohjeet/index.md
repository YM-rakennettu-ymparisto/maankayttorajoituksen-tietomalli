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

### Asemakaavan rakennuskielto

**Koodi:** http://uri.suomi.fi/codelist/rytj/RY_MaankayttorajoituksenLaji/code/01

<!--Lisää sisäiset linkit vielä -->
{% include clause_start.html type="req" id="prof-tjs/vaat-esitontti" %}
Ilmaisee, että esitonttikohde kuvaa esitontin 2-ulotteisena alueena tai 3-ulotteisena kappaleena.
{% include clause_end.html %}

<!--Lisää sisäiset linkit vielä -->
{% include clause_start.html type="req" id="prof-tjs/vaat-esitontti-arvot" %}
```arvo```-attribuutin arvona saa esiintyä nolla tai yksi Tunnusarvo, jotka kuvaavat tulevan tontin tunnusarvoa tietojärjestelmissä tai rekistereissä.
{% include clause_end.html %}

### Asemakaavan toimenpiderajoitus

**Koodi:** http://uri.suomi.fi/codelist/rytj/RY_MaankayttorajoituksenLaji/code/02

<!--Lisää sisäiset linkit vielä -->
{% include clause_start.html type="req" id="prof-tjs/vaat-esitonttirajapiste" %}
Ilmaisee, että esitonttikohde kuvaa sijainnin, johon on tarkoitus rakentaa kiinteistönmuodostustoimituksessa rajamerkki.
{% include clause_end.html %}

<!--Lisää sisäiset linkit vielä -->
{% include clause_start.html type="req" id="prof-tjs/vaat-esitonttrajapiste-arvot" %}
```arvo```-attribuutin arvona saa esiintyä nolla tai useampi TekstiArvo, jotka kuvaavat tulevan tontin rajamerkkien numeroita tietojärjestelmissä tai rekistereissä.
{% include clause_end.html %}

### Maakuntakaavan rakentamisrajoitus

**Koodi:** http://uri.suomi.fi/codelist/rytj/RY_MaankayttorajoituksenLaji/code/03

<!--Lisää sisäiset linkit vielä -->
{% include clause_start.html type="req" id="prof-tjs/vaat-esitonttirajapiste" %}
Ilmaisee, että esitonttikohde kuvaa sijainnin, johon on tarkoitus rakentaa kiinteistönmuodostustoimituksessa rajamerkki.
{% include clause_end.html %}

<!--Lisää sisäiset linkit vielä -->
{% include clause_start.html type="req" id="prof-tjs/vaat-esitonttrajapiste-arvot" %}
```arvo```-attribuutin arvona saa esiintyä nolla tai useampi TekstiArvo, jotka kuvaavat tulevan tontin rajamerkkien numeroita tietojärjestelmissä tai rekistereissä.
{% include clause_end.html %}

### Yleiskaavan rakennuskielto

**Koodi:** http://uri.suomi.fi/codelist/rytj/RY_MaankayttorajoituksenLaji/code/04

<!--Lisää sisäiset linkit vielä -->
{% include clause_start.html type="req" id="prof-tjs/vaat-esitonttirajapiste" %}
Ilmaisee, että esitonttikohde kuvaa sijainnin, johon on tarkoitus rakentaa kiinteistönmuodostustoimituksessa rajamerkki.
{% include clause_end.html %}

<!--Lisää sisäiset linkit vielä -->
{% include clause_start.html type="req" id="prof-tjs/vaat-esitonttrajapiste-arvot" %}
```arvo```-attribuutin arvona saa esiintyä nolla tai useampi TekstiArvo, jotka kuvaavat tulevan tontin rajamerkkien numeroita tietojärjestelmissä tai rekistereissä.
{% include clause_end.html %}

### Yleiskaavan toimenpiderajoitus

**Koodi:** http://uri.suomi.fi/codelist/rytj/RY_MaankayttorajoituksenLaji/code/05

<!--Lisää sisäiset linkit vielä -->
{% include clause_start.html type="req" id="prof-tjs/vaat-esitonttirajapiste" %}
Ilmaisee, että esitonttikohde kuvaa sijainnin, johon on tarkoitus rakentaa kiinteistönmuodostustoimituksessa rajamerkki.
{% include clause_end.html %}

<!--Lisää sisäiset linkit vielä -->
{% include clause_start.html type="req" id="prof-tjs/vaat-esitonttrajapiste-arvot" %}
```arvo```-attribuutin arvona saa esiintyä nolla tai useampi TekstiArvo, jotka kuvaavat tulevan tontin rajamerkkien numeroita tietojärjestelmissä tai rekistereissä.
{% include clause_end.html %}

### Yleiskaavan erityisharkinta-alue

**Koodi:** http://uri.suomi.fi/codelist/rytj/RY_MaankayttorajoituksenLaji/code/06

<!--Lisää sisäiset linkit vielä -->
{% include clause_start.html type="req" id="prof-tjs/vaat-esitonttirajapiste" %}
Ilmaisee, että esitonttikohde kuvaa sijainnin, johon on tarkoitus rakentaa kiinteistönmuodostustoimituksessa rajamerkki.
{% include clause_end.html %}

<!--Lisää sisäiset linkit vielä -->
{% include clause_start.html type="req" id="prof-tjs/vaat-esitonttrajapiste-arvot" %}
```arvo```-attribuutin arvona saa esiintyä nolla tai useampi TekstiArvo, jotka kuvaavat tulevan tontin rajamerkkien numeroita tietojärjestelmissä tai rekistereissä.
{% include clause_end.html %}

### Rakennusjärjestyksen erityisharkinta-alue

**Koodi:** http://uri.suomi.fi/codelist/rytj/RY_MaankayttorajoituksenLaji/code/07

<!--Lisää sisäiset linkit vielä -->
{% include clause_start.html type="req" id="prof-tjs/vaat-esitonttirajapiste" %}
Ilmaisee, että esitonttikohde kuvaa sijainnin, johon on tarkoitus rakentaa kiinteistönmuodostustoimituksessa rajamerkki.
{% include clause_end.html %}

<!--Lisää sisäiset linkit vielä -->
{% include clause_start.html type="req" id="prof-tjs/vaat-esitonttrajapiste-arvot" %}
```arvo```-attribuutin arvona saa esiintyä nolla tai useampi TekstiArvo, jotka kuvaavat tulevan tontin rajamerkkien numeroita tietojärjestelmissä tai rekistereissä.
{% include clause_end.html %}

