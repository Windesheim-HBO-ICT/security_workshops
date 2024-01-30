# Workshop ZAP

## Voorwaarden deelname

Geen

## Beschrijving

ZAP (Zed Attack Proxy) is een penetration security testing tool. Penetration testing (pentesting) simuleert een hacker die probeert data te stelen, of een vorm van Denial Of Service (DOS) uit te voeren. ZAP is een man-in-the-middle proxy en komt tussen de browser en de server. ZAP kan op deze wijze requests bekijken, aanpassen en weer doorsturen.

In een aantal opdrachten gaan we je eigen applicatie in kaart brengen en aanvallen. Hiervan genereren we een rapport, die je in je eigen portfolio kan verwerken.

## Eindresultaat

Na het afronden van de workshop beschik je over het volgende eindresultaat:

- ⚡ Kennis van het werken van ZAP
- 🗺️ Je website in kaart gebracht met verschillende spiders
- 🔥 Een attack uitgevoerd op je eigen webapplicatie
- ✍️ Een request aangepast en doorgestuurd naar de webserver
- 🔍 Resultaten bekeken, een rapport gegenereerd en deze verwerkt in je portfolio

## Notes

- ZAP simuleert een echte aanval, gebruik ZAP niet op andere URLs dan waar je eigenaar van bent of expliciete toestemming voor hebt. Ook niet op google.com of andere publieke websites.
- In de instructies wordt verwezen naar <http://localhost:XXXX>. Als je je website al op skylab hebt gedeployed, kun je hier ook de daadwerkelijke URL van je applicatie gebruiken.

## Opdracht 1: 🗃️Setup

Voordat we kunnen beginnen met pentesting, moeten we ZAP en de benodigde software installeren. Volg de onderstaande stappen:

