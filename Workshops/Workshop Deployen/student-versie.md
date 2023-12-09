# Workshop Deployen
# Voorwaarden deelname
Om deel te nemen, dien je de Skylab-workshop te hebben gevolgd en moet je webapplicatie een repository op Git hebben.
# Beschrijving
Tijdens deze workshop ga je je webapplicatie live zetten, zodat anderen er online bij kunnen komen! Dit bereik je door middel van zeven opdrachten. 🚀🛠️
# Eindresultaat
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
