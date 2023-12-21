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
- In de instructies wordt verwezen naar http://localhost:XXXX. Als je je website al op skylab hebt gedeployed, kun je hier ook de daadwerkelijke URL van je applicatie gebruiken.

## Opdracht 1: 🗃️Setup 
Voordat we kunnen beginnen met pentesting, moeten we ZAP en de benodigde software installeren. Volg de onderstaande stappen: 

**Stap 1:** ZAP maakt gebruik van JAVA, als dit nog niet op je computer staat kun je dit <a href="https://www.oracle.com/java/technologies/downloads/" target="_blank">hier downloaden</a>. *Let op: Zap vereist minimaal JAVA versie 11.*

**Stap 2:** Download ZAP via <a href="https://www.zaproxy.org/download/" target="_blank">deze link</a>.

**Stap 3:** Volg de instructies in de setup.

**Stap 4:** Start ZAP.

**Stap 5:** Selecteer *Yes, I want to persist this session but I want to specify the name and location* en klik op start.

**Stap 6:** Geef een herkenbare naam en druk op save. Op deze manier word je sessie opgeslagen en kun je later verder met deze sessie.

*Als je alle stappen correct hebt doorlopen, zie je het volgende: ![ZAP home page](zaphomepage.png)* 

**✔️ opdracht 1 is klaar!**
## Opdracht 2: 🕷 Spider
We gaan starten met het in kaart brengen van je website, dit gaan we doen met een spider. Dit is een tool die automatisch nieuwe resources (URLs) ontdekt. De spider begint met een lijst aan URLs om te bezoeken en gaat van daaruit nieuwe hyperlinks opzoeken en voegt deze toe aan de lijst. Hij blijft doorgaan tot alle URLs in de lijst bezocht zijn.

