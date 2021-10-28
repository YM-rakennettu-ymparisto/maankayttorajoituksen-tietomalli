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

Kaikki muut maankäyttörajoitusten lajien arvot linkitetään maankäyttörajoituksia sisältäviltä kaavakohteilta ja niiden kaavamääräyksistä. Ainoana poikkeuksena on rakennusjärjestyksen erityisharkinta-alue.

### Rakennusjärjestyksen erityisharkinta-alue

**Koodi:** http://uri.suomi.fi/codelist/rytj/RY_MaankayttorajoituksenLaji/code/07

<!--Lisää sisäiset linkit vielä -->
{% include clause_start.html type="req" id="prof-mkp/vaat-erityisharkinta-alue" %}
Ilmaisee, että kyseinen maankäyttörajoitus koskee Rakennusjärjestyksen erityisharkinta-aluetta 
{% include clause_end.html %}

<!--Lisää sisäiset linkit vielä -->
{% include clause_start.html type="req" id="prof--mkp/vaat...-arvot" %}
```arvo```-attribuutin arvona saa esiintyä nolla tai useampi TekstiArvo, jotka kuvaavat rakennusjärjestyksen erityisharkinta-alueen informatiivisen sisällön tietojärjestelmissä tai rekistereissä.
{% include clause_end.html %}

