# TrueNAS NAS-projekti

Tämä repositorio dokumentoi NAS-Palvelin projektia. Projekti alkoi tarpeesta jakaa opiskelussa ja omissa harjoituksissa käytettäviä tiedostoja yhteisesti. Siitä on ajansaatossa tullut oppimisympäristö, jossa harjottelemme tallennusratkaisuja, palveluiden ylläpitoa, etäyhteyksiä, valvontaa ja paikallisen tekoälyn käyttöä.

Dokumentaation tarkoitus on kuvata, mitä palvelimella tehdään, mikä on jo toteutettu ja mitkä asiat ovat vielä työn alla. Toteutuksia kehitetään sitä mukaa, kun testaamme niiden toimivuutta ja opitaan lisää.

## Sisältö

- [Projektin tavoitteet](#projektin-tavoitteet)
- [Nykyinen kokoonpano](#nykyinen-kokoonpano)
- [Miten projekti eteni](#miten-projekti-eteni)
- [Palvelut ja niiden tila](#palvelut-ja-niiden-tila)
- [Paikallinen tekoäly ja RAG](#paikallinen-tekoäly-ja-rag)
- [Etäkäyttö, valvonta ja tietoturva](#etäkäyttö-valvonta-ja-tietoturva)
- [Seuraavat kehitysvaiheet](#seuraavat-kehitysvaiheet)
- [Dokumentaation ylläpito](#dokumentaation-ylläpito)

## Projektin tavoitteet

NAS (Network Attached Storage) toimii yhteisenä tiedostojen tallennus- ja jakopaikkana sekä alustana omille palveluille. Alkuperäinen käyttötarve oli SMB-verkkolevy, jonka kautta voimme käyttää opiskeluun liittyviä työkaluja, ohjelmia, skriptejä ja muuta projektiaineistoa. Palvelimella kokeilemme myös, miten useita sovelluksia voidaan ajaa, seurata ja ylläpitää samassa ympäristössä.

Projektin tärkeimmät osaamistavoitteet ovat:

- ottaa käyttöön ja ylläpitää TrueNAS SCALE -palvelinta;
- hallita tiedostojakoja, sovelluksia ja niiden tarvitsemia tallennustiloja;
- järjestää etäkäyttö ja valvoa palveluiden saatavuutta;
- käyttää paikallista kielimallia ja kehittää sen käyttöä oman aineiston kanssa;
- dokumentoida muutokset, ongelmat ja ratkaisut niin, että ympäristö on myöhemmin helpompi ymmärtää ja ylläpitää.

Kyseessä on siis oppimisprojekti: palveluiden kokoonpano ja käyttötavat voivat muuttua testauksen perusteella.

## Nykyinen kokoonpano

Projektidokumentin mukaan käytössä oleva laitteisto on seuraava:

| Osa | Kokoonpano |
| --- | --- |
| Emolevy | ASUS P8H61M PRO |
| Prosessori | Intel Core i5-4690K |
| Keskusmuisti | 16 Gt DDR3 |
| Näytönohjain | ASUS Turbo GeForce GTX 1060, 6 Gt |
| Käyttöjärjestelmä | TrueNAS SCALE |

Palvelin rakennettiin aluksi vanhan Fujitsu Esprimo pöytäkoneen ympärille. Kokoonpanoa päivitettiin myöhemmin mm. kotelon, virtalähteen ja näytönohjaimen osalta. Taulukko kuvaa päivitettyä laitteistoa.

Näytönohjaimen lisääminen liittyi erityisesti paikallisen kielimallin suorituskyvyn päivittämiseen. Projektin omassa yksinkertaisessa kokeilussa vastausaika lyheni noin 33 sekunnista noin 2,4 sekuntiin näytönohjaimen käyttöönoton jälkeen. Lukemat kuvaavat kyseistä kokeilua, eikä yleistä suorituskykyä.

## Miten projekti eteni

1. **Yhteinen tiedostojako.** Rakennettiin ensin TrueNAS-palvelimelle SMB-jaon, jotta projektin tiedostot ja työkalut olisivat saatavilla samasta paikasta.
2. **Etäkäyttö.** Otimme käyttöön Tailscalen, jotta palvelinta ja sen palveluita voidaan käyttää myös paikallisverkon ulkopuolelta hallitun verkkoyhteyden kautta.
3. **Valvonta ja sovellukset.** Lisäsimme palveluiden saatavuuden seurantaa. Kokeiltiin erilaisia itse ylläpidettäviä sovelluksia, kuten mediasovellusta ja järjestelmän valvontaa.
4. **Paikallinen tekoäly.** Asensimme Ollaman kielimallien ajamiseen ja yhdistettiin se Odysseus-verkkokäyttöliittymään.
5. **Laitteistopäivitys.** Päivitimme palvelimen kokoonpanoa ja lisäsimme GTX 1060 -näytönohjaimen nopeuttamaan tekoälyyn liittyviä tehtäviä ja prosesseja.
6. **Omaan aineistoon perustuvat vastaukset.** Aloitimme RAG-menetelmän ja aineiston rakenteen kokeilun, jotta paikallinen tekoäly voisi hyödyntää omia dokumenttejamme.

## Palvelut ja niiden tila

Alla olevat tilat perustuvat tähän README-tiedostoon käytettyyn projektidokumenttiin. **Toiminnassa** tarkoittaa, että palvelu on saatu käyttöön; se ei yksinomaan kerro kaikkien toimintojen olevan valmiita. **Kesken** tarkoittaa, että palvelua tai sen suunniteltua käyttötapaa kehitetään edelleen.

| Palvelu | Tarkoitus | Dokumentoitu tila |
| --- | --- | --- |
| SMB-tiedostojako | Yhteiset tiedostot, työkalut ja projektiaineisto | Toteutettu |
| Tailscale | Etäyhteys palvelinympäristöön | Toiminnassa |
| Uptime Kuma | Palveluiden saatavuuden seuranta ja hälytykset | Toiminnassa |
| Netdata | Palvelimen tilan ja suorituskyvyn seuranta | Toiminnassa |
| Ollama | Paikallisten kielimallien ajaminen | Toiminnassa |
| Odysseus | Kielimallin verkkokäyttöliittymä | Toiminnassa |
| Jellyfin | Oman mediakirjaston hallinta ja toisto | Käyttöönotto kesken |
| Filebrowser Quantum | Tiedostojen käyttö verkkoselaimella | Kesken |
| Kerberos-agent | Kameravalvontakokeilu Opticam i5 -projektissa | Kesken |

Uptime Kumaan on projektin aikana kokeiltu Telegram-ilmoituksia, jotta palvelimen tilasta saataisiin tieto. Jellyfinin osalta kehitystyöhön kuuluu mediakirjaston ja käyttöoikeuksien määrittely; palvelussa käytettävän sisällön tulee olla sellaista johon meillä on tarvittavat oikeudet.

## Paikallinen tekoäly ja RAG

Paikallisen tekoälyn tavoitteena on ajaa kielimallia palvelimella ja käyttää sitä esimerkiksi oppimiseen sekä projektityöhön itsessään. **Ollama** huolehtii mallin ajamisesta, ja **Odysseus** tarjoaa sitä varten selaimessa toimivan käyttöliittymän. Näytönohjaimen käyttöönotto paransi tämän kokonaisuuden käytettävyyttä projektin omissa kokeiluissa.

Kehitämme parhaillaan **RAG-ratkaisua** (Retrieval-Augmented Generation). Siinä järjestelmä etsii kysymyksen kannalta olennaista tietoa erillisestä aineistosta ja antaa sen kielimallille vastauksen tueksi. Tarkoituksena on, että malli voi hyödyntää esimerkiksi NAS-projektin dokumentaatiota sekä myöhemmin muita järjestettyjä oppimisaineistoja.

RAG-työssä keskitymme tällä hetkellä aineiston kokoamiseen, aiheiden erotteluun ja siihen, että löydetty tieto vaikuttaisi vastauksiin. Pelkkä aineiston indeksointi ei osoita, että vastaukset ovat oikeita tai että malli käyttäisi lähteitä johdonmukaisesti. Tämä osa projektista on siis edelleen kehitysvaiheessa.

## Etäkäyttö, valvonta ja tietoturva

Etäyhteydet helpottavat palvelimen ylläpitoa ja valvontapalvelut auttavat havaitsemaan häiriöitä. Projektissa käytämme Tailscalea etäkäyttöön sekä Uptime Kumaa ja Netdataa saatavuuden ja järjestelmän tilan seuraamiseen. Näitä palveluita kehitämme mahdollisten tarpeiden perusteilla.

Ympäristöä käytetään opiskeluun ja järjestelmähallinnan harjoitteluun. Olemme siis kiinnittänyt huomiota käyttöoikeuksiin, palveluiden asetuksiin ja siihen mitä tietoja julkaistaan. Tämä julkinen dokumentaatio kuvaa kokonaisuuden ja opitut asiat; salasanat, API-avaimet, yksityiset osoitteet ja muut arkaluonteiset asetukset eivät siis kuulu repositorioon.

## Seuraavat kehitysvaiheet

Seuraavat asiat ovat tavoitteita tai suunnitelmia, EI valmiiksi toteutettuja ominaisuuksia:

- **RAG-aineiston kehittäminen:** jäsennetään lähdemateriaalin selkeisiin aiheisiin ja arvioidaan, miten hyvin sitä hyödynnetään vastauksissa.
- **Palveluiden viimeistely:** jatkamme keskeneräisten sovellusten, kuten Jellyfinin ja Filebrowser Quantumin, asetusten ja käyttötapojen selvittämistä.
- **Etäkonsoli:** tutkimme KVM-ratkaisua, joka mahdollistaisi koneen näytön ja ohjauksen etänä myös silloin kun käyttöjärjestelmän tavanomainen etäyhteys ei ole käytettävissä.
- **Cyberdeck:** suunnittelemme kannettavaa laiteprojektia jonka tarkempi toteutus määritellään myöhemmin.
- **Uudet itse ylläpidettävät palvelut:** arvioimme esimerkiksi viestintäpalvelun kokeilua sen mukaan mitä projekti ja käytettävissä oleva laitteisto mahdollistavat.
- **Dokumentaation täydentäminen:** lisäämme tarkempia kuvauksia kokoonpanosta, palveluiden käyttöönotosta, muutoksista ja ratkaistuista ongelmista.

## Dokumentaation ylläpito

Pidämme tässä etusivussa yleiskuvan projektista. Kun jokin ratkaisu muuttuu, päivittelemme sen tilan tänne ja erottelemme aiemmat kokeilut nykyisestä kokoonpanosta. Yksityiskohtaisille ohjeille ja kuvalliselle dokumentaatiolle voidaan myöhemmin luoda omat sivut.

Projektin tekijät: **Eetu Ala-Kortesniemi ja Jesse Korhonen** (`badopsec.local`).
