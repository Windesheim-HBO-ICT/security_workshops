# Workshop Deployen
## Voorwaarden deelname
Om deel te nemen, dien je de Skylab-workshop te hebben gevolgd en moet je webapplicatie een repository op Git hebben.
## Beschrijving
Tijdens deze workshop ga je je webapplicatie live zetten, zodat anderen er online bij kunnen komen! Dit bereik je door middel van zeven opdrachten. 🚀🛠️
## Eindresultaat
Na het doorlopen van deze workshop, heb je:
-	Een reverse proxy opgezet 🔄
-	Een SQL server opgezet 🗄️
-	Gewerkt met Docker 🐳
-	Een TSL-certificaat geïmplementeerd (inclusief een grondige scan) 🔒
-	Jouw webapplicatie met succes gedeployed 🌐

## Opdracht 1 ASP dotnet core
In deze taak installeer en configureer je de Dotnet Core applicatieserver, inclusief de SDK, op de op de acceptatieomgeving.

 **Stap 1**:  Open je opdrachtenprompt en login via SSH.   
 
 `ssh s-studentnummer@145.xxx.xxx`



**Stap 2** : Voeg de Microsoft repository to aan de APT (Advanced Package Tool) door de volgende commando’s uit: 

`sudo wget https://packages.microsoft.com/config/debian/12/packages-microsoft-prod.deb -O packages-microsoft-prod.deb`

`sudo dpkg -i packages-microsoft-prod.deb`

`sudo rm packages-microsoft-prod.deb`


**Stap 3** : Installeer de SDK: ` sudo apt-get update && \ sudo apt-get install -y dotnet-sdk-8.0`


**Stap 4**:  Controleer de versie `dotnet –version`


**Stap 5**: Test Dotnet doormiddel van een console applicatie. Als je de volgende commando’s uit voert zul je “Hello World!” zien.

`sudo dotnet new console --output myConsoleApp`

`sudo dotnet run --project myConsoleApp`


**Stap 6**: Installeer entity framework tool door de volgende commando uit te voeren: 

`sudo dotnet tool install --tool-path /usr/bin dotnet-ef`


**Stap 7**: Als gelukt is zul je de versie van entity framework zien als je de volgende commando uitvoert: 

` $ sudo dotnet tool list  --tool-path /usr/bin`


**Stap 8:** Installeer .Nettools: 

`dotnet tool install -g dotnetsay`

✅Opdracht 1 is Klaar! 

## Opdracht 2  Docker installeren
Docker is een platform waarmee je applicaties kunt verpakken en draaien in geïsoleerde, draagbare containers. Het maakt het gemakkelijk om applicaties consistent en efficiënt over verschillende omgevingen te verplaatsen. In deze opdracht ga je docker installeren, in een latere opdrachten ga je nog meer hiermee doen.

**Stap 1**:  Open je opdrachtenprompt en login via SSH.   `ssh s-studentnummer@145.xxx.xxx`
**Stap 2**:  Run de volgende commando’s om verouderde packages te verwijderen 

` for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done`

ℹ️ Je gaat nu de Docker APT-repository instellen. Dit houdt in dat je een pakketbeheerder op je Debian-systeem configureert, waardoor het systeem Docker-softwarepakketten kan herkennen en gebruiken

**Stap 3:** Voer de volgende commando’s een voor een uit : 

` sudo apt-get update`

` sudo apt-get install ca-certificates curl gnupg`

` sudo install -m 0755 -d /etc/apt/keyrings `

`  curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg `

` sudo chmod a+r /etc/apt/keyrings/docker.gpg `

` echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null `
` sudo apt-get update`

**Stap 4**: Controleer of alles correct is verlopen. Als dat het geval is, zal de uitvoer niet leeg zijn. Gebruik hiervoor het commando, ` cat /etc/apt/sources.list.d/docker.list`

**Stap 5**:  Installeer docker `sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin`

**Stap 6** : Controleer of de Docker-installatie succesvol is verlopen. Als alles correct is, zal het commando `sudo docker run hello-world` "Hello World" weergeven en het programma afsluiten.

✅Opdracht 2 is Klaar! 

## Opdracht 3 SQL server
In deze opdracht ga je een SQL Server instellen op een Docker-image. Daarna maak je een testdatabase aan.

### Deel 1 SQL server installeren

**Stap 1**: Haal het SQL Server 2022 (15.x) Linux-containerimage op vanuit de Microsoft Container Register. ` sudo docker pull mcr.microsoft.com/mssql/server:2022-latest`

**Stap 2**: Run de container image met Docker met behulp van de volgende commando, waarbij je <YourStrong@Passw0rd> vervangt door een wachtwoord dat minimaal 10 tekens lang is en zowel hoofdletters als kleine letters bevat.  Dit is het wachtwoord voor de systeembeheerder in SQL server.
` sudo docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong@Passw0rd>" \
   -p 1433:1433 --name sql1 --hostname sql1 \
   -d \
   mcr.microsoft.com/mssql/server:2022-latest `

**Stap 3**:  Controleer of alles goed is gegaan door te kijken of de container met de naam 'sql1' actief is met het commando 

`sudo docker ps -a`

ℹ️ Handige commando's zijn onder andere het starten van een Docker-image met **sudo docker start {naam}**, het stoppen ervan met **sudo docker stop {naam}**, en het verwijderen met **sudo docker rm {naam}**.

### Deel 2 SQL server Testen 

**Stap 4**: Voer de commando `sudo docker exec -it sql1 "bash"` uit.

**Stap 5**: Je bent nu binnen de container en je moet lokaal verbinding maken met sqlcmd door het volledige pad 

` /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P "<YourNewStrong@Passw0rd>"` te gebruiken, met het wachtwoord dat je zojuist hebt aangemaakt.

**Stap 6**: Creëer een testdatabase met het commando 'CREATE DATABASE TestDB;' gevolgd door 'GO'.

**Stap 7**: Verifieer of je database is aangemaakt met het commando 'SELECT Name from sys.databases;' gevolgd door 'GO'.


✅Opdracht 3 is Klaar! 

# Opdracht 4 Git
Je gaat nu de code van de website op de Debian-server plaatsen. Als het goed is, heb je al een repository opgezet. Als dat niet het geval is, stel er dan een in of vraag om hulp aan een student-assistent als je er niet uitkomt.

### Repository klonen
**Stap 1**: Open je code editor en ga naar je main branche.

**Stap2**:  Pas de connectiestring van de main branche aan zorg ervoor dat de gebruiker sa is en het wachtwoord overeenkomt met het wachtwoord dat je hebt ingesteld voor je SQL Server. Daarnaast moet de server worden ingesteld op localhost, de poort op 1433, en zet TrustServerCertificate op true. **Doe dit voor je projecten die een database gebruiken**. Hier is een voorbeeld:.

`{
  "ConnectionStrings": {
    "DefaultConnection": "Server=localhost,1433;Database=myDatabase;User Id=sa;Password=YourSqlServerPassword;TrustServerCertificate=true;"
  },`

**Stap 3**: Push de veranderingen

**Stap 4**: Ga naar GitHub, navigeer naar je project en klik op de groene knop om de HTTPS-link te kopiëren.

**Stap 5**: Open weer de terminal met ssh verbinding tot de Debian en clone je project. ‘git clone <git url>`

⚠️Als het klonen niet lukt, moet je mogelijk een token genereren en dat gebruiken als je wachtwoord. Ga naar de link https://github.com/settings/tokens. Noteer de token, want na generatie is deze niet meer zichtbaar en je hebt deze later nog nodig. 

**Stap 6:** Bevestig of je MS SQLserver container nog draait `docker ps -a`;

**Stap 7:** Als het nodig is, start je de container met het commando `docker start sql1` als deze nog niet actief is.

### Migrations
⚠️ Stap 8 en 9 worden uitgevoerd voor alle projecten met een database, de overige stappen zijn voor nu alleen van toepassing zijn op het front-end project.

**Stap 8:** Voer migraties uit ` dotnet ef migrations add InitialCreate`

**Stap 9:** Update je database ` dotnet-ef database update`

**Stap 10:** Ga naar de map van je project (gebruik hiervoor `cd` en `ls` als hints) en voer vervolgens het 
volgende commando uit: `dotnet run --urls=http://localhost:6009`.

**Stap 11:** Zodra het bouwen van je project is voltooid, navigeer je in je browser naar de website via je domeinnaam als je die al hebt, of via je openbare IP-adres (bijvoorbeeld 145.44.xxx.xxx). Als je webapplicatie zichtbaar is, ben je klaar.

✅Opdracht 4 is Klaar! 


## Opdracht 5 Reverse proxy
Je gaat nu een reverse proxy opstellen met behulp van Apache (webserver). Een reverse proxy fungeert als een tussenliggende server tussen gebruikers en een webserver. Het verwerkt verzoeken van gebruikers, fungeert als een beveiliging laag en optimaliseert de prestaties. 

### Deel 1: Apache installatie 
**Stap 1**:  ⛔ Stop je applicatie door Ctrl + Z in te voeren. 

**Stap 2**: Instaleer de nieuwste versie van apache  ` sudo apt install apache2`

**Stap 3**: Controleer f apache actief is, port 80 moet aan het luisteren zijn.  ` ss -ant`

**Stap 4**  Identificeer je privé IP adres, je hebt deze zo nodig. ` ip address`

**Stap 5** Voeg je zelf toe aan de docker groep zodat je docker images kan beheren. ` sudo adduser (s-studentnummer) docker`

**Stap 6** Om te verifiëren dat alles goed is gegaan, ga je nu een statische website hosten op Docker via poort 6009. `sudo docker run -p 6009:80 -d dockersamples/static-site`

**Stap 7**  Stuur een verzoek naar de website om de inhoud weer te geven. De poort is ingesteld op 6009 omdat je deze hebt toegewezen bij het starten van de Docker-container. Voer het commando uit met `curl localhost:6009`.

ℹ️ Om de huidige lijst met actieve containers te controleren kun je het volgende Docker-commando gebruiken `sudo docker ps -a`.  Dit commando toont een overzicht van alle containers op je systeem zowel de actieve als gestopte containers. Mocht je tegen problemen aanlopen controleer dan of je docker container actief is.

### Deel 2: Reverse proxy configureren
Je gaat nu de reverse proxy functionaliteit toevoegen. Mocht je een melding krijgen dat de module al enabled is voer dan na stap 7  de volgende commando uit: ` sudo systemctl restart apache2`

**Stap 8**: Activeer de HTTP proxy module in Apache ` sudo a2enmod proxy proxy_http`

ℹ️ In Linux kun je door mappen navigeren met behulp van het cd-commando gevolgd door de mapnaam om een map te betreden, of cd ../ om terug te gaan naar de vorige map. Met het commando nano kun je een tekstbestand bewerken.

**Stap 9**:  Navigeer naar de 000-default.conf bestand.  `sudo nano /etc/apache2/sites-enabled/000-default.conf`

**Stap 9**: Voeg de volgende keywords  aan het bestand toe: 

` ProxyPass / http://localhost:6009/
  ProxyPassReverse / http://localhost:6009/`

` ProxyPass /api http://localhost:5000
  ProxyPassReverse /api http://localhost:5000`

 ![image](https://github.com/Windesheim-HBO-ICT/security_workshops/assets/90692319/63be4cf3-fef7-415c-979a-ceb85a8d3581)


**Stap 10**:  Toets `Control x` en bewaar de veranderingen.

**Stap 11**:  Restart apache ‘sudo systemctl restart apache2`

ℹ️ Je hebt nu succesvol een reverse proxy opgezet. Verkeer naar jouw domeinnaam of website wordt doorgestuurd naar localhost:6009, terwijl verzoeken naar jouw interne API worden gerouteerd via het pad /api naar localhost:5000. Het is belangrijk ervoor te zorgen dat je in je API-controllers het /api-pad hebt toegevoegd aan de naamgeving, indien dat nog niet was gedaan. 

✅Opdracht 5 is Klaar! 

## Opdracht 6 TSL certificaat
In deze opdracht ga je ervoor zorgen dat je webapplicatie beschikbaar is via HTTPS. HTTPS is een protocol dat zorgt voor versleutelde communicatie tussen de gebruiker en de webserver, wat essentieel is voor veiligheid en privacy. Om HTTPS mogelijk te maken, heb je een TLS-certificaat nodig. 

### Deel 1 Snap installeren
**Stap 1:** Voer een systeemupdate uit met het commando sudo apt update.

**Stap 2**: Installeer Snapd met het commando `sudo apt install snapd`.

**Stap 3**: Controleer de status van Snapd met het commando `sudo systemctl status snapd`.
Als er iets mis is gegaan, voer dan het volgende commando uit: 
`sudo systemctl enable --now snapd.socket.` 

**Stap 4**:  Installeer de core-snaps met het commando `sudo snap install core`. Hiermee installeer je de basiscomponenten die nodig zijn voor het gebruik van Snap-pakketten. 

### Deel 2 Certbot installeren 
**Stap 5** : Verwijder verouderde Certbot-pakketten met het commando `sudo apt-get remove certbot`. Hiermee ruim je oude Certbot-installaties op.

**Stap 6**: Installeer Certbot als een klassieke snap met het commando `sudo snap install --classic certbot`. Hiermee verkrijg je Certbot voor het beheren van TLS-certificaten.

**Stap 7**: Zorg ervoor dat certbot gerund kan worden op je machine door de volgende uit te voeren 

`sudo ln -s /snap/bin/certbot /usr/bin/certbot`

**Stap 8**:  Voer het commando` sudo certbot --apache` uit. Hiermee start je Certbot met de Apache-plugin, waardoor je een SSL-certificaat kunt verkrijgen en configureren voor je webapplicatie.

**Stap 9:** Ga naar de map van je project (gebruik hiervoor `cd` en `ls` als hints) en voer vervolgens het volgende commando uit: 

`dotnet run --urls=http://localhost:6009`.

**Stap 10:** Ga naar je website en controleer of er een slotje staat, wat aangeeft dat HTTPS correct is geconfigureerd.

## Opdracht 7: Deployen
🚀 Je staat op het punt je projecten te deployen! Als het goed is, zijn de connection strings voor alle projecten al correct geconfigureerd, heb je alle migraties al uitgevoerd, en ben je klaar om te beginnen. 💻✨

**Stap 1:** Navigeer naar de projectfolder van je front-end project. Gebruik het commando cd.

**Stap 2:**  Voer het volgende commando uit om je project te publiceren:
-	`dotnet publish -r linux-x64 --self-contained false --configuration Release`

**Stap 3:**  Navigeer vanuit dezelfde folder naar bin/Release/net-8.0/linux-x64/publish.

**Stap 4:** In die folder zul je  <projectnaam>.dll zien staan. Voer de volgende commando uit 
-	`dotnet <projectnaam>.dll --urls=http://localhost:6009 `
**Stap 5: ** ⛔ Stop je applicatie door Ctrl + Z in te voeren, zodat je deze op de achtergrond kan draaien. 

**Stap 6:** Voer het commando bg uit om het op de achtergrond te laten draaien.

**Stap 7:** Herhaal de bovenstaande stappen voor je API project. Het enigste verschil zit in stop vier daar run je hem niet op poort 6009, maar op 5000 dus 
-	`dotnet  <projectnaam>..dll --urls=http://localhost:5000`

Je hebt zojuist je webapplicatie gepubliceerd met de configuratie "Release". Hierdoor draait je applicatie nu in productiemodus, geoptimaliseerd voor efficiëntie en prestaties. 👏✨

**Herinnering:** Als je tussentijds wijzigingen aanbrengt in je applicatie, haal je deze op met git pull en voer eventuele database-migraties uit in je projectfolder. Na deze stappen moet je de applicatie opnieuw publiceren met de bovenstaande commando's om ervoor te zorgen dat deze up-to-date is. ✨🔄
✅Opdracht TODO is Klaar! 




 


