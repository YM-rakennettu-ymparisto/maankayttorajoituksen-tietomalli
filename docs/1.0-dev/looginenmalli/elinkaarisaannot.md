---
layout: "default"
title: "Elinkaarisäännöt"
description: ""
page: "elinkaarisaannot"
modelversion: "1.0-dev"
status: "Keskeneräinen"
---

# Elinkaarisäännöt
{:.no_toc}

1. 
{:toc}

## Johdanto

Tietomalleilla on elinkaari, joka määrää niiden sisältämien tietokohteiden: 

- Syntytavan
- Sen, voivatko ne muuttua
- Miten ne voivat muuttua
- Miten ne raukeaa tai kumoutuu johtaen niiden voimassaolon päättymiseen

Elinkaarisääntöjen määrittely liittyy olennaisesti tietokohteiden versionhallintaan, eli miten yksittäisten tietokohteiden niiden elinkaaren aikana muodostettavat versiot voidaan tallentaa ja yksilöidä viittauskelpoisten pysyvien tunnusten avulla. 

Tässä annetut säännöt pohjautuvat paikkatietokohteiden yksilöivien tunnusten ja elinkaarisääntöjen periaatteisiin, jotka on kuvattu jukishallinnon suosituksessa [JHS 193 - Paikkatiedon yksilöivät tunnukset](http://www.jhs-suositukset.fi/suomi/jhs193).

### HTTP URI -tunnukset

HTTP URI -muotoiset tunnukset ovat [RFC 3986 -standardiin](https://tools.ietf.org/html/rfc3986) perustuvia HTTP(S) -protokollan mukaisia URI-osoitteita (Uniform Resource Identifier), joiden globaali yksilöivyys varmistetaan Internetin DNS-nimipalveluun rekisteröityjen domain-nimien avulla. Kullakin DNS-palveluun rekisteröidyllä domain-nimellä (esim. ```uri.suomi.fi```) on yksiselitteinen omistaja, joka on suoraan tai välillisesti vastuussa ko. domain-nimen alla julkaistavasta sisällöstä. Nimen omistaja on myös ainoa taho, joka voi päättää ko. domain-nimeä käyttävien osoitteiden ohjautumisesta haluttuihin resursseihin, mikä tekee siitä luontevan perustan yksilöivien tunnusten nimiavaruuksille (esim. <http://uri.suomi.fi/object/rytj/kaava>). HTTP URI -muotoisen tunnuksen yksilöivyys perustuu siis domain-nimien ja siten niihin perustuvien nimiavaruuksien keskitettyyn hallintaprosessiin.

URI-tunnuksen ei tarvitse viitata konkreettiseen sijaintiin internetissä, vaan se voi olla abstraktimpi tunnus. [JHS 193 Paikkatiedon yksilöivät tunnukset](http://www.jhs-suositukset.fi/suomi/jhs193) määrittelee paikkatiedon yksilöiville tunnuksille muodon <http://paikkatiedot.fi/{tunnustyyppi}/{aineistotunnus}/{paikallinen tunnus}>, jossa paikkatietokohteiden ```tunnustyyppi``` on ```so```. Maankäyttörajoitusten tietomallissa on esimerkkinä käytetty tunnusmuotoa 
<http://uri.suomi.fi/object/rytj/{aineistotyyppi}/{TietotyypinNimi}/{paikallinenTunnus}>. HTTP URI -muotoisen tunnuksen etuna on luettavuus sekä DNS- ja HTTP-protokollien tarjoama kyky ratkaista (resolve) tunnus ja ohjata kysyjä sitä kuvaavaan Internet-resurssiin ilman tarvetta erityiselle keskitetylle tunnusrekisterille ja siihen perustuvalle ratkaisupalvelulle.

Maankäyttörajoitusten tietomallissa HTTP URI -muotoa käytetään [viittaustunnus](#viittaustunnus)-attribuutissa, jonka avulla viitataan tiettyyn versioon tietokohteesta maankäyttörajoitusten ulkopuolelta.

### UUID-tunnukset
UUID (Universally Unique Identifier) on OSF:n (Open Software Foundation) määrittelemä standardoitu tunnusmuoto, jonka avulla voidaan luoda vakiokokoisia, hyvin suurella todennäköisyydellä yksilöiviä tunnuksia ilman keskitettyä hallintajärjestelmää. UUID-tunnukset voivat perustua satunnaislukuihin, aikaleimoihin, tietokoneiden verkkokorttien MAC-osoitteisiin tai merkkijonomuotoisiin nimiavaruuksiin eri yhdistelmissä. UUID-tunnukset erityisen hyvin tietojärjestelmissä, joissa uusia globaalisti pysyviä ja yksilöiviä tunnuksia on tarpeen luoda hajautetusti ilman keskitettyä tunnusrekisteriä.


Maankäyttörajoitusten tietomallissa UUID-muotoisia tunnuksia suositellaan käytettäväksi [identiteettiTunnus-](#identiteettitunnus), maankäyttörajoituksenTunnus-attribuuttien arvoina.

## Tietomallien kohteiden elinkaaren hallinnan periaatteet

Maankäyttörajoitusten tietomallin elinkaarisäännöt mahdollistavat tietomallin tietokohteiden käsittelyn, tallentamisen ja muuttamisen hallitusti sekä niiden eri voimassaolovaiheissa. Maankäyttörajoitusten tietomallin mukaiset tietosisällöt ovat merkittäviä oikeusvaikutuksia aiheuttavia, juridisesti päteviä aineistoja, joita käsitellään hajautetusti eri toimijoiden tietojärjestelmissä. Tämän vuoksi niiden tunnusten, viittausten ja versionnin hallintaan on syytä kiinnittää erityistä huomiota.

Seuraavat keskeiset periaatteet ohjaavat maankäyttörajoitusten elinkaaren hallintaa:
* Kukin maankäyttörajoitusten tietovarastoon tallennettu versio maankäyttörajoituksesta saa pysyvän, versiokohtaisen tunnuksen.
* Kuhunkin maankäyttörajoitusten tietovarastoon tallennetun tietokohteen versioon voidaan viitata sen pysyvän tunnuksen avulla.
* Maankäyttörajoitusten tietomallin tietokohteiden väliset viittaukset toteutetaan hallitusti sekä maankäyttörajoitustietoa tuottavissa tietojärjestelmissä että yhteisissä maankäyttörajoitusten tietovarastoissa.
* Maankäyttörajoitusten tietovarasto vastaa pysyvien tunnusten luomisesta ja antamisesta tallennettaville tietokohteille.

Maankäyttörajoitusten tietomallin mukaisten aineistojen tallentamisessa erotetaan toisistaan tietojen tuottaminen ja muokkaus sisäisesti niiden tuottamiseen ja muokkaamiseen käytettävissä tietojärjestelmissä ja niiden hallinta yhteisessä versiohallitussa maankäyttörajoitusten tietovarastoissa. Maankäyttörajoitusten tietomallin ei ole mielekästä asettaa vaatimuksia maankäyttörajoitustietoa tuottavien tietojärjestelmien tunnusten ja versioiden hallintaan, vaan tietomallissa tulee varautua siihen, että yhteiseen tietovarastoon tallennettavia tietoja on muokattu ja tallennettu sisäisesti tuntematon määrä kertoja ennen ensimmäistä viemistä yhteiseen tietovarastoon, ja samoin tuntematon määrä kertoja kunkin yhteiseen varastoon vietävän version välillä. Näin ollen on mahdollista, että maankäyttörajoituksesta voi olla joissain tietojärjestelmissä tallennettuna paikallisia versiota, joita ei ole koskaan viety yhteiseen maankäyttörajoitusten tietovarastoon.

## Tunnukset ja niiden hallinta

### Identiteettitunnus
Identiteettitunnus yhdistää saman tunnistettavan tietokohteen kehitysversiot toisiinsa.

{% include clause_start.html type="req" id="elinkaari/vaat-identiteettitunnus-maar" %}
Tietomallin tietokohteissa identiteettitunnus kuvataan attribuutilla ```identiteettiTunnus```. Kahdella versioitavalla objektilla voi olla sama ```identiteettiTunnus```-attribuutin arvo ainoastaan, mikäli kaikki seuraavista ehdoista ovat tosia:

* Molemmat objektit kuvaavat saman tietokohteen tai sen sisältämän, nimettävissä olevan tietokohteen kehityskaaren eri tiloja.
* Molemmat objektit liittyvät samaan tietokohteeseen.
* Molemmat objektit ovat saman loogisen tietomallin luokan edustajia.
{% include clause_end.html %}

Yksittäisen tietokohteen koko ko. tietojärjestelmään tallennettu kehityshistoria saadaan noutamalla kaikki ko. tyyppisen tietokohteen objektit, joilla on sama ```identiteettiTunnus```-attribuutin arvo.

Yhteinen tietovarasto on vastuussa uusien identiteettitunnusten luomisesta tarvittaessa tallennustapahtumien yhteydessä, ja niiden välittämisestä tiedoksi tallentavalle tietojärjestelmälle. Tallentavan tietojärjestelmän tulee tallentaa itselleen kopiot tietovaraston tallennustapahtuman yhteydessä palautamista maankäyttörajoitusten tietokohteiden identiteettitunnuksista, sillä ne tulee sisällyttää ko. tietokohteiden seuraavien versioden tallennettavaksi lähetettäviin objekteihin.

{% include clause_start.html type="req" id="elinkaari/vaat-identiteettitunnus-gen" %}
* Mikäli tallennettavalle tietokohteelle ei ole annettu ```identiteettitunnus```-attribuuttia, tai tietovarasto ei sisällä sellaista saman luokan tietokohdetta, jolla on sama ```identiteettiTunnus```-attribuutin arvo, tietovarasto luo ko. objektille uuden identiteettitunnuksen, joka korvaa tuottavan tietojärjestelmän objektille mahdollisesti antaman ```identiteettiTunnus```-attribuutin arvon. Tällöin objektia pidetään uuden tietokohteen ensimmäisenä versiona.
* Mikäli tietovarasto sisältää saman luokan tietokohteen, jolla on sama ```identiteettiTunnus```-attribuutin arvo kuin tallennetavalla objektilla, objekti tallennetaan tietovarastoon ko. tietokohteen uutena versiona. Tällöin tallennettavan objektin ```identiteettiTunnus```-attribuutin arvo ei muutu.
{% include clause_end.html %}

<!--
{% include clause_start.html type="req" id="elinkaari/vaat-kaavan-identiteettitunnus" %}
[Maankayttorajoitus](../../looginenmalli/dokumentaatio/#maankayttorajoitus)-luokan tietokohteen tallennuksen yhteydessä maankäyttörajoitusten tietovarasto tarkistaa, että sen attribuutti ```maankayttorajoituksenTunnus``` on annettu ja validi.
* Mikäli kohde katsotaan sen ```identiteettiTunnus```-attribuutin arvon perusteella uudeksi tietokohteeksi, sama ```maankayttorajoituksenTunnus```-attribuutti ei saa olla käytössä muilla [Maankayttorajoitus](../../looginenmalli/dokumentaatio/#maankayttorajoitus)-luokan objekteilla.
* Mikäli kohde katsotaan sen ```identiteettiTunnus```-attribuutin arvon perusteella aiemmin tallennetun tietokohteen uudeksi versioksi, aiemmin tallennetun version ```maankayttorajoituksenTunnus```-attribuutin tulee olla sama kuin tallennettavassa objektissa.
{% include clause_end.html %}
-->

{% include clause_start.html type="rec" id="elinkaari/suos-identiteettitunnus-form" %}
Identiteettitunnuksen suositeltu muoto on UUID.
{% include clause_end.html %}

Esimerkki: ```640bff6b-c16a-4947-af8d-d86f89106be1```

### Paikallinen tunnus
Paikallinen tunnus yksilöi tietokohteen yhden version tietovaraston sisällä. 

{% include clause_start.html type="req" id="elinkaari/vaat-paikallinentunnus-maar" %}
Tietomallien tietokohteissa paikallinen tunnus kuvataan attribuutilla ```paikallinenTunnus```. Kaikilla saman tietovaraston objekteilla (ml. saman tietokohteen eri versiot) tulee olla eri ```paikallinenTunnus```-attribuutin arvo.
{% include clause_end.html %}

{% include clause_start.html type="req" id="elinkaari/vaat-paikallinentunnus-gen" %}
Tietokohteiden paikallinen tunnus muuttuu sen jokaisen version tallennuksen yhteydessä. Tietovarasto vastaa paikallisten tunnusten luomisesta tallennustapahtuman yhteydessä. Tuottavan tietojärjestelmän mahdollisesti asettamat arvot korvataan.
{% include clause_end.html %}

{% include clause_start.html type="req" id="elinkaari/vaat-paikallinentunnus-form" %}
Paikallinen tunnus koostuu identiteettitunnuksesta ja siihen erotinmerkillä liitetystä versiokohtaisesta, esimerkiksi tarkkaan tallennusajanhetkeen perustuvasta merkkijonosta.
{% include clause_end.html %}

{% include clause_start.html type="rec" id="elinkaari/suos-paikallinentunnus-merk" %}
Paikallisen tunnuksen muodostamisessa tulee välttää merkkejä, jotka joudutaan URL-koodaamaan rajapintapalvelujen kutsuissa. Paikkatietokohteen paikallista tunnusta käytetään fyysisten tietomallien pääavaimena, esim. GeoJSON Feature ```id```-omaisuuden ja GML:n ```gml:id```-attribuutin arvona, ja siten esimerkiksi OGC Web Feature Service (WFS) - ja OGC API - Features -rajapintapalvelujen paikkatietokohteen yksilöivissä kyselyissä.
{% include clause_end.html %}

Tallennusajanhetkeen päättyvää paikallista tunnusta voidaan käyttää ilman sekaannusmahdollisuuksia samalla logiikalla myös paikallisissa versionneissa, eli sellaisissa tietokohteen versioiden tallennuksissa, joita ei viedä lainkaan tietovarastoon.

Esimerkki:```640bff6b-c16a-4947-af8d-d86f89106be1.b05cf48d46d8c905c54522f44b0a12daff11604e```

{% include note.html content="Käyttämällä paikallisena tunnuksena pelkkää identiteettitunnuksesta riippumatonta UUID-tunnusta päästäisiin lyhyempiin tunnuksiin, mutta menetetään yhteys identiteettitunnusten ja paikallisten tunnusten välillä, mikä saattaa hankaloittaa erilaisten vikatilanteiden selvitystä ja toimintavarmuuden testaamista, kun pelkkien tunnusten perusteella ei voida päätellä ovatko kaksi objektia saman tietokohteen eri versioita." %}

### Nimiavaruus
{% include clause_start.html type="req" id="elinkaari/vaat-nimiavaruus-maar" %}
Nimiavaruus määrää tietomallin kaikkien tietokohteiden viittaustunnusten alkuosan yhden tietovaraston sisällä. Maankäyttörajoitusten tietomallin tietokohteissa paikallinen tunnus kuvataan attribuutilla ```nimiavaruus```.
{% include clause_end.html %}

{% include clause_start.html type="req" id="elinkaari/vaat-nimiavaruus-form" %}
Nimiavaruus on HTTP URI -muotoinen.
{% include clause_end.html %}

Nimiavaruus on syytä valita huolella siten, että se olisi mahdollisimman pysyvä, eikä sitä tarvitsisi tulevaisuudessa muuttaa esimerkiksi valtionhallinnon virastojen tai ministeriröiden mahdollisten uudelleenorganisointien ja -nimeämisten johdosta. Valittu URL-osoite tulee myös voida aina tarvittaessa ohjata kulloinkin käytössä olevaan rajapintapalveluun (HTTP redirect). 

{% include clause_start.html type="req" id="elinkaari/vaat-nimiavaruus-gen" %}
Tietovarasto vastaa ```nimiavaruus```-attribuuttien asetamisesta tallennustapahtuman yhteydessä. Tuottavan tietojärjestelmän mahdollisesti antamat arvot korvataan.
{% include clause_end.html %}

Esimerkki: ```http://uri.suomi.fi/object/rytj/mkr```

### Viittaustunnus
{% include clause_start.html type="req" id="elinkaari/vaat-viittaustunnus-maar" %}
Viittaustunnus yksilöi tietokohteen yhden, keskitettyyn tietovarastoon tallennetun kehitysversion globaalisti. Tietomallin tietokohteissa paikallinen tunnus kuvataan attribuutilla ```viittausTunnus```.
{% include clause_end.html %}

{% include clause_start.html type="req" id="elinkaari/vaat-viittaustunnus-form" %}
Viittaustunnus on HTTP URI -muotoinen ja se muodostuu nimiavaruudesta, tietokohteen luokan nimestä ja paikallisesta tunnuksesta yhdessä kauttaviivoilla (```/```) erotettuina.
{% include clause_end.html %}

{% include clause_start.html type="req" id="elinkaari/vaat-nimiavaruus-gen" %}
Tietovarasto vastaa ```viittausTunnus```-attribuuttien asetamisesta tallennustapahtuman yhteydessä. Tuottavan tietojärjestelmän mahdollisesti antamat arvot korvataan.
{% include clause_end.html %}

Tallentavan tietojärjestelmän ei siis tarvitse tallentaa luotuja viittaustunnuksia itselleen seuraavia tallennuksia varten.

{% include clause_start.html type="rec" id="elinkaari/suos-viittaustunnus-ohj" %}
Viittaustunnuksen on suositeltavaa ohjautua aina ko. tietokohteen version tietosisältöön kulloinkin toiminnassa olevassa tietovaraston latauspalvelussa.
{% include clause_end.html %}

Esimerkki: ```http://uri.suomi.fi/object/rytj/mkr/maankayttorajoitus/640bff6b-c16a-4947-af8d-d86f89106be1.b05cf48d46d8c905c54522f44b0a12daff11604e```

### Tuottajakohtainen tunnus

{% include clause_start.html type="req" id="elinkaari/vaat-tuottajakohtainen-tunnus-maar" %}
Tietokohdetietoa tuottavat järjestelmät voivat niin halutessaan käyttää tuottajakohtaista tunnusta niiden omien tietojärjestelmäspesifisten tunnusten antamiseen  tietomallin tietokohteille. Tietomallin tietokohteissa tuottajakohtainen tunnus kuvataan attribuutilla ```tuottajakohtainenTunnus```.
{% include clause_end.html %}

{% include clause_start.html type="req" id="elinkaari/vaat-tuottajakohtainen-tunnus-gen" %}
Tietovarasto ei koskaan muuta tuottavan tietojärjestelmän mahdollisesti asettamia tuottajakohtaisia tunnuksia, ja ne palautetaan sellaisenaan latattaessa tietokohteita tietovarannosta.
{% include clause_end.html %}

Tietojärjestelmät voivat käyttää tuottajakohtaisia tunnuksia kohdistamaan tietovarastoon ja paikallisiin tietojärjestelmiin tallennettuja tietokohteita toisiinsa esimerkiksi päivitettäessä niiden tallennuksen yhteydessä syntyneitä tunnuksia, vertailtaessa tietovarastoon tallennettuja kohteita ja paikallisia kohteita toisiinsa, sekä esitettäessä validointipalvelun tuloksia suunnitteluohjelmiston käyttäjälle.

Tuottajakohtaisilta tunnuksilta ei vaadita yksilöivyyttä tai mitään tiettyä yhtenäistä muotoa, mutta UUID-muodon käyttäminen tarjoaa hyvin määritellyn ja standardoidun tavan luoda tuottajakohtaisista tunnuksista yksilöiviä eri tietojärjestelmien kesken. Tästä saattaa olla etua haluttaessa tehdä tuotettavista tietokohdetiedoista mahdollisimman järjestelmäriippumattomia ja esimerkiksi taata tuottajakohtaisten tunnusten yksilöivyys yli mahdollisten tietoa tuottavien tietojärjestelmien vaihdosten ja päivitysten.


{% include clause_start.html type="rec" id="elinkaari/suos-tuottajakohtainen-tunnus-form" %}
Tuottajakohtaisen tunnuksen suositeltu muoto on UUID.
{% include clause_end.html %}

Esimerkki: ```mkr-123445```

### Maankäyttörajoituksen tunnus
{% include clause_start.html type="req" id="elinkaari/vaat-maankayttorajoitustunnus-maar" %}
Maankäyttörajoituksen tunnus on maankäyttöpäätökselle ennakolta haettava, maankäyttöpäätöksen kansallisesti yksilöivä tunnus. Maankäyttörajoitusten tietomallissa maankäyttörajoituksen tunnus kuvataan [Maankayttorajoitus](../../looginenmalli/dokumentaatio/#maankayttorajoitus)-luokan attribuutilla ```maankayttorajoitusTunnus```.
{% include clause_end.html %}

{% include clause_start.html type="req" id="elinkaari/vaat-maankayttorajoitustunnus-gen" %}
Tuottava tietojärjestelmän vastaa maankäyttörajoituksen tunnuksen asettamisesta [Maankayttorajoitus](../../looginenmalli/dokumentaatio/#maankayttorajoitus)-luokan attribuutiksi. Se tulee olla asetettuna myös maankäyttörajoituksen ensimmäisen maankäyttörajoitusten tietovarastoon tallennuksen yhteydessä.
{% include clause_end.html %}

{% include clause_start.html type="req" id="elinkaari/vaat-maankayttorajoitustunnus-yks" %}
Maankäyttörajoituksen tunnus on [Maankayttorajoitus](../../looginenmalli/dokumentaatio/#maankayttorajoitus)-luokan objekteille globaalisti yksilöivä, eikä muutu saman Maankäyttörajoituksen eri elinkaaren aikaisten versioiden tallennuksen yhteydessä.
{% include clause_end.html %}

Käytännössä myönnetyt maankäyttörajoitusten tunnukset  kannattaa tallentaa valmiiksi maankäyttörajoitusten tietovarastoon, jotta voidaan tarkistaa, onko tallennettavaksi tarkoitettu maankäyttörajoituksen tunnus myönnetty organisaatiolle, jonka maankäyttörajoitusta ollaan tallentamassa. Kuntakoodin tai muun hallinnollisen alueen tunnuksen käyttö osana maankäyttörajoituksen tunnus tunnusta ei ole suositeltavaa, sillä hallinnolliset alueet muuttuvat ajan kuluessa. Kun sidos tunnuksen ja hallinnollisen alueen välillä ei näy tunnuksessa, voidaan maankäyttörajoituksen hallinnollista aluetta muuttaa joustavammin maankäyttörajoituksen elinkaaren aikana.

{% include clause_start.html type="rec" id="elinkaari/suos-tonttijakosuunnitelmatunnus-form" %}
Maankäyttörajoituksen tunnuksen suositeltu muoto on UUID.
{% include clause_end.html %}

Esimerkki: ```df5b2d6f-d6d6-4695-938c-dd7c4c784c28```

### Pysyvien tunnusten palauttaminen tuottavalle järjestelmälle

Versionhallinnan näkökulmasta on tärkeää, että maankäyttörajoituksen tuottava tietojärjestelmä käyttää saman maankäyttörajoituksen seuraavan version tallentamisessa maankäyttörajoituksen ensimmäisen version tallennuksen yhteydessä luotua identiteettitunnusta. Vastaavasti kaikkien maankäyttörajoituksen tietokohteiden osalta käytetään niiden ensimmäisen tallennuksen yhteydessä luotuja identiteettitunnuksia, mikäli objektin katsotaan kuvaavan ko. tietokohteen uutta versiota.

{% include clause_start.html type="req" id="elinkaari/vaat-tunnusten-palautus" %}
Tietovaraston tallennusrajapinta palauttaa tallennetun maankäyttörajoituksen tiedot tuottavalle tietojärjestelmälle tallennusoperaation yhteydessä siten, että ne sisältävät yllä mainittujen tunnustenhallintasääntöjen mukaisesti mahdollisesti generoidut tai muokatut identiteettitunnukset, paikalliset tunnukset, nimiavaruudet ja viittaustunnukset kaikille tallennetuille tietokohteille.
{% include clause_end.html %}

### Maankäyttörajoituksen tietokohteisiin viittaaminen ja viitteiden ylläpito

{% include clause_start.html type="req" id="vaat-tonttijakosuunnitelman-sisaiset-viittaukset" %}
Saman maankäyttörajoituksen tietokohteiden keskinäiset assosiaatiot toteutetaan viitattavan tietokohteen [paikallinenTunnus](#paikallinen-tunnus)-attribuuttia käyttäen.
{% include clause_end.html %}

{% include clause_start.html type="req" id="elinkaari/vaat-tietovaraston-sisaiset-viittaukset" %}
Maankäyttörajoituksen tietokohteen luokkien assosiaatiot eri maankäyttörajoitusten välillä tai maankäyttörajoituksen ja muiden maankäyttöpäätösten tietokohteiden välillä toteutetaan viitattavan tietokohteen [viittaustunnus](#viittaustunnus)-attribuuttia käyttäen.
{% include clause_end.html %}

{% include clause_start.html type="req" id="elinkaari/vaat-viittaukset-ulkoa" %}
Pysyvät viittaukset maankäyttörajoitusten tietomallin ulkopuolelta tietomallin tietokohteisiin toteutetaan viitattavan tietokohteen [viittaustunnus](#viittaustunnus)-attribuuttia käyttäen.
{% include clause_end.html %}

{% include clause_start.html type="req" id="elinkaari/vaat-viittaukset-tallennettaessa" %}
Tallennettaessa maankäyttörajoitusten tietomallin tietokohteita maankäyttörajoitusten tietovarastoon tietokohteiden tunnukset muuttuvat niiden pysyvään muotoon, kuten kuvattu luvussa [Tunnukset ja niiden hallinta](#tunnukset-ja-niiden-hallinta). Maankäyttörajoitusten tietovaraston vastuulla on päivittää kunkin paikallisen tunnuksen muuttamisen yhteydessä myös kaikkien ko. tietokohteen versioon sen paikallisen tunnuksen avulla viittaavien muiden ko. maankäyttörajoituksen tietokohteiden viittaukset käyttämään tietokohteen muutettua paikallista tunnusta.   
{% include clause_end.html %}
<!--
### Koodistojen koodien tunnuksiin liittyvät vaatimukset

{% include clause_start.html type="req" id="elinkaari/vaat-koodien-yksiloivat-tunnukset" %}
Kullakin koodiston koodilla on oltava pysyvä tunnus, joka sellaisenaan yksilöi kyseisen koodin globaalisti ilman erilistä tietoa koodistosta, johon koodi kuuluu. Koodin tunnus on HTTP URI -muotoinen.
{% include clause_end.html %}

{% include clause_start.html type="req" id="elinkaari/vaat-alakoodi-maar" %}
Olkoon koodi ```A``` mikä tahansa hierarkkisen koodiston sisältämä koodi. Koodin ```A``` alakoodilla tarkoitetaan koodia, joka on hierakkiassa sijoitettu koodin ```A``` alle. Koodi voi olla useamman ylemmän tason koodin alakoodi vain mikäli ko. ylemmän tason koodit ovat alakoodisuhteessa keskenään.
{% include clause_end.html %}

Käytännössä tietyn koodin alakoodit voidaan tunnistaa vertaamalla niiden tunnuksia:

{% include clause_start.html type="req" id="elinkaari/vaat-alakoodi-tunnus" %}
Koodin ```A``` alakoodin ```B``` tunnus alkaa koodin ```A``` tunnuksella ja sisältää sen jälkeen yhden tai useamman merkin.
{% include clause_end.html %}
-->

## Muutokset ja tietojen versionti
{% include clause_start.html type="req" id="elinkaari/vaat-pysyva-sisalto" %}
Kukin maankäyttörajoituksen tallennusoperaatio yhteiseen tietovarastoon muodostaa uuden version tallennettavista tietokohteista, mikäli yksittäinen tietokohde on miltään osin muuttunut verrattuna sen edelliseen versioon. Myös muutokset muissa maankäyttörajoitusten tietomallin tietokohteissa, joihin tietokohteesta on viittaus, lasketaan tietokohteen muutoksiksi. Tallennetun tietokohteen version sisältö ei voi muuttua tallennuksen jälkeen, poislukien sen voimassaolon päättymiseen, seuraavaan versioon linkittämiseen ja elinkaaritilaan liittyvät attribuutit, joita maankäyttörajoitusten tietovarasto itse päivittää tietyissä tilanteissa.
{% include clause_end.html %}

Näin taataan ulkoisten viittausten eheys, sillä maankäyttörajoituksen kaikkien kohteiden paikalliset ja viittaustunnukset viittaavat aina vain tietyn, sisällöllisesti muuttumattomaan versioon viittatusta kohteesta. Suositeltavaa on, että kaikki tallennusversiot myös pidetään pysyvästi tallessa, jotta mahdolliset keskenäiset ja ulkopuolelta tulevat linkit eivät mene rikki muutosten yhteydessä.

### Muutosten leviäminen viittausten kautta
Maankäyttörajoitusten tietomallin tietokohteiden keskinäiset viittaukset kohdistuvat aina viitattavien tietokohteiden tiettyyn versioon, ja toisaalta kaikki kohteiden sisällölliset muutokset johtavat uusien versioiden tallentamiseen. Siten kohteiden välisten linkkien kohdetietoa täytyy muuttaa mikäli halutaan viitata jollain tapaa muuttuneeseen kohteeseen. Tämä päivitystarve johtaa edelleen myös viittaavan tietokohteen uuden version luomiseen, vaikka ainoa muuttunut tieto olisi linkki uuteen versioon viitatusta tietokohteesta. Molempiin suuntiin tietokohteiden välillä tehty linkitys saattaa siten johtaa hyvin laajalle leviävään muutosketjuun.
<!--
Maankäyttörajoitusten tietomallissa kukin Esitonttikohde on linkitetty kahdensuuntaisesti tonttijakosuunnitelmaan ja kukin Kaavamääräys yhdensuuntaisesti esitonttikohteisiin, joiden alueita ne koskevat. Tällöin uuden kaavamääräyksen luominen johtaa uuden version luomiseen siihen linkitetyistä esitonttikohteista, ja edelleen niihin linkitetystä tonttijakosuunnitelma-objektista, mikä puolestaan johtaa lopulta uusien versioiden luomiseen kaikista ko. tonttijakosuunnitelman muistakin esitonttikohteista, koska tonttijakosuunnitelma-objektiin päin osoittavat linkit pitää muuttaa osoittamaan sen uuteen versioon. 

**Esimerkki**:

Tallennuspalveluun viedään tonttijakosuunnitelma, jonka yhteen esitonttikohteeseen liittyvää kaavamääräystä **asuinpientaloalue** on muutettu kaavaprosessissa **erillispientaloalueeksi**. Kaikki tonttijakosuunnitelman muut tietokohteet ovat identtisiä tonttijakosuunnitelman edellisen tallennusversion kanssa.

- Esitonttikohteesta, johon muuttunut kaavamääräys kohdistuu, luodaan uusi versio, jossa muuttuu vain linkki, viitaten nyt uuteen kaavamääräykseen.
-->
### Yksittäisen maankäyttörajoituksen elinkaaren vaiheisiin liittyvät muutokset
Maankäyttörajoitusten tietomalli mahdollistaa tunnistettavien maankäyttörajoitusten tietokohteiden eri kehitysversioiden erottamisen toisistaan. Kullakin tietomallin kohteella on sekä sen tosimaailman identiteettiin liittyvä ns. identiteettitunnus että yksittäisen tallennusversion tunnus (paikallinen tunnus). Tallennettaessa uutta versiota samasta maankäyttörajoituksesta, sen identiteettitunnus pysyy ennallaan, mutta sen paikallinen tunnus muuttuu. Tallennettaessa Maankayttorajoitus-luokan objektia se katsotaan saman tietokohteen uudeksi versioksi, mikäli sen maankäyttörajoituksen tunnus on sama. Muiden maankäyttörajoitusten tietomallin versioitavien objektien suhteen samuuden määritteleminen on tietoja tuottavien järjestelmien vastuulla: mikäli objektilla on tallennettavaksi lähetettäessä saman ```identititeettiTunnus```-attribuutin arvo kuin aiemmin tallennetulla, samantyyppisellä tietokohteella, katsotaan uusi objekti on saman tietokohteen uudeksi versioksi.

{% include clause_start.html type="req" id="elinkaari/vaat-version-korvaus" %}
Kun maankäyttörajoituksen tietokohteesta tallennetaan uusi muuttunut versio, tulee tietokohteen edellisen version ```korvattuObjektilla```-assosiaatio asettaa viittaamaan tietokohteen uuteen versioon. Uuden tietokohteen version ```korvaaObjektin```-assosiaatio puolestaan asetetaan viittaamaan tietokohteen edelliseen, korvattavaan versioon. Molempien kohteiden ```tallennusAika```-attribuutin arvoksi asetetaan ajanhetki, jolloin tallennus ja muutos maankäyttörajoitusten tietovarastoon on tehty.
{% include clause_end.html %}

Yksittäisen tietokohteen yksityiskohtainen muutoshistoria maankäyttörajoitusten tietovarastossa saadaan seuraamalla sen ```korvattuObjektilla```- ja ```korvaaObjektin```-assosiaatioita. Ainoa muutos, joka ei näy tietokohteen omana versionaan, on kohteen kumoaminen, jolloin sen viimeisimmän version tietoja päivitetään sen elinkaaritilan, voimassaolon ja tallennusajan osalta.

{% include question.html content="Pitääkö [AbstraktiVersioituObjekti](dokumentaatio/#abstraktiversioituobjekti)-luokalle lisätä attribuutti ```ensimmainenTallennusAika```, joka kertoo ko. version alkuperäisen tallennusajan? Kumoamisen yhteydessä ```tallennusAika```-attribuutin arvoa muutetaan, jolloin hukkuu tieto ko. version alkuperäisestä tallennusajankohdasta." %}

Attribuutin ```viimeisinMuutos``` arvo kuvaa ajanhetkeä, jolloin ko. tietokohteeseen on tehty sisällöllinen muutos tiedontuottajan tietojärjestelmässä. Tiedontuottajan järjestelmän osalta ei vaadita tiukkaa versiointipolitiikkaa, eli ```paikallinenTunnus```-attribuutin päivittämistä jokaisen tietokohteen muutoksen johdosta. ```viimeisinMuutos```-attribuutin päivittämien riittää kuvaamaan tiedon todellisen muuttumisajankohdan.

### Maankäyttörajoituksen käsittelytapahtumien elinkaari
Maankäyttörajoitusprosessin historian yhdessä kuvaavat AbstraktiTapahtuma-luokasta perityt Kasittelytapahtuma-luokan tietokohteet linkitetään yksisuuntaisesti AbstraktiMaankayttoasia-luokkaan (Maankayttorajoitus-luokan yläluokka) päin. Tapahtumatietokohteiden uusina versiona tallennettavat muutokset eivät koskaan johda uuden version luomiseen Maankayttorajoitus-luokan tietokohteesta. Syy tähän on se, että käsittelytapahtumien on tärkeää kohdistua nimenomaan tiettyyn, pysyvään versioon maankäyttörajoituksesta.
<!--
Tietyllä ajanhetkellä nähtävillä olevat tai nähtävillä olleet tonttijakosuunnitelman versiot voidaan poimia valitsemalla ne tonttijakosuunnitelmat, joihin kohdistuu Vuorovaikutustapahtuma, jonka laji-attribuutin arvo on Nähtävilläolo, tapahtumaAika-attribuuttin aikaväli kattaa halutun ajankohdan ja peruttu-attribuutin arvo on false. Näiden vuorovaikutustapahtumien liittyvaAsia-assosiaatio viittaa siihen AbstraktiMaankayttoasia-luokan instanssiin, joka ko. aikaan on nähtävillä. Katso tonttijakosuunnitelmaehdotuksen nähtävilläolon ilmoittamiseen liittyvät vaatimukset kohdasta Tonttijakosuunniteman elinkaaritilan muutoksiin liittyvät käsittely- ja vuorovaikutustapahtumat.
-->
{% include clause_start.html type="req" id="elinkaari/vaat-tapahtumien-poistaminen" %}
Kerran tallennettuja AbstraktiTapahtuma-luokan tietokohteita ei voi poistaa maankäyttörajoitusten tietovarastosta. Mikäli suunniteltu käsittelytapahtumaan liittyvä päätös kumotaan, tulee sen attribuutti peruttu asettaa arvoon true.
{% include clause_end.html %}

{% include question.html content="Miten käsittelytapahtumat vaikuttavat versiointiin ja sen muutosketjuun?" %}

{% include question.html content="Miten maankäyttörajoitusten eri elinkaarikoodit vaikuttavat käsittelytapahtumiin?" %}
<!--
### Tonttijakosuunnitelman ja sen tietokohteiden voimaantulo
Tonttijakosuunnitelman ```voimassaoloAika``` -attribuutin alkuaika on ajanhetki, jolloin tonttijakosuunnitelma sen nähtävilläoloajan umpeuduttua ja mahdollisten mielipiteiden käsittelyn jälkeen tulee voimaan.

{% include clause_start.html type="req" id="vaat-tonttijakosuunnitelman-voimaantulo" %}
Voimaantulemisen yhteydessä tonttijakosuunnitelmasta tallennetaan tonttijakosuunnitelmatietovarastoon uusi versio, jossa sen:
- Tonttijakosuunnitelma-luokan objektin elinkaaritila-attribuutin arvoksi on asetettu Voimassa,
- Tonttijakosuunnitelma-luokan objektin voimassaoloAika-attribuutin alkuajaksi on asetettu kuulutuksen ajanhetki ja loppuaikaa ei ole annettu.
{% include clause_end.html %}

{% include clause_start.html type="req" id="elinkaari/vaat-voimassaoloaika" %}
Tonttijakosuunnitelma ja sen esitonttikohteet ovat voimassa niiden voimassaoloAika-attribuuttien määräämillä aikaväleillä. Mikäli voimassaoloAika-attribuutin loppuaika puuttuu, on tietokohde voimassa toistaiseksi.
{% include clause_end.html %}

{% include clause_start.html type="req" id="vaat-elinkaaritila-voimassaoloaika" %}
Tonttijakosuunnitelma ja sen esitonttikohteet voivat olla elinkaaritilassa Voimassa ainoastaan, mikäli niiden voimassaoloAika on annettu ja sisältää vain alkuajan ilman loppuaikaa. Tonttijakosuunnitelman ja sen esitonttikohteiden voimassaoloAika voi olla annettu vain mikäli ne ovat joko elinkaaritilassa Voimassa tai Kumottu. Tonttijakosuunnitelman ja sen esitonttikohteiden voimassaoloAika sisältää sekä alku- että loppuajan vain, kun ne ovat elinkaaritilassa Kumottu.
{% include clause_end.html %}

### Tonttijakosuunnitelman kumoutuminen ja kumoaminen 

Maankäyttö- ja rakennuslain pykälässä XX säädetään tonttijakosuunnitelman kumoutumisesta ja kumoamisesta.

Voimassaoleva tonttijakosuunnitelma voi kumoutua uudella tonttijakosuunnitelmalla osittain tai kokonaan.  Tonttijakosuunnitelma voidaan kumota, jos alueelta kumotaan kokonaan tai osittain se asemakaava, jonka toteuttamiseksi tonttijakosuunnitelma on tehty, kumoutuu myös tonttijakosuunnitelma kyseisen alueen osalta.

Lisää tähän vielä sisäiset linkit kuntoon
{% include clause_start.html type="req" id="elinkaari/vaat-kumoutumistieto-per-tonttijakosuunnitelma" %}
Tonttijakosuunnitelmilla kumoutuvat, aiemmin hyväksyttyjen tonttijakosuunnitelmien esitonttikohteet tulee yksilöidä kumoutuvassa tonttijakosuunnitelmassa. Kutakin tonttijakosuunnitelmaa kohti tulee antaa yksi Tonttijakosuunnitelma-luokan attribuutin kumoamistieto arvo tyyppiä TonttijakosuunnitelmanKumoamistieto, jonka kumottavanTonttijakosuunnitelmanTunnus-attribuutin arvo on kumottavan tonttijakosuunnitelman ```viittaustunnus```.
{% include clause_end.html %}

Lisää tähän vielä sisäiset linkit kuntoon
{% include clause_start.html type="req" id="elinkaari/vaat-kumoutuva-esitonttikohteen-tunnus" %}
Kumoutumisessa esitonttikohteet kuvataan ensisijaisesti kumoattavanEsitonttikohteenTunnus-attribuutin arvojen avulla. Attribuutin arvo on kumottavan Esitonttikohde-luokan tietokohteen ```viittaustunnus```.
{% include clause_end.html %}

Lisää tähän vielä sisäiset linkit kuntoon
{% include clause_start.html type="req" id="elinkaari/vaat-tonttijakosuunnitelman-voimaantulo" %}
Kun tonttijakosuunnitelman kumoutumisessa tallennetaan versio, jonka elinkaaritila-attribuutin arvo on Voimassa, tonttijakosuunnitelmatietovarasto päivittää niiden siinä kumoutuviksi asetettuja esitonttikohteita, joiden elinkaaritila-attribuutin arvo on Voimassa, attribuutteja seuraavasti luomatta niistä uusia versioita:

- ```voimassaoloAika```-attribuutin päättymisaika asetetaan samaksi kuin uuden tonttijakosuuunnitelman ```voimassaoloAika```-attribuutin alkamisaika.
- ```elinkaaritila```-attribuutin arvoksi asetetaan Kumottu.
- ```tallennusAika```-attribuutin arvoksi asetetaan ajanhetki, jolloin tonttijakosuunnitelma tallennettiin tonttijakosuunnitelmatietovarastoon elinkaaritilassa Voimassa.
{% include clause_end.html %}

Tonttijakosuunnitelman tietomalli ei sisällä omaa tietorakennettaan ajantasaiselle tonttijakosuunnitelma-aineistolle, joka sisältää annetun alueella tietyllä ajanhetkellä voimassaolevat esitonttikohteet, huomioiden kaavamuutosten ja vaihekaavojen vaikutukset niiltä osin kun ne ovat ko. ajanhetkellä voimassa. Tällainen toiminnallisuus on kuitenkin aivan ilmeisesti yhteisen tonttijakosuunnitelmatietovaraston palveluna erittäin hyödyllinen. Esitonttikohteiden ```voimassaoloAika```-attribuutin arvojen avulla tällainen ajantasainen “Esitonttimatto” voidaan laskea mille tahansa ajanhetkelle, olettaen, että kaikki kyseisen alueen tonttijakosuunnitelmat on viety tonttijakosuunnitelmatietovarastoon tonttijakosuunnitelman tietomallin mukaisessa muodossa.

### Asemakaavan suhde esitonttikohteeseen

Lisää sisäiset linkit
Voimassaolevan tonttijakosuunnitelman esitonttikohde voi saada uuden version tai kumoutua kokonaan kaavamuutoksen tai vaiheasemakaavan voimaan tullessa esitonttikohteen alueella.

{% include clause_start.html type="req" id="elinkaari/vaat-kaavatunnus" %}
Esitonttikohteille tulee yksilöidä tonttijakosuunnitelmassa siihen liittyvät hyväksytyt asemakaavat. Kutakin  esitonttikohdetta kohti tulee antaa yksi [Esitonttikohde-luokan](https://www.tonttijakosuunnitelma.fi/1.0-dev/looginenmalli/dokumentaatio/#esitonttikohde) attribuutin ```kaavatilannetieto``` arvo tyyppiä Kaavatilannetieto, jonka ```kaavaTunnus```-attribuutin arvo on [Kaava-luokan](https://kaavatietomalli.fi/1.0/looginenmalli/dokumentaatio/#kaava) ```viittaustunnus```.
{% include clause_end.html %}

{% include clause_start.html type="req" id="elinkaari/vaat-kaavalaji-vaikutus" %}
Asemakaavan muutoksen tai vaiheasemakaavan hyväksyminen esitonttikohteen alueella, edellyttää uuden tallennusversion luomista esitonttikohteesta ja [Kaavatilannetieto-luokan](https://www.tonttijakosuunnitelma.fi/1.0-dev/looginenmalli/dokumentaatio/#kaavansuhdetieto) ```kaavalaji```-attribuutin arvoksi tulee asettaa hyväksytyn kaavan kaavalaji-koodi.

Asemakaavan määräysten muuttuessa asetetaan kaavatietomallin uuden [Kaavamaarays-luokan](https://kaavatietomalli.fi/1.0/looginenmalli/dokumentaatio/#kaavamaarays) viittaustunnus tonttijakosuunnitelman tietomallin [Kaavamaarays-luokan](https://www.tonttijakosuunnitelma.fi/1.0-dev/looginenmalli/dokumentaatio/#kaavamaarays) ```liittyvanKaavamaarayksenTunnus```-attribuutin arvoksi. Lisäksi [Kaavamaarays-luokan](https://www.tonttijakosuunnitelma.fi/1.0-dev/looginenmalli/dokumentaatio/#kaavamaarays) viittaustunnus tallennetaan esitonttikohteen uudelle tallennusversiolle.<!-- Tällöin esitonttikohteen versiolla voi olla voimassa olevan asemakaavan ja luonnosvaiheessa olevan asemakaavan määräyksiä. Kun asemakaava tulee voimaan, tallennetaan esitonttikohteesta uusi tallennusversio, jolla vain uudet asemakaavan määräykset.

Asemakaavan määräysten muuttuessa tulee tulkita tonttijakosuunnitelman kaavan mukaisuus. Jos tonttijakosuunnitelma ei ole asemakaavan mukainen, tulee tonttijakosuunnitelman sisältämät ei kaavan mukaiset esitonttikohteet asettaa rakennuskieltoon, kun asemakaava hyväksytään. Kaavakohteen rajojen muutos  asettaa esitonttikohteen aina rakennuskieltoon:

- ```rakennuskielto```-attribuutin arvoksi asetetaan true.

Rakennuskiellon asettaminen true arvoksi edellyttää aina uuden tonttijakosuunnitelman laatimista niiltä osin, mitä esitonttikohteita rakennuskielto koskee.
{% include clause_end.html %}

{% include note.html content="Kaavan kaavalaji-koodia ei ole toistaiseksi olemassa. Elinkaarenhallinnan näkökulmasta merkittävimmät kaavalajit voisi olla: ensimmäinen asemakaava, asemakaavan määräysten muutos ja asemakaavan rajojen muutos. " %}

{% include clause_start.html type="req" id="elinkaari/vaat-kumoaa-esitonttikohteen" %}
Jos asemakaavalla esitontin rajat muuttuvat kokonaan tai osittain yleiseksi alueeksi, kumoaa asemakaava esitonttikohteen. Näin esitonttikohde muuttuu ei-kortteliksi, ja kumoaminen tonttijakosuunnitelmalla ei olisi mahdollista. [Kaavatilannetieto-luokan](https://www.tonttijakosuunnitelma.fi/1.0-dev/looginenmalli/dokumentaatio/#kaavansuhdetieto) kumoaa-attribuutin arvoksi asetetaan true. Esitonttikohteesta ei luoda uutta versiota, vaan:

- ```elinkaarentila```-attribuutin arvoksi asetetaan **kumoutunut**.
- ```voimassaoloAika```-attribuutin päättymisaika asetetaan samaksi kuin kaavan ```voimassaoloAika```-attribuutin alkamisaika.

Tämä edellyttää uuden tonttijakosuunnitelman laatimista kumotun esitonttikohteen alueelle.
{% include clause_end.html %}

## Tonttijakosuunnitelman elinkaaren vaiheet ja elinkaaritila-attribuutin käyttötavat

Tonttijakosuunnitelman ja sen sisältämien esitonttikohteiden elinkaareen liittyvää tilaa hallitaan ko. tietokohteiden elinkaaritila-attribuutin ja sen mahdolliset arvot kuvaavan Elinkaaren tila-koodiston avulla. Tonttijakosuunnitelma- ja  Esitonttikohde-luokkien elinkaaritila-attribuutit ovat pakollisia.

**Elinkaaren tila**-koodisto kuvaa 9 mahdollista tilaa, joissa tonttijakosuunnitelma voi olla sen elinkaaren eri vaiheissa:

- Vireillä
- Luonnos
- Ehdotus
- Hyväksytty
- Voimassa
- Kumottu osittain
- Kumottu kokonaan
- Kumoutunut osittain
- Kumoutunut kokonaan

{% include question.html content="Mitkä ovat Kumottu- ja Kumoutunut-tilojen tarkat määritelmät ja erot?" %}

Tonttijakosuunnitelmien, joiden elinkaaritila on Vireillä, Luonnos, Ehdotus, Hyväksytty laadinta- ja päätösprosessi on kesken, eli niiden esitonttikohteet eivät (vielä) ole lainvoimaisia. Tonttijakosuunnitelma, jotka ovat elinkaaritilassa Voimassa,  Kumottu osittain tai Kumoutunut osttain, sisältävät nykyajanhetkellä rajaamallaan alueella voimassa olevia esitonttikohteita. Koodit Kumottu kokonaan ja Kumoutunut kokonaan kuvaavat tonttijakosuunnitelman tiloja, joissa olevan tonttijakosuunnitelman elinkaari on päättynyt.

### Sallitut tonttijakosuunnitelman elinkaaren tilan muutokset

Tonttijakosuunnitelman elinkaaritila voi sen laadinta-, päätös-, valitus-, voimassaolo- ja kumoutumisvaiheidensa esiintyä ja muuttua vain tässä luvussa kuvatuilla tavoilla.

{% include clause_start.html type="req" id="elinkaari/vaat-ensimmainen-elinkaaritila" %}
Tonttijakosuunnitelman elinkaaritila tallennettaessa tonttijakosuunnitelmaa ensimmäistä kertaa tonttijakosuunnitelmatietovarastoon voi olla jokin seuraavista riippuen Tonttijakosuunnitelman ```digitaalinenAlkupera```-attribuutin arvosta:

- **Tietomallin mukaan laadittu**: tilat Vireillä, Luonnos, Ehdotus, Hyväksytty, Voimassa tonttijakosuunnitelma.
- **Kokonaan digitoitu**, **Osittain digitoitu** tai **Tonttijakosuunnitelman rajaus digitoitu**: tilat Voimassa, Kumottu osittain, Kumottu, Kumoutunut osittain, Kumoutunut
{% include clause_end.html %}

{% include clause_start.html type="req" id="elinkaari/vaat-elinkaaritila-siirtymat" %}
Tonttijakosuunnitelman ```elinkaaritila```-attribuutin arvo voi kahden sen peräkkäisen tallennusversion välillä vain seuraavilla tavoilla:

- Tilasta ```Vireillä``` tilaan ```Ehdotus```, ```Hyväksytty```.
- Tilasta ```Hyväksytty``` tilaan ```Voimassa```, ```Kumottu osittain```, ```Kumottu kokonaan```, ```Kumoutunut osittain``` tai ```Kumoutunut kokonaan```.
- Tilasta ```Voimassa``` tilaan ```Kumottu osittain```, ```Kumottu kokonaan```, ```Kumoutunut osittain``` tai ```Kumoutunut kokonaan```.
- Tilasta ```Kumottu``` ei ole sallittuja siirtymiä.
- Tilasta ```Kumoutunut``` ei ole sallittuja siirtymiä.
{% include clause_end.html %}

### Esitonttikohteen elinkaaren tila

Tavallisesti tonttijakosuunnitelman sisältämien esitonttikohteiden elinkaaritilan arvo on sama kuin koko tonttijakosuunnitelmalla, mutta ne voivat erota toisistaan kahdessa tapauksessa:

- Tonttijakosuunnitelman Kumottu osittain tai Kumoutunut osittain tapauksessa osa esitonttikohteista voidaan kumota
- Kaavamuutoksen tai vaihekaavan voimaantulo aiheuttaa siinä kumottaviksi esitonttikohteita

 (ks. Tonttijakosuunnitelman kumoutuminen ja kumoaminen)

### Tonttijakosuunnitelman elinkaaritilan muutoksiin liittyvät käsittely- ja vuorovaikutustapahtumat

 Kun tonttijakosuunnitelmasta viedään tonttijakosuunnitelmatietovarastoon uusi versio, jossa sen elinkaaritila on muuttunut, liittyy kyseisen tonttijakosuunniteman version syntymiseen tyypillisesti jokin käsittelytapahtuma.

{% include clause_start.html type="req" id="elinkaari/vaat-elinkaaritilan-muutostapahtumat" %}
Tonttijakosuunnitelman ```elinkaaritila```-attribuutin arvon seuraaviin muutoksiin tulee aina liittyä **Kasittelytapahtuma**, jonka ```laji```-attribuutin arvo tulee olla elinkaarimuutosta vastaava:

- Muutos tilaan **Vireillä**: Liityttävä käsittelytapahtuman laji Tonttijakosuunnitelman virelletulo.
- Muutos tilaan **Ehdotus**: Liityttävä käsittelytapahtuman laji Tonttijakosuunnitelman ehdotuksen nähtäville asettaminen.
- Muutos tilaan **Hyväksytty**: Liityttävä käsittelytapahtuman laji Tonttijakosuunnitelman hyväksyminen.
- Muutos tilaan **Voimassa**: Liityttävä käsittelytapahtuman laji Tonttijakosuunnitelman voimaantulo.
- Muutos tilaan **Kumoutunut osittain**: Liityttävä käsittelytapahtuman laji Tonttijakosuunnitelman kumoutuminen.
- Muutos tilaan **Kumoutunut kokonaan**: Liityttävä käsittelytapahtuman laji Tonttijakosuunnitelman kumoutuminen.
{% include clause_end.html %}

Yllä luetellut käsittelytapahtumat tulee tallentaa samaan aikaan elinkaaritilaltaan muuttuneen tonttijakosuunnitelman kanssa.

{% include clause_start.html type="req" id="elinkaari/vaat-ehdotuksen-nahtavilleasettaminen" %}
Tonttijakosuunnitelman ```elinkaaritila```-attribuutin arvon muuttuminen arvosta Ehdotus arvoon Hyväksytty vaatii, että tonttijakosuunnitelmatietovarastossa on sekä Kasittelytapahtuma lajia Ehdotuksen nähtäville asettaminen että Vuorovaikutustapahtuma lajia Nähtävilläolo, joista molemmat viittaavat johonkin ko. tonttijakosuunnitelman aiemmista Ehdotus-tilassa olevista versioista assosiaatiolla ```liittyvaAsia```. Vuorovaikutustapahtuman attribuutin ```tapahtumaAika``` tulee kuvata aikaväli, jonka aikana tonttijakosuunnitelman ehdotus on ollut nähtävillä.
{% include clause_end.html %}

{% include clause_start.html type="rec" id="elinkaari/suos-nahtavillaolopaikka" %}
Mikäli tonttijakosuunnitelman ehdotus on nähtävillä tietyssä fyysisessä paikassa, on suositeltavaa ilmaista kyseisen paikan sijainti Vuorovaikutustapahtuma-luokan attribuutin ```sijainti```-attribuutin avulla.
{% include clause_end.html %}

Huomaa, että muutos tilaan Kumottu osittain, Kumottu kokonaan, Kumoutunut osittain,  Kumoutunut kokonaan voi liittyvä joko käsittelytapahtuman lajiin Tonttijakosuunnitelman kumoaminen tai kaavan kumoamiseen kaavamuutokseen tai vaihekaavan lainvoimaiseksi tulon yhteydessä.

-->