**Stap 1:** ZAP maakt gebruik van JAVA, als dit nog niet op je computer staat kun je dit [hier downloaden](https://www.oracle.com/java/technologies/downloads/). _Let op: Zap vereist minimaal JAVA versie 11._ Op het moment van schrijven is JDK 21 de nieuwste lts-versie, deze wordt aangeraden om te gebruiken.

**Stap 2:** Download ZAP via [deze link](https://www.zaproxy.org/download/).

**Stap 3:** Volg de instructies in de setup.

**Stap 4:** Start ZAP.

**Stap 5:** Selecteer _Yes, I want to persist this session but I want to specify the name and location_ en klik op start.

**Stap 6:** Geef een herkenbare naam en druk op save. Op deze manier word je sessie opgeslagen en kun je later verder met deze sessie.

_Als je alle stappen correct hebt doorlopen, zie je het volgende: ![ZAP home page](https://github.com/Windesheim-HBO-ICT/security_workshops/assets/62651445/b2d1e0a6-8b7d-4d04-b8d4-1fc53e08b5fd)_ De ZAP UI bestaat uit de volgende onderdelen:
1. **Menu Bar** – Provides access to many of the automated and manual tools.
2. **Toolbar** – Includes buttons which provide easy access to most commonly used features.
3. **Tree Window** – Displays the Sites tree and the Scripts tree.
4. **Workspace Window** – Displays requests, responses, and scripts and allows you to edit them.
5. **Information Window** – Displays details of the automated and manual tools.
6. **Footer** – Displays a summary of the alerts found and the status of the main automated tools.

**✔️ opdracht 1 is klaar!**

## Opdracht 2: 🕷 Spider

We gaan starten met het in kaart brengen van je website, dit gaan we doen met een spider. Dit is een tool die automatisch nieuwe resources (URLs) ontdekt. De spider begint met een lijst aan URLs om te bezoeken en gaat van daaruit nieuwe hyperlinks opzoeken en voegt deze toe aan de lijst. Hij blijft doorgaan tot alle URLs in de lijst bezocht zijn.

### Opstarten Spider

**Stap 1:** Launch je eigen webapplicatie lokaal. Onthoud of noteer de URL (Bijvoorbeeld: <https://localhost:7095/>).

**Stap 2:** In ZAP, klik onderaan in de Information window (5) op de groene plus.

**Stap 3:** Selecteer _🕷 Spider_.

**Stap 4:** Klik op _🕷 New Scan_.

### Instellen scope

Om ervoor te zorgen dat de spider alleen op jouw webapplicatie blijft, moet eerst de scope ingesteld worden. Dit voorkomt dat ZAP andere websites scant of aanvalt.

**Stap 5:** In het veld _Starting point_ vul je de URL van je eigen applicatie in die je bij stap 1 hebt genoteerd. **⚠️Let op: Gebruik ZAP alleen op applicaties waar je de eigenaar van bent, of waar je toestemming voor hebt. ZAP simuleert een echte aanval en kan echte schade aanrichten aan websites. ⚠️**

**Stap 6:** De context kan leeg blijven, dan wordt de standaard context gebruikt. De andere opties kunnen blijven zoals ze zijn.

_In de volgende opdracht gaan we de default context aanpassen met een gebruiker. Voor nu laten we wat het is._

**Stap 7:** Klik op _Start Scan_.

### Resultaten spiderscan

De lijst met URLs wordt nu gevuld. Bij elke URL staat de volgende informatie:

- **Processed** - Of the URL was verwerkt door de spider of was overgeslagen. (Bijvoorbeeld buiten de scope)
- **Method** - De gebruikte HTTP methode, bijvoorbeeld **GET** of **POST**.
- **URL** - De gevonden resource.
- **Flags** - Extra informatie over de URL.

**Stap 8:** Aan de zijkant, in de tree window(3), staat het tabje 🌍_Sites_. Als je de folder met URL van je webapplicatie uiteenklapt, zie je een folder structuur. Komt deze structuur (gedeeltelijk) overeen met de folderstructuur in je editor? Mis je nog een aantal folders/resources? Zie je bestanden die je er niet tussen wilt zien? Denk aan admin pagina's, pagina's die je alleen mag zien als je ingelogd bent of andere resources. Zie je onverwachte folders of items? Noteer deze dan.

**Stap 9:** In de information window(5) onderaan staat het tabje 🚩_Alerts_. In dit tabje kun je zien welke security issues de spiderscan heeft gevonden. Bekijk de alerts, kies een aantal uit die je wil gaan oplossen.

**✔️ Opdracht 2 is klaar!**

## Opdracht 3: 🕷️ Ajax spider

De Ajax spider gebruikt een andere methode dan de normale spider om URLs te vinden. Deze spider is bedoeld voor sites die veel gebruik maken van AJAX (Asynchronous JavaScript and XML [Wikipedia](https://en.wikipedia.org/wiki/Ajax_(programming))). Omdat deze spider een andere methode gebruikt, kan deze ook andere URLs vinden. Het starten van de Ajax spider is vergelijkbaar met de normale spider.

### Opstarten Spider

**Stap 1:** Launch je eigen webapplicatie lokaal. Onthoud of noteer de URL (Bijvoorbeeld: <https://localhost:7095/>).

**Stap 2:** In ZAP, klik onderaan in de information window(5) op de groene plus.

**Stap 3:** Selecteer _🕷 Ajax spider_.

**Stap 4:** Klik op _🕷 New Scan_.

**Stap 5:** In het veld _Starting point_ vul je de URL van je eigen applicatie in die je bij stap 1 hebt genoteerd. **⚠️Let op: Gebruik ZAP alleen op applicaties waar je de eigenaar van bent, of waar je toestemming voor hebt. ZAP simuleert een echte aanval en kan echte schade aanrichten aan websites. ⚠️**

**Stap 6:** De context kan leeg blijven, dan wordt de standaard context gebruikt.

**Stap 7:** Zorg ervoor dat je bij het selecteren van een browser een _Headless_ variant kiest. Anders worden er tientallen instanties van je browser geopend. Je kunt hierbij kieze uit Chrome Headless of Firefox headless, afhankelijk van welke je geïnstalleerd hebt.

**Stap 8:** Klik op _Start Scan_. De AJAX spider kan langer duren dan de normale spider.

### Resultaten spiderscan

De lijst met URLs wordt nu gevuld. Bij elke URL staat de volgende informatie:

- **Processed** - Of the URL was verwerkt door de spider of was overgeslagen. (Bijvoorbeeld buiten de scope)
- **Method** - De gebruikte HTTP methode, bijvoorbeeld **GET** of **POST**.
- **URL** - De gevonden resource.
- **Size Resp. Header en Size Resp. Body** - De grootte van de response header en body.

Je folder structuur is nu groter geworden, je ziet meer pagina's en andere resources in het 🌍_Sites_ tabje.
We hebben nu je webapplicatie in kaart gebracht.

**✔️ opdracht 3 is klaar!**

## Opdracht 4: 🔥Active Scan

We hebben nu aan de hand van spiders je webapplicatie in kaart gebracht. Nu is het tijd om de gevonden pagina's aan te vallen.

**⚠️Let op: De volgende stappen kunnen schade toebrengen aan je applicatie en database. Het kan zijn dat je data uit je database verliest. Als er data in je database zit, die er niet via seeding in is gekomen, zorg er dan voor dat je een kopie van je database hebt.⚠️**

De active scan probeert verschillende bekende aanvallen tegen de geselecteerde doelen. Je kunt zelf instellen welke aanvallen extra vaak uitgevoerd worden en welke waarden deze krijgen. Standaard zijn deze instellingen goede genoeg voor het uitvoeren van de active scan.

**Stap 1:** In het 🌍_Sites_ tabje, klik met je rechtermuis op de 📄_GET:/_ pagina en selecteer _Attack_ --> 🔥_Active scan_.

**Stap 2:** Klik op _Start Scan_.

Er wordt nu een scan uitgevoerd op de pagina's die gevonden zijn met de spiders.

**Stap 3:** Omdat deze scan iets langer kan duren, voornamelijk voor grote websites, is het mogelijk om specifiekere voortgang in te zien. In het 🔥_Active Scan_ tabje dat nu is geopend, klik op het 📟_Progress details_ icoontje naast de ⏸️_Pauze_ en ⏹️_Stop_ knop.

In het venster dat nu geopend wordt, zie je welke attacks uitgevoerd worden en hoever de attacks zijn. Hier wordt getoond hoeveel requests voor die attack zijn uitgevoerd en hoeveel van deze requests een alert opleveren.

**✔️ opdracht 4 is klaar!**

## Opdracht 5: 👤Active scan met gebruikers-rechten

We hebben nu een scan uitgevoerd vanuit het perspectief van en niet-ingelogde gebruiker. Je hebt in je eigen applicatie aan de hand van Identity (of op een andere manier) authenticatie en authorizatie geïmplementeerd. ZAP kan ook werken vanuit een ingelogde gebruiker. We gaan nu een scan uitvoeren vanuit een standaard ingelogde gebruiker.

Een context is een manier om URLs die bij elkaar horen te groeperen. Het is aanbevolen om voor elke webapplicatie die in je systeem bestaat een aparte context te geven. In het geval van je eigen applicatie is dit er maar 1, daarom gebruiken we de default context. Om aan de default context een gebruiker toe te voegen, moet eerst een URL aan de context toegevoegd worden.

**Stap 1:** In het 🌍_Sites_ tabje, klik met je rechtermuis op de 📂_<https://localhost:XXXX>_ folder en selecteer _Include in context_ --> _Default context_.

**Stap 2:** Bovenin het 🌍_Sites_ tabje staat de context, dubbelklik op de default context om de default context in de session properties te wijzigen.

Onder het tabje _Context_ --> _1: Default context_ --> _1:Include in context_ kun je zien dat de URL die we in stap 4 hebben toegevoegd in de include lijst staat.

Om een gebruiker toe te voegen, geven we ZAP instructies om in te loggen. We gaan aangeven waar de inlogpagina te vinden is, welke gegevens verstuurd moeten worden om in te loggen en hoe ZAP kan weten dat er ingelogd is.

**Stap 3:** Ga naar _Context_ --> _1: Default context_ --> _1: Authentication_.

**Stap 4:** Verander de authentication method naar form-based authentication.

**Stap 5:** In de _Login Form Target URL_, klik op 🌍_Select_. Selecteer de loginpagina POST request.  
Deze staat standaard onder 📂_<https://localhost:XXXX>_ --> 📂_Identity_ --> 📂_Account_ --> 📄_POST:Login()(Input.Pass...)_.

**Stap 6:** Veel velden worden automatisch ingevuld, het is wel belangrijk om deze te controleren.

- URL to GET login page: De url die je gebruikt om bij de inlogpagina te komen. Bij Identity: _<https://localhost:XXXX/Identity/Account/Login>_
- Login Request POST Data: De data die meegegeven word in de POST voor het inloggen.
- Username parameter: Het veld waarin je de username meegeeft (Bij Identity: Input.Username).
- Password parameter: Het veld waarin je het wachtwoord meegeeft (Bij Identity: Input.Password).

Om ZAP te laten weten of de huidige pagina een ingelogde pagina is, moeten we een kenmerk van een ingelogde pagina meegeven. Dit is vaak een uitlogknop of een welkomstbericht. Voor een uitgelogde pagina is een kenmerk vaak een inlog-knop. We gaan nu handmatig in de applicatie inloggen, zodat we de inlogrequest en response in de history terug kunnen vinden.

**Stap 7:** Sluit het venster met de OK knop. In het quick start venster klik je op manual explore en vul je de URL van je applicatie in.
Zet _Enable HUD_\* uit. Selecteer je browser en klik op _Launch Browser_. Log nu in met een gebruiker van je applicatie. Je kunt nu de geopende broser weer wegklikken.

\*_De HUD is een meer handmatige manier om je applicatie te ontdekken/aan te vallen. Er zitten ook functies in die niet in deze workshop worden behandeld. Als je dit interessant vind, kun je later de HUD aanzetten en de HUD-tutorial volgen._

**Stap 8:** In het 📆_History_ tabje vind je de requests die je zojuist gemaakt hebt. Meer info over de request en response, kun je in de ➡️_Request_ en ⬅️_Response_ tabjes vinden. Open het response tabje en klik op verschillende requests om de response te vinden die de HTML voor je ingelogde pagina toont.

**Stap 9:** In de response body, zoek naar de uitlogknop HTML tag (Bijvoorbeeld:

```HTML
<button id="logout" type="submit">Logout</button>
```

) en selecteer deze. Klik dan met je rechtermuisknop en _Flas as Context_ --> _Default Context: Authentication Logged-in indicator_ en klik op OK.

Je hebt nu aangegeven dat je op een ingelogde pagina bent, omdat er een uitlogknop op de pagina staat.

**Stap 10:** Doe nu hetzelfde, maar zoek nu in de 📆_History_ een response van een niet-ingelogde pagina. Selecteer hierin de inlogknop en markeer deze als _Logged-out indicator_.

Je hebt nu voor ZAP aangegeven hoe je kunt inloggen, nu gaan we een gebruiker aanmaken.

**Stap 11:** In de session properties (dubbelklik op de default context bovenin het 🌍_Sites_ tabje), klik in het tabje _Users_ op Add. Geef je gebruiker een herkenbare naam en inloggegevens. Dit kan zijn van een bestaande gebruiker, of een gebruiker die je hier speciaal voor aanmaakt. Zorg er in ieder geval voor dat de gebruiker in je applicatie bestaat. Klik op OK om te bevestigen.

We hebben nu een gebruiker aangemaakt. Laten we paginas in kaart brengen die we alleen als ingelogde gebruiker kunnen bezoeken.

**Stap 12:** Ga terug naar het 🕷_Spider_ tabje en volg de instucties zoals die zijn gegeven bij opdracht 1. Bij de context selecteer je de default context, bij de user selecteer je de zojuist aangemaakte gebruiker. Start de scan.

**Stap 13:** Doe hetzelfde voor de 🕷️_Ajax Spider_.

We hebben nu de applicatie als ingelogde gebruiker in kaart gebracht, nu kunnen we een groter deel van de website aanvallen.

**Stap 14:** Start een active scan en zorg ervoor dat de correcte context en user geselecteerd zijn.

**✔️ opdracht 5 is klaar!**

## Opdracht 6: ✍️Request wijzigen

We gaan een eerder gemaakt request wijzigen en kijken of we hiermee je webapplicatie kapot kunnen maken.

**Stap 1:** In het _Quick Start_ tabje (Workspace window(4)), klik op manual explore. vul de url van je applicatie in (<http://localhost:XXXX>), zet _Enable HUD_ **uit** en launch in browser naar keuze.

**Stap 2:** Navigeer naar je inlog-pagina.

**Stap 3:** We moeten ervoor zorgen dat ZAP alle requests onderschept. Om dit te doen klik je op 🟢 _Set Break on All Requests and Responses_ in de toolbar (2). 🟢 verandert naar 🔴.

**Stap 4:** Log in met een incorrect wachtwoord.

Als het goed is, wordt je request onderschept en zal de applicatie bevriezen. Je kunt het onderschepte request vinden in het ❌ _break_ tabje in de workspace window (4).

**Stap 5:** We gaan het request wijzigen. Haal bijvoorbeeld het Input.UserName veld weg en klik op ▶️_Submit and Continue to Next Breakpoint_. Vangt je applicatie dit af?

**Stap 6:** Zet de 🟢 _break all_ weer aan en log nog een keer in, dit keer met correcte inloggegevens. Pas het _\_\_RequestVerificationToken_ aan. Kun je nu nog succesvol inloggen?

**Stap 7:** Probeer andere gegevens in de request te veranderen. Kun je iemand doorsturen naar een andere pagina? Kun je inloggen op een ander account? Kun je een SQL injectie uitvoeren?

**✔️ opdracht 6 is klaar!**

## Opdracht 7: 🔍Analyseren resultaten

Om in te zien of je applicatie veiliger is geworden, gaan we nu een rapport genereren en later in het project nog een scan uitvoeren en daar ook een rapport van genereren. In je portfolio kun je deze resultaten vergelijken en aantonen welke verbeteringen je hebt uitgevoerd.

We gaan eerst een nulmeting vastleggen.

**Stap 1:** Klik in de menubar (1) op _Report_ --> _Generate report_

**Stap 2:** In de context, selecteer alleen je eigen applicatie (<http://localhost:XXXX>).

**Stap 3:** In het _Template_ tabje, selecteer een template. Je kunt er hier zelf een van kiezen. Aanraders zijn:

- High level Report Sample. --> Handig voor makkelijk vergelijken van grafieken en een makkelijk tabelformaat om te kopieëren. Ook veel verwijzingen naar documentatie/uitleg over het veiligheidsrisico.
- Modern HTML Report with themes and options. --> Veel informatie en voorbeelden.
- Traditional Markdown Report. --> Makkelijk te lezen als plaintext.

**Stap 4:** Klik op _Generate Report_.

**Stap 5:** Sla het rapport op en zorg ervoor dat je deze later weer kunt bekijken.

**Stap 6:** Zorg ervoor dat je ook je sessie opslaat. Deze zou je later weer kunnen gebruiken.

**✔️ opdracht 7 is klaar!**

## Opdracht 8: ⚒️ Fixen

Deze opdracht doe je vanzelf in de volgende workshops en je eigen tijd.

**Stap 1:** Bekijk het rapport en bedenk welke items je wilt aanpakken/verbeteren.

Tip: Begin met de items die het meeste risico (_Risk_) vormen en de hoogste zekerheid (_Confidence_) hebben. Deze zijn handig in te zien in de Risk and Confidence HTML template.

**Stap 2:** Bekijk de documentatie van deze security-risicos en zoek op het internet hoe je deze zou kunnen oplossen. Los de risicos in je applicatie op.

Er is geen vast aantal dat je moet oplossen, het gaat erom dat je kunt aantonen dat je voldoende met de veiligheid van je webapplicatie bezig bent geweest.

**Stap 3:** Ben je verdergekomen met je applicatie en heb je een aantal veiligheidsrisicos opgelost? Voer nog een keer de spiders en een active scan uit. Genereer weer een rapport.

**Stap 4:** Vergelijk je rapporten en noteer de verschillen in je portfolio. Laat zien wat je hebt gedaan om je applicatie veiliger te maken.

**✔️ opdracht 8 is klaar!**

## Vandaag voltooide taken

- 🗺️ Website in kaart gebracht met verschillende spiders.
- 🔥 Active scan uitgevoerd als niet-ingelogde gebruiker en ingelogde gebruiker.
- ✍️ Een request aangepast en deze verstuurd naar de webserver.
- 📃 Een rapport gegenereerd en opgeslagen.