### Opstarten Spider
**Stap 1:** Launch je eigen webapplicatie lokaal. Onthoud of noteer de URL (Bijvoorbeeld: https://localhost:7095/).

**Stap 2:** In ZAP, klik onderaan in de toolbar op de groene plus.

**Stap 3:** Selecteer *🕷 Spider*.

**Stap 4:** Klik op *🕷 New Scan*.

### Instellen scope
Om ervoor te zorgen dat de spider alleen op jouw webapplicatie blijft, moet eerst de scope ingesteld worden. Dit voorkomt dat ZAP andere websites scant of aanvalt.

**Stap 5:** In het veld *Starting point* vul je de URL van je eigen applicatie in die je bij stap 1 hebt genoteerd. **⚠️Let op: Gebruik ZAP alleen op applicaties waar je de eigenaar van bent, of waar je toestemming voor hebt. ZAP simuleert een echte aanval en kan echte schade aanrichten aan websites. ⚠️**

**Stap 6:** De context kan leeg blijven, dan wordt de standaard context gebruikt. De andere opties kunnen blijven zoals ze zijn.

*In de volgende opdracht gaan we de default context aanpassen met een gebruiker. Voor nu laten we wat het is.*

**Stap 7:** Klik op *Start Scan*.

### Resultaten spiderscan.
De lijst met URLs wordt nu gevuld. Bij elke URL staat de volgende informatie: 
- **Processed** - Of the URL was verwerkt door de spider of was overgeslagen. (Bijvoorbeeld buiten de scope)
- **Method** - De gebruikte HTTP methode, bijvoorbeeld **GET** of **POST**.
- **URL** - De gevonden resource.
- **Flags** - Extra informatie over de URL.

**Stap 8:** Aan de zijkant staat het tabje 🌍*Sites*. Als je de folder met URL van je webapplicatie uiteenklapt, zie je een folder structuur. Komt deze structuur (gedeeltelijk) overeen met de folderstructuur in je editor? Mis je nog een aantal folders/resources? Zie je bestanden die je er niet tussen wilt zien? Denk aan admin pagina's, pagina's die je alleen mag zien als je ingelogd bent of andere resources. Zie je onverwachte folders of items? Noteer deze dan.

**Stap 9:** In de toolbar onderaan staat een tabje 🚩*Alerts*. In dit tabje kun je zien welke security issues de spiderscan heeft gevonden. Bekijk de alerts, kies een aantal uit die je wil gaan oplossen.

**✔️ Opdracht 2 is klaar!**
## Opdracht 3: 🕷️ Ajax spider
De Ajax spider gebruikt een andere methode dan de normale spider om URLs te vinden. Deze spider is bedoeld voor sites die veel gebruik maken van AJAX (Asynchronous JavaScript and XML <a href="https://en.wikipedia.org/wiki/Ajax_(programming)" target="_blank">Wikipedia</a>). Omdat deze spider een andere methode gebruikt, kan deze ook andere URLs vinden. Het starten van de Ajax spider is vergelijkbaar met de normale spider.

### Opstarten Spider
**Stap 1:** Launch je eigen webapplicatie lokaal. Onthoud of noteer de URL (Bijvoorbeeld: https://localhost:7095/).

**Stap 2:** In ZAP, klik onderaan in de toolbar op de groene plus.

**Stap 3:** Selecteer *🕷 Ajax spider*.

**Stap 4:** Klik op *🕷 New Scan*.

**Stap 5:** In het veld *Starting point* vul je de URL van je eigen applicatie in die je bij stap 1 hebt genoteerd. **⚠️Let op: Gebruik ZAP alleen op applicaties waar je de eigenaar van bent, of waar je toestemming voor hebt. ZAP simuleert een echte aanval en kan echte schade aanrichten aan websites. ⚠️**

**Stap 6:** De context kan leeg blijven, dan wordt de standaard context gebruikt.

**Stap 7:** Zorg ervoor dat je bij het selecteren van een browser een *Headless* variant kiest. Anders worden er tientallen instanties van je browser geopend. 

**Stap 8:** Klik op *Start Scan*. De AJAX spider kan langer duren dan de normale spider.

### Resultaten spiderscan.
De lijst met URLs wordt nu gevuld. Bij elke URL staat de volgende informatie: 
- **Processed** - Of the URL was verwerkt door de spider of was overgeslagen. (Bijvoorbeeld buiten de scope)
- **Method** - De gebruikte HTTP methode, bijvoorbeeld **GET** of **POST**.
- **URL** - De gevonden resource.
- **Size Resp. Header en Size Resp. Body** - De grootte van de response header en body.

Je folder structuur is nu groter geworden, je ziet meer pagina's en andere resources in het 🌍*Sites* tabje. 
We hebben nu je webapplicatie in kaart gebracht. 

**✔️ opdracht 3 is klaar!**
## Opdracht 4: 🔥Active Scan
We hebben nu aan de hand van spiders je webapplicatie in kaart gebracht. Nu is het tijd om de gevonden pagina's aan te vallen.

**⚠️Let op: De volgende stappen kunnen schade toebrengen aan je applicatie en database. Het kan zijn dat je data uit je database verliest. Als er data in je database zit, die er niet via seeding in is gekomen, zorg er dan voor dat je een kopie van je database hebt.⚠️**

De active scan probeert verschillende bekende aanvallen tegen de geselecteerde doelen. Je kunt zelf instellen welke aanvallen extra vaak uitgevoerd worden en welke waarden deze krijgen. Standaard zijn deze instellingen goede genoeg voor het uitvoeren van de active scan.

**Stap 1:** In het 🌍*Sites* tabje, klik met je rechtermuis op de 📄*GET:/* pagina en selecteer *Attack* --> 🔥*Active scan*.

**Stap 2:** Klik op *Start Scan*.

Er wordt nu een scan uitgevoerd op de pagina's die gevonden zijn met de spiders.

**Stap 3:** Omdat deze scan iets langer kan duren, voornamelijk voor grote websites, is het mogelijk om specifiekere voortgang in te zien. In het 🔥*Active Scan* tabje dat nu is geopend, klik op het 📟*Progress details* icoontje naast de ⏸️*Pauze* en ⏹️*Stop* knop.

In het venster dat nu geopend wordt, zie je welke attacks uitgevoerd worden en hoever de attacks zijn. Hier wordt getoond hoeveel requests voor die attack zijn uitgevoerd en hoeveel van deze requests een alert opleveren.

## Opdracht 5: 👤Active scan met gebruikers-rechten
We hebben nu een scan uitgevoerd vanuit het perspectief van en niet-ingelogde gebruiker. Je hebt in je eigen applicatie aan de hand van Identity (of op een andere manier) authenticatie en authorizatie geïmplementeerd. ZAP kan ook werken vanuit een ingelogde gebruiker. We gaan nu een scan uitvoeren vanuit een standaard ingelogde gebruiker.

Een context is een manier om URLs die bij elkaar horen te groeperen. Het is aanbevolen om voor elke webapplicatie die in je systeem bestaat een aparte context te geven. In het geval van je eigen applicatie is dit er maar 1, daarom gebruiken we de default context. Om aan de default context een gebruiker toe te voegen, moet eerst een URL aan de context toegevoegd worden.

**Stap 4:** In het 🌍*Sites* tabje, klik met je rechtermuis op de 📂*https://localhost:XXXX* folder en selecteer *Include in context* --> *Default context*.

**Stap 5:** Bovenin het 🌍*Sites* tabje staat de context, dubbelklik op de default context om de default context in de session properties te wijzigen.

Onder het tabje *Context* --> *1: Default context* --> *1:Include in context* kun je zien dat de URL die we in stap 4 hebben toegevoegd in de include lijst staat.

Om een gebruiker toe te voegen, geven we ZAP instructies om in te loggen. We gaan aangeven waar de inlogpagina te vinden is, welke gegevens verstuurd moeten worden om in te loggen en hoe ZAP kan weten dat er ingelogd is.

**Stap 6:** Ga naar *Context* --> *1: Default context* --> *1: Authentication*.

**Stap 7:** Verander de authentication method naar form-based authentication.

**Stap 8:** In de *Login Form Target URL*, klik op 🌍*Select*. Selecteer de loginpagina POST request.   
Deze staat standaard onder 📂*https://localhost:XXXX* --> 📂*Identity* --> 📂*Account* --> 📄*POST:Login()(Input.Pass...)*.

**Stap 9:** Veel velden worden automatisch ingevuld, het is wel belangrijk om deze te controleren.
- URL to GET login page: De url die je gebruikt om bij de inlogpagina te komen. Bij Identity: *https://localhost:XXXX/Identity/Account/Login*
- Login Request POST Data: De data die meegegeven word in de POST voor het inloggen.
- Username parameter: Het veld waarin je de username meegeeft (Bij Identity: Input.Username).
- Password parameter: Het veld waarin je het wachtwoord meegeeft (Bij Identity: Input.Password).

Om ZAP te laten weten of de huidige pagina een ingelogde pagina is, moeten we een kenmerk van een ingelogde pagina meegeven. Dit is vaak een uitlogknop of een welkomstbericht. Voor een uitgelogde pagina is een kenmerk vaak een inlog-knop. We gaan nu handmatig in de applicatie inloggen, zodat we de inlogrequest en response in de history terug kunnen vinden.

**Stap 10:** Sluit het venster met de OK knop. In het quick start venster klik je op manual explore en vul je de URL van je applicatie in. 
Zet *Enable HUD** uit. Selecteer je browser en klik op *Launch Browser*. Log nu in met een gebruiker van je applicatie. Je kunt nu de geopende broser weer wegklikken.

**De HUD is een meer handmatige manier om je applicatie te ontdekken/aan te vallen. Er zitten ook functies in die niet in deze workshop worden behandeld. Als je dit interessant vind, kun je later de HUD aanzetten en de HUD-tutorial volgen.*

**Stap 11:** In het 📆*History* tabje vind je de requests die je zojuist gemaakt hebt. Meer info over de request en response, kun je in de ➡️*Request* en ⬅️*Response* tabjes vinden. Open het response tabje en klik op verschillende requests om de response te vinden die de HTML voor je ingelogde pagina toont. 

**Stap 12:** In de response body, zoek naar de uitlogknop HTML tag (Bijvoorbeeld: ***\<button id="logout" type="submit"\>Logout\</button\>***) en selecteer deze. Klik dan met je rechtermuisknop en *Flas as Context* --> *Default Context: Authentication Logged-in indicator* en klik op OK.

Je hebt nu aangegeven dat je op een ingelogde pagina bent, omdat er een uitlogknop op de pagina staat.

**Stap 13:** Doe nu hetzelfde, maar zoek nu in de 📆*History* een response van een niet-ingelogde pagina. Selecteer hierin de inlogknop en markeer deze als *Logged-out indicator*.

Je hebt nu voor ZAP aangegeven hoe je kunt inloggen, nu gaan we een gebruiker aanmaken.

**Stap 14:** In de session properties (dubbelklik op de default context bovenin het 🌍*Sites* tabje), klik in het tabje *Users* op Add. Geef je gebruiker een herkenbare naam en inloggegevens. Dit kan zijn van een bestaande gebruiker, of een gebruiker die je hier speciaal voor aanmaakt. Zorg er in ieder geval voor dat de gebruiker in je applicatie bestaat. Klik op OK om te bevestigen.

We hebben nu een gebruiker aangemaakt. Laten we paginas in kaart brengen die we alleen als ingelogde gebruiker kunnen bezoeken.

**Stap 15:** Ga terug naar het 🕷*Spider* tabje en volg de instucties zoals die zijn gegeven bij opdracht 1. Bij de context selecteer je de default context, bij de user selecteer je de zojuist aangemaakte gebruiker. Start de scan.

**Stap 16:** Doe hetzelfde voor de 🕷️*Ajax Spider*.

We hebben nu de applicatie als ingelogde gebruiker in kaart gebracht, nu kunnen we een groter deel van de website aanvallen.

**Stap 17:** Start een active scan en zorg ervoor dat de correcte context en user geselecteerd zijn.

**✔️ opdracht 4 is klaar!**

## Opdracht 5: ✍️Request wijzigen
We gaan een eerder gemaakt request wijzigen en kijken of we hiermee je webapplicatie kapot kunnen maken.

**Stap 1:** In het *Quick Start* tabje, klik op manual explore. vul de url van je applicatie in (http://localhost:XXXX), zet *Enable HUD* uit en launch in browser naar keuze.

**Stap 2:** Navigeer naar je inlog-pagina.

**Stap 3:** We moeten ervoor zorgen dat ZAP alle requests onderschept. Om dit te doen klik je op 🟢*Set Break on All Requests and Responses* in de menubar. 🟢 verandert naar 🔴.

**Stap 4:** Log in met een incorrect wachtwoord.

Als het goed is, wordt je request onderschept en krijg je deze te zien in ZAP.

**Stap 5:** We gaan het request wijzigen. Haal bijvoorbeeld het Input.UserName veld weg en klik op ▶️*Submit and Continue to Next Breakpoint*. Vangt je applicatie dit af?

**Stap 6:** Zet de 🟢break all weer aan en log nog een keer in, dit keer met correcte inloggegevens. Pas het *__RequestVerificationToken* aan. Kun je nu nog succesvol inloggen?

**Stap 7:** Probeer andere gegevens in de request te veranderen. Kun je iemand doorsturen naar een andere pagina? Kun je inloggen op een ander account? Kun je een SQL injectie uitvoeren?

**✔️ opdracht 5 is klaar!**
## Opdracht 6: 🔍Analyseren resultaten.
Om in te zien of je applicatie veiliger is geworden, gaan we nu een rapport genereren en later in het project nog een scan uitvoeren en daar ook een rapport van genereren. In je portfolio kun je deze resultaten vergelijken en aantonen welke verbeteringen je hebt uitgevoerd.

We gaan eerst een nulmeting vastleggen.

**Stap 1:** Klik in de menubar op *Report* --> *Generate report*

**Stap 2:** In de context, selecteer alleen je eigen applicatie (http://localhost:XXXX).

**Stap 3:** In het *Template* tabje, selecteer een template. Je kunt er hier zelf een van kiezen. Aanraders zijn:
- High level Report Sample. --> Handig voor makkelijk vergelijken van grafieken en een makkelijk tabelformaat om te kopieëren. Ook veel verwijzingen naar documentatie/uitleg over het veiligheidsrisico.
- Modern HTML Report with themes and options. --> Veel informatie en voorbeelden.
- Traditional Markdown Report. --> Makkelijk te lezen als plaintext.

**Stap 4:** Klik op *Generate Report*.

**Stap 5:** Sla het rapport op en zorg ervoor dat je deze later weer kunt bekijken.

**Stap 6:** Zorg ervoor dat je ook je sessie opslaat. Deze zou je later weer kunnen gebruiken.

**✔️ opdracht 6 is klaar!**
## Opdracht 7: ⚒️ Fixen

Deze opdracht doe je vanzelf in de volgende workshops en je eigen tijd. 

**Stap 1:** Bekijk het rapport en bedenk welke items je wilt aanpakken/verbeteren. 

Tip: Begin met de items die het meeste risico (*Risk*) vormen en de hoogste zekerheid (*Confidence*) hebben. Deze zijn handig in te zien in de Risk and Confidence  HTML template.

**Stap 2:** Bekijk de documentatie van deze security-risicos en zoek op het internet hoe je deze zou kunnen oplossen. Los de risicos in je applicatie op. 

Er is geen vast aantal dat je moet oplossen, het gaat erom dat je kunt aantonen dat je voldoende met de veiligheid van je webapplicatie bezig bent geweest.

**Stap 3:** Ben je verdergekomen met je applicatie en heb je een aantal veiligheidsrisicos opgelost? Voer nog een keer de spiders en een active scan uit. Genereer weer een rapport.

**Stap 4:** Vergelijk je rapporten en noteer de verschillen in je portfolio. Laat zien wat je hebt gedaan om je applicatie veiliger te maken.

**✔️ opdracht 7 is klaar!**

## Vandaag voltooide taken
- 🗺️ Website in kaart gebracht met verschillende spiders.
- 🔥 Active scan uitgevoerd als niet-ingelogde gebruiker en ingelogde gebruiker.
- ✍️ Een request aangepast en deze verstuurd naar de webserver.
- 📃 Een rapport gegenereerd en opgeslagen.