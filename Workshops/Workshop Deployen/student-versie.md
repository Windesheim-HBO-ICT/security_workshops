# Workshop Deployen

## Voorwaarden deelname

Om deel te nemen, dien je de Skylab-workshop te hebben gevolgd en moet je webapplicatie een repository op Git hebben.

## Beschrijving

Tijdens deze workshop ga je je webapplicatie live zetten, zodat anderen er online bij kunnen komen! Dit bereik je door middel van acht opdrachten. 🚀🛠️

## Eindresultaat

Na het doorlopen van deze workshop, heb je:

- Een reverse proxy opgezet 🔄
- Een SQL server opgezet 🗄️
- Gewerkt met Docker 🐳
- Een TLS-certificaat geïmplementeerd (inclusief een grondige scan) 🔒
- Jouw webapplicatie met succes gedeployed 🌐

## Opdracht 1 ASP dotnet core

In deze opdracht installeer en configureer je de Dotnet Core-applicatieserver met SDK op de acceptatieomgeving, waardoor je de omgeving gereed maakt om Dotnet Core-applicaties te ontwikkelen, testen én uit te voeren. 🚀✨👩‍💻

**Stap 1**: Open je opdrachtenprompt en login via SSH.

- `ssh <studentnummer>@145.44.xxx.xxx` **Vergeet niet de 's' toe te voegen voor je studentnummer.**

**Stap 2**: Voeg de Microsoft repository toe aan de APT (Advanced Package Tool) door de volgende commando’s uit te voeren:

- `sudo wget https://packages.microsoft.com/config/debian/12/packages-microsoft-prod.deb -O packages-microsoft-prod.deb`

- `sudo dpkg -i packages-microsoft-prod.deb`

- `sudo rm packages-microsoft-prod.deb`

**Stap 3**: Installeer de SDK:

```shell
sudo apt-get update && \
sudo apt-get install -y dotnet-sdk-8.0
```

**Stap 4**: Controleer de versie `dotnet --version`

**Stap 5**: Test Dotnet doormiddel van een console applicatie. Als je de volgende commando’s uitvoert zul je “Hello World!” zien.

- `sudo dotnet new console --output myConsoleApp`

- `sudo dotnet run --project myConsoleApp`

**Stap 6**: Installeer entity framework tool door het volgende commando uit te voeren:

- `sudo dotnet tool install --tool-path /usr/bin dotnet-ef`

**Stap 7**: Als dit gelukt is zul je de versie van entity framework zien als je het volgende commando uitvoert:

- `sudo dotnet tool list  --tool-path /usr/bin`

**Stap 8**: Installeer .Nettools:

- `dotnet tool install -g dotnetsay`

✅Opdracht 1 is Klaar!

## Opdracht 2 Docker installeren

In deze opdracht installeer je Docker; in latere stappen zullen we hier dieper op ingaan. Docker fungeert als een platform waarmee je applicaties kunt verpakken en isoleren in draagbare containers. Hierdoor wordt het beheer van applicaties over verschillende omgevingen consistent en efficiënt. 🐳🚀

**Stap 1**: Run de volgende commando’s om verouderde packages te verwijderen

- `for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done`

ℹ️ Je gaat nu de Docker APT-repository instellen. Dit houdt in dat je een pakketbeheerder op je Debian-systeem configureert, waardoor het systeem Docker-softwarepakketten kan herkennen en gebruiken

**Stap 2:** Voer de volgende commando’s een voor een uit :

- `sudo apt-get update`

- `sudo apt-get install ca-certificates curl`

- `sudo install -m 0755 -d /etc/apt/keyrings`

- `sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc`

- `sudo chmod a+r /etc/apt/keyrings/docker.asc`

