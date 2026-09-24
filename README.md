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



# TrueNAS NAS Project

This repository documents our NAS server project. It began with a need to share files used in our studies and personal projects. Over time, it has grown into a learning environment where we practise storage solutions, service administration, remote access, monitoring, and the use of local AI.

This documentation explains what we use the server for, what we have already built, and what is still in progress. We improve the setup as we test what works and learn more.

## Contents

- [Project goals](#project-goals)
- [Current hardware](#current-hardware)
- [How the project evolved](#how-the-project-evolved)
- [Services and their status](#services-and-their-status)
- [Local AI and RAG](#local-ai-and-rag)
- [Remote access, monitoring, and security](#remote-access-monitoring-and-security)
- [Next steps](#next-steps)
- [Maintaining the documentation](#maintaining-the-documentation)

## Project goals

The NAS (Network Attached Storage) serves as a shared place to store and access files, as well as a platform for our own services. Our original goal was to set up an SMB network share for tools, software, scripts, and other project materials related to our studies. We also use the server to learn how to run, monitor, and maintain multiple applications in one environment.

Our main learning goals are to:

- set up and maintain a TrueNAS SCALE server;
- manage file shares, applications, and their storage;
- arrange remote access and monitor service availability;
- run a local language model and develop ways to use it with our own material;
- document changes, problems, and solutions so the environment is easier to understand and maintain later.

This is a learning project, so the services and how we use them may change as we test things.

## Current hardware

According to the project documentation, the current setup is:

| Component | Configuration |
| --- | --- |
| Motherboard | ASUS P8H61M PRO |
| CPU | Intel Core i5-4690K |
| RAM | 16 GB DDR3 |
| GPU | ASUS Turbo GeForce GTX 1060, 6 GB |
| Operating system | TrueNAS SCALE |

The server was originally built around an old Fujitsu Esprimo desktop. We later upgraded the setup, including the case, power supply, and graphics card. The table shows the upgraded hardware.

We added the GPU mainly to improve the performance of the local language model. In one simple test of our setup, response time dropped from about 33 seconds to about 2.4 seconds after enabling the GPU. These figures describe that particular test, not the server's performance in general.

## How the project evolved

1. **Shared files.** We first set up an SMB share on the TrueNAS server so our project files and tools could be accessed from one place.
2. **Remote access.** We added Tailscale so we could access the server and its services from outside the local network through a controlled connection.
3. **Monitoring and applications.** We added service availability monitoring and tried various self-hosted applications, including media and system monitoring tools.
4. **Local AI.** We installed Ollama to run language models and connected it to the Odysseus web interface.
5. **Hardware upgrade.** We upgraded the server and added a GTX 1060 to speed up AI-related tasks and processes.
6. **Answers based on our own material.** We began experimenting with RAG and organising our material so the local AI could use our documentation.

## Services and their status

The statuses below are based on the project documentation used to prepare this README. **Running** means we have got the service up and running; it does not mean every feature is finished. **In progress** means we are still working on the service or how we plan to use it.

| Service | Purpose | Documented status |
| --- | --- | --- |
| SMB file share | Shared files, tools, and project materials | Implemented |
| Tailscale | Remote access to the server environment | Running |
| Uptime Kuma | Service availability monitoring and alerts | Running |
| Netdata | Server health and performance monitoring | Running |
| Ollama | Running local language models | Running |
| Odysseus | Web interface for the language model | Running |
| Jellyfin | Managing and playing our media library | Setup in progress |
| Filebrowser Quantum | Accessing files through a web browser | In progress |
| Kerberos-agent | Camera monitoring experiment for the Opticam i5 project | In progress |

We have tested Telegram notifications in Uptime Kuma to receive updates about the server's status. For Jellyfin, we are still defining the media library and access permissions. We only use content for which we have the necessary rights.

## Local AI and RAG

Our goal with local AI is to run a language model on the server and use it for learning and for the project itself. **Ollama** runs the model, while **Odysseus** provides a browser-based interface. Enabling the GPU made this setup more practical in our own tests.

We are currently developing a **RAG setup** (Retrieval-Augmented Generation). With RAG, the system searches a separate collection of material for information relevant to a question and gives that information to the language model to support its answer. The aim is for the model to use our NAS project documentation and, later, other organised learning materials.

Right now, we are focusing on collecting material, organising it by topic, and making sure the retrieved information actually affects the answers. Indexing the material alone does not prove that the answers are correct or that the model uses the sources consistently. This part of the project is still in development.

## Remote access, monitoring, and security

Remote access makes it easier to maintain the server, while monitoring helps us spot problems. We use Tailscale for remote access and Uptime Kuma and Netdata to track availability and system health. We continue to develop these services as our needs change.

We use this environment for studying and practising system administration, so we pay attention to access permissions, service settings, and what information we publish. This public documentation describes the setup and what we have learned. Passwords, API keys, private addresses, and other sensitive settings do not belong in the repository.

## Next steps

The following are goals or plans, **not features we have already completed**:

- **Improve the RAG material:** organise sources into clear topics and evaluate how well the model uses them in its answers.
- **Finish setting up services:** continue working out the settings and intended use of applications such as Jellyfin and Filebrowser Quantum.
- **Remote console:** investigate a KVM solution that would let us see and control the machine remotely even when the operating system's usual remote access is unavailable.
- **Cyberdeck:** plan a portable device project; we will decide on the details later.
- **More self-hosted services:** consider testing a communication service, depending on what the project and available hardware allow.
- **Expand the documentation:** add more detailed descriptions of the hardware, service setup, changes, and problems we have solved.

## Maintaining the documentation

This front page gives an overview of the project. When something changes, we update its status here and distinguish earlier experiments from the current setup. We may create separate pages later for detailed instructions and documentation with images.

Project members: **Eetu Ala-Kortesniemi and Jesse Korhonen** (`badopsec.local`).