```shell
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

**Als alles correct is verlopen, zie je het volgende verschijnen in je configuratie:**

✔️ ``` [arch=amd64 signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian <releasename> stable ```

**Voer tot slot een update uit:**:

- `sudo apt-get update`

⚠️ Krijg je een error waarbij er wordt aangegeven dat de release versie niet geaccepteerd wordt? Zorg er dan voor dat je in het bestand _apt/source.list.d/docker.list_ trusted op _yes_ zet.

**Stap 3**: Controleer of alles correct is verlopen. Als dat het geval is, zal de output niet leeg zijn. Gebruik hiervoor het commando:

- `cat /etc/apt/sources.list.d/docker.list`

**Stap 4**: Installeer docker `sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin`

**Stap 5**: Controleer of de Docker-installatie succesvol is verlopen. Als alles correct is, zal het commando `sudo docker run hello-world` "Hello from Docker!" weergeven en het programma afsluiten.

✅Opdracht 2 is Klaar!

## Opdracht 3 SQL server

In deze opdracht stel je een SQL Server in op een Docker-image en maak je een testdatabase aan. SQL Server is een databasesysteem waarmee je gegevens kunt beheren. Lokale databases worden vaak via LocalDB opgeslagen, terwijl een SQL Server in Docker een draagbare, geïsoleerde omgeving biedt voor databaseconfiguratie en -ontwikkeling. 🐳🛢️

### Deel 1 SQL server installeren

**Stap 1**: Haal de SQL Server 2022 (15.x) Linux-containerimage op vanuit de Microsoft Container Register.

- `sudo docker pull mcr.microsoft.com/mssql/server:2022-latest`

**Stap 2**: Run de container image met Docker met behulp van het volgende commando, waarbij je **YourStrong@Passw0rd** vervangt door een wachtwoord dat minimaal 10 tekens lang is en zowel hoofdletters als kleine letters bevat. Dit is het wachtwoord voor de systeembeheerder in SQL server.

```shell
sudo docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=YourStrong@Passw0rd" \
   -p 1433:1433 --name sql1 --hostname sql1 \
   -d \
   mcr.microsoft.com/mssql/server:2022-latest
```

**Stap 3**: Controleer of alles goed is gegaan door te kijken of de container met de naam 'sql1' actief is met het commando

- `sudo docker ps -a`

ℹ️ Handige commando's zijn onder andere het starten van een Docker-image met **sudo docker start {naam}**, het stoppen ervan met **sudo docker stop {naam}**, en het verwijderen met **sudo docker rm {naam}**.

### Deel 2 SQL server Testen

**Stap 4**: Voer het commando `sudo docker exec -it sql1 "bash"` uit.

**Stap 5**: Je bent nu binnen de container en je moet lokaal verbinding maken met sqlcmd door het volledige pad

- `/opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P "<YourNewStrong@Passw0rd>"` te gebruiken, met het wachtwoord dat je zojuist hebt aangemaakt.

**Stap 6**: Creëer een testdatabase met het commando `CREATE DATABASE TestDB;` gevolgd door `GO`.

**Stap 7**: Verifieer of je database is aangemaakt met het commando `SELECT Name from sys.databases;` gevolgd door `GO`.

✅Opdracht 3 is Klaar!

## Opdracht 4 Apache installeren

In deze opdracht installeer je apache-server, een veelgebruikte open-source webserver die wordt ingezet voor het hosten van webpagina's en het verwerken van HTTP-verzoeken van gebruikers. 🌐

**Stap 1**: Om terug te keren naar je normale terminal, voer je de commando `exit` uit binnen de container.

**Stap 2**: Installeer de nieuwste versie van apache

- `sudo apt install apache2`

**Stap 3**: Controleer of apache actief is, port 80 moet aan het luisteren zijn.

- `ss -ant`

**Stap 4** Voeg je zelf toe aan de docker groep zodat je docker images kan beheren.

- `sudo adduser (s-studentnummer) docker`

**Stap 5** Om te verifiëren dat alles goed is gegaan, ga je nu een statische website hosten op Docker via poort 6009.

- `sudo docker run -p 6009:80 -d dockersamples/static-site`

**Stap 6** Stuur een verzoek naar de website om de inhoud te bekijken. De poort is ingesteld op 6009 omdat je deze hebt toegewezen bij het starten van de Docker-container. Voer de volgende commando uit:

- `curl localhost:6009`.

ℹ️ Om de huidige lijst met actieve containers te controleren kun je het volgende Docker-commando gebruiken `sudo docker ps -a`. Dit commando toont een overzicht van alle containers op je systeem zowel de actieve als gestopte containers. Mocht je tegen problemen aanlopen controleer dan of je docker container actief is.

✅Opdracht 4 is Klaar!

## Opdracht 5 Git

Nu is het tijd om de code van de website op de Debian-server te plaatsen. Zorg ervoor dat je al een repository hebt opgezet. Als dat nog niet is gebeurd, stel er dan een in of vraag om hulp aan een student-assistent als je vastloopt. 🛠️

### Deel 1: Repository klonen

**Stap 1**: Open je code editor en ga naar je main branche.

**Stap 2**: Pas de connectiestring van de main branche aan zorg ervoor dat de gebruiker sa is en het wachtwoord overeenkomt met het wachtwoord dat je hebt ingesteld voor je SQL Server. Daarnaast moet de server worden ingesteld op localhost, de poort op 1433, en zet TrustServerCertificate op true. **Doe dit voor al je projecten die een database gebruiken**. Hier is een voorbeeld:.

`{
  "ConnectionStrings": {
    "DefaultConnection": "Server=localhost,1433;Database=myDatabase;User Id=sa;Password=YourSqlServerPassword;TrustServerCertificate=true;"
  },`

**Tussenstap**: Beginnen de routes van jouw API-project (als je die hebt) met /api? Zo niet, pas dat dan nu ook even aan, aangezien je toch de code aan het wijzigen bent. Dit is belangrijk voor de reverse proxy later. Hieronder staat een voorbeeld; dat scheelt je later werk

![image](https://github.com/Windesheim-HBO-ICT/security_workshops/assets/90692319/c1c51720-1432-474b-bd29-0a6d624de696)

**Stap 3**: Push de veranderingen

**Stap 4**: Ga naar GitHub, navigeer naar je project en klik op de groene knop om de HTTPS-link te kopiëren.

**Stap 5**: Open weer de terminal met ssh verbinding tot de Debian en clone je project. `git clone <git url>`

⚠️Als het klonen niet lukt, moet je mogelijk een token genereren en dat gebruiken als je wachtwoord. Ga naar de [link](https://github.com/settings/tokens). Noteer het token, want na generatie is deze niet meer zichtbaar en je hebt deze later nog nodig.

**Stap 6:** Bevestig of je MS SQLserver container nog draait `docker ps -a`;

**Stap 7:** Als het nodig is, start je de container met het commando `docker start sql1` als deze nog niet actief is.

### Deel 2: Migrations

⚠️ Stap 8 en 9 worden uitgevoerd voor alle projecten met een database, de overige stappen zijn voor nu alleen van toepassing op het front-end project. Als je later wijzigingen in je database wilt aanbrengen, kun je opnieuw stap 8 en 9 uitvoeren om je migraties bij te werken.

**Stap 8:** Voer migraties uit `dotnet ef migrations add InitialCreate`

**Stap 9:** Update je database `dotnet-ef database update`

✅Opdracht 5 is Klaar!

## Opdracht 6 Reverse proxy

Je gaat nu een reverse proxy opzetten met behulp van Apache (webserver). Een reverse proxy fungeert als een tussenliggende server tussen gebruikers en een webserver. Het verwerkt verzoeken van gebruikers, fungeert als een beveiligingslaag en optimaliseert de prestaties. 🌐🔒✨

**Stap 1**: Activeer de HTTP proxy module in Apache `sudo a2enmod proxy proxy_http`

ℹ️ In Linux kun je door mappen navigeren met behulp van het cd-commando gevolgd door de mapnaam om een map te betreden, of cd ../ om terug te gaan naar de vorige map. Met het commando nano kun je een tekstbestand bewerken.

**Stap 2**: Navigeer naar de 000-default.conf bestand.

- `sudo nano /etc/apache2/sites-enabled/000-default.conf`

**Stap 3**: Voeg de volgende keywords aan het bestand toe:

`ProxyPass / http://localhost:6009/
  ProxyPassReverse / http://localhost:6009/`

`ProxyPass /api http://localhost:5000
  ProxyPassReverse /api http://localhost:5000`

![image](https://github.com/Windesheim-HBO-ICT/security_workshops/assets/90692319/63be4cf3-fef7-415c-979a-ceb85a8d3581)

**Stap 4**: Gebruik de toetscombinatie `Control + X` om de wijzigingen op te slaan.

**Stap 5**: Restart apache `sudo systemctl restart apache2`

ℹ️ Je hebt zojuist succesvol een reverse proxy geconfigureerd! 🌐 Verkeer naar jouw website wordt doorgestuurd naar localhost:6009, terwijl verzoeken naar jouw interne API worden gerouteerd via het pad /api naar localhost:5000. 🚀 Zorg ervoor dat je in de naamgeving van je API-controllers het /api-pad hebt toegevoegd, indien dat nog niet is gedaan. 🔍
![image](https://github.com/Windesheim-HBO-ICT/security_workshops/assets/90692319/4c730ac3-4060-4137-b6c3-c512196b75de)

**Stap 6:** Ga naar de map van je project (gebruik hiervoor `cd` en `ls`) en voer vervolgens het volgende commando uit:

- `dotnet run --urls=http://localhost:6009`.

**Stap 7:** Zodra het bouwen van je project is voltooid, navigeer je in je browser naar de website via je domeinnaam als je die al hebt, of via je openbare IP-adres (bijvoorbeeld 145.44.xxx.xxx). Als je webapplicatie zichtbaar is, ben je klaar.

✅Opdracht 6 is Klaar!

## Opdracht 7 TLS certificaat

In deze opdracht zorg je ervoor dat jouw webapplicatie beschikbaar is via HTTPS. HTTPS is een protocol dat zorgt voor versleutelde communicatie tussen de gebruiker en de webserver, wat essentieel is voor veiligheid en privacy. Om HTTPS mogelijk te maken, heb je een TLS-certificaat nodig. 🔒✨

### Deel 1 Snap installeren

**Stap 1:** Voer een systeemupdate uit met het commando:

- `sudo apt update`.

**Stap 2**: Installeer Snapd met het commando:

- `sudo apt install snapd`.

**Stap 3**: Controleer de status van Snapd met het commando

- `sudo systemctl status snapd`.
  Als er iets mis is gegaan, voer dan het volgende commando uit: `sudo systemctl enable --now snapd.socket.`

**Stap 4**: Installeer de core-snaps met het commando `sudo snap install core`. Hiermee installeer je de basiscomponenten die nodig zijn voor het gebruik van Snap-pakketten.

### Deel 2 Certbot installeren

**Stap 5**: Verwijder verouderde Certbot-pakketten met het commando `sudo apt-get remove certbot`.

**Stap 6**: Installeer Certbot via snap met het commando `sudo snap install --classic certbot`. Hiermee verkrijg je Certbot voor het beheren van TLS-certificaten.

**Stap 7**: Zorg ervoor dat certbot gerund kan worden op je machine door de volgende uit te voeren

- `sudo ln -s /snap/bin/certbot /usr/bin/certbot`

**Stap 8**: Voer het commando`sudo certbot --apache` uit. Hiermee start je Certbot met de Apache-plugin, waardoor je een SSL-certificaat kunt verkrijgen en configureren voor je webapplicatie.

**Stap 9**: Ga naar de map van je project (`cd` en `ls`) en voer vervolgens het volgende commando uit:

- `dotnet run --urls=http://localhost:6009`.

**Stap 10**: Ga naar je website en controleer of er een slotje staat.

ℹ️ Je hebt zojuist succesvol een TLS-certificaat toegepast op je webserver. TLS (Transport Layer Security) is de hedendaagse opvolger van SSL (Secure Sockets Layer), beide ontworpen om gegevens te versleutelen tijdens de communicatie tussen een webserver en een gebruiker. Met dit TLS-certificaat wordt de vertrouwelijkheid en integriteit van de gegevensoverdracht verzekerd. Het is een cruciale stap om een veilige verbinding (https) op een website te realiseren. 🔒✨

**Stap 11**:
Nadat je het TLS-certificaat hebt geïnstalleerd, is het raadzaam een beveiligingsrapport voor je portfolio te genereren. Voer [de test](https://www.ssllabs.com/ssltest/) uit om de configuratie te analyseren, mogelijke kwetsbaarheden te identificeren en voeg een screenshot van het rapport toe aan je portfolio als mogelijk bewijsmateriaal.

✅Opdracht 7 is Klaar!

## Opdracht 8: Deployen

🚀 Je staat nu op het punt je projecten te deployen! Als het goed is, zijn de connection strings voor alle projecten al correct geconfigureerd, heb je alle migraties al uitgevoerd, en ben je klaar om te beginnen. 💻✨

**Stap 1:** Navigeer naar de projectfolder van je front-end project.

**Stap 2:** Voer het volgende commando uit om je project te publiceren:

- `dotnet publish -r linux-x64 --self-contained false --configuration Release`

**Stap 3:** Navigeer vanuit dezelfde folder naar bin/Release/net-8.0/linux-x64/publish.

**Stap 4:** In die folder zul je \<projectnaam\>.dll zien staan. Voer de volgende commando uit

- `dotnet <projectnaam>.dll --urls=http://localhost:6009`

**Stap 5:** ⛔ Stop je applicatie door Ctrl + Z in te voeren, zodat je deze op de achtergrond kan draaien.

**Stap 6:** Voer het commando `bg` uit om het op de achtergrond te laten draaien.

**Stap 7:** Herhaal de bovenstaande stappen voor je API project. **Laat bij stap 4 voor de API --urls=<http://localhost:6009> weg, zie hieronder een voorbeeld!!**

- `dotnet  <projectnaam>..dll`

**Stap 8:** Controleer of alle stappen succesvol zijn verlopen door naar je website te navigeren. Als je een eenvoudige GET-request hebt, kun je jouw API in de terminal testen met de volgende commando's:

Met TLS-certificaat (HTTPS):

- `curl https://localhost/api/ <naam_get_request>`

Geen TLS-certificaat (de redirect naar https lukt niet):

- `curl https://localhost:5000/api/ <naam_get_request>`

Je hebt zojuist je webapplicatie gepubliceerd met de configuratie "Release". Hierdoor draait je applicatie nu in productiemodus, geoptimaliseerd voor efficiëntie en prestaties. 👏✨

**Belangrijk:** Wanneer je tussentijdse wijzigingen aanbrengt in je applicatie, haal deze dan op met 'git pull' en voer eventuele database-migraties uit in je projectfolder. Na deze stappen dien je de applicatie opnieuw te publiceren met de bovenstaande commando's om ervoor te zorgen dat deze up-to-date is. Het is mogelijk dat je een melding krijgt dat de poorten in gebruik zijn. Als dat het geval is, zoek dan de commando's op om ze te sluiten. ✨🔄

✅Opdracht 7 is Klaar!

## Voltooide Taken van Vandaag

- 🔄 **Reverse Proxy**

  - Implementatie van een reverse proxy via Apache voor verbeterde verkeersroutering

- 🗄️ **SQL-server**

  - Opzetten van een SQL-server binnen een Docker-container voor effectief gegevensbeheer.

- 🐳 **Docker**

  - Professionele implementatie van een TLS-certificaat op de webserver voor versleutelde communicatie. Inclusief een grondige scan voor beveiligingsrisico's.

- 🔒 **TLS-certificaat Implementeren:**

  - Implementatie Docker voor draagbaarheid en vereenvoudigde implementatie van applicaties.

- 🌐 **Webapplicatie Deployen:**

  - Beschikbaar maken van de webapplicatie voor eindgebruikers. ✅

  Reflecteer op de activiteiten die je hebt uitgevoerd in je eindverslag over je portfolio en zorg ervoor dat je dit ondersteunt met bewijsmateriaal. Je hebt immers veel bereikt vandaag (rapport TLS, Git, reverse proxy-instellingen, enzovoort). Je bent nu klaar voor de workshop ZAP. 🚀💻✨
