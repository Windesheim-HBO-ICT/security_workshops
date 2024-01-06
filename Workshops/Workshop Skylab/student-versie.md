# Workshop Skylab  


## Voorwaarden deelname
Geen

## Beschrijving 
**DTAP** staat voor Development, Testing, Acceptance, en Production, een gestructureerde aanpak waarbij verschillende omgevingen de software door diverse ontwikkelingsfasen leiden. Kortom, een slimme manier om software te ontwikkelen en te testen vóór productie. 

Voor jullie fungeert de acceptatieomgeving als zowel de acceptatie- als productieomgeving. 

**In deze workshop ga je aan de slag met het configureren van de acceptatieomgeving van je DTAP-buildstraat in Skylab (een virtuele omgeving). Dat ga je doen door **zes opdrachten** te maken**. 🛠️🚀
## Eindresultaat
Na het afronden van de workshop beschik je over het volgende eindresultaat:
-	**pfSense:** Een firewall die toegang beperkt tot alleen HTTP(S) (poort TCP/80 en TCP/443) en SSH (poort TCP/22).
-	**Kali Linux:** host met hacktools.
-	**Debian Linux:** host voor webserver.
-	**Domeinnaam:** website naam aangevraagd.

## Opdracht 1: Setup 
Voordat we aan de slag kunnen, moeten we een lab en de drie benodigde machines aan te vragen. _Houd er rekening mee dat dit enige tijd kan vergen_, aangezien het een handmatige handeling van het Skylab-beheer betreft. Volg de onderstaande stappen: 

**Stap 1:** Log in met je Windesheim-account  op [Skylab](https://skylab.windesheim.nl). **Let op: laat @windesheim.nl achterwege.**

**Stap 2:** Vraag een SE-lab aan.

**Stap 3:** Voer je studentnummer in bij 'Group Members' (voeg jezelf toe!).

**Stap 4:**  Vraag 3 hosts aan:
-	Een pfSense-firewall 
-	Een Debian 12 serverhost
-	Een Kali Linux host

*Als je alle stappen correct hebt doorlopen, zullen de machines zichtbaar zijn zodra je "Implementaties" open (linksboven, naast categorieën)*. 

**✔️ opdracht 1 is klaar!**
## Opdracht 2: Firewall Configureren

We gaan de router configureren om internettoegang voor alle machines mogelijk te maken. Deze opdracht is opgesplitst in twee delen: 
1. Voorbereiding van de router door instellingen van de machine aan te passen.
2. Koppelen van de routerinterfaces en tot stand brengen van een verbinding met het internet.
### Router Voorbereiding En Instellingen Configuratie
**Stap 1:** Ga naar het tabblad "Implementaties" en selecteer de pfSense-router.

**Stap 2:** Selecteer pLab-jouw studentnummer, klik op het tandwielpictogram en kies "reconfigure".

**Stap 3:** Klik op het tabblad "Network".

Je ziet nu twee netwerkinterfaces op de router:
- 💻 *LAN-interface:* Gebruikt voor directe communicatie binnen het lokale netwerk.
- 🌐 *WAN-interface:* Gebruikt voor gecontroleerde toegang tot het internet voor machines binnen het lokale netwerk.

**Stap 4**: Klik op "Edit" (bewerken) en wijzig alleen de netwerkinterface "Default First Network" naar studentnet0. Klik vervolgens op het groene vinkje en dan op "Submit".

**Stap 5:** Klik weer op pLab-jouw studentnummer klik vervolgens op het tandwielpictogram en kies “Power cycle”.

**Stap 6:** Klik opnieuw op pLab-jouw studentnummer, navigeer vervolgens naar het tabje “Network”.  Je hebt bij stap 8 de MAC-adressen van de netwerk interfaces nodig. Transit is de WAN en studentnet0 is de LAN.

**Stap 7:** Klik op pLab-jouw studentnummer en klik vervolgens op het tandwielpictogram, en selecteer "connect to your remote ".

### Terminal Connectie en Interface Koppeling
Je bent nu in de terminal van je router. De twee interfaces die we zojuist hebben opgezet, moeten nu aan de LAN- en WAN-poorten van de router worden gekoppeld.

**Stap 8:**  Voer 'n' in om geen VLAN's op te zetten en druk op Enter.

**Stap 9:** Je hebt nu het MAC-adres van de WAN-interface nodig. In de terminal van je router zie je vmx0 en vmx1 staan. Controleer welke overeenkomt met het MAC-adres van je WAN-interface en typ de juiste naam in (dus vmx0 of vmx1) en klik op enter.

**Stap 10**: Zet de LAN gelijk aan de overgebleven naam (dus welke je nog niet hebt gebruikt vmx0 of vmx1) en klik op enter.

**Stap 11:** Voer 'y' in om verder te gaan met het proces. 

**Stap 12:** Voer '7' in, druk op Enter en voer vervolgens 'google.nl' in. Als de ping succesvol is, zie je dat er 3 pakketten zijn aangekomen. Als dit niet het geval is, vraag dan om hulp, omdat er mogelijk iets fout is gegaan tijdens de configuratie.

**Stap 13:** In de pfsense terminal staat informatie over je ip-adres. In je terminal vind je de regel: *Wan -> vmx0 -> 145.xxx.xxx.xxx. Noteer of onthoud het ip-adres, deze heb je bij de volgende opdracht nodig.

**Stap 14:** Voer nu een update uit met ‘13’ en daarna een reboot met ‘y’. 


**✔️ Opdracht 2 is klaar!**

## Opdracht 3 Domeinadres Opvragen 
Apparaten binnen het interne netwerk communiceren via de router en de LAN-interface. Elk apparaat heeft een privé-IP-adres, herkenbaar aan "192.168.xxx.xxx". De router, met een publiek IP-adres (hier 145.xxx.xxx.xxx), fungeert als gateway naar het internet. Om de toegang tot de website te vereenvoudigen, moet een domeinnaam worden aangevraagd. Anderzijds is toegang tot de website later alleen mogelijk via het minder gebruiksvriendelijke publieke IP-adres (145.xxx.xxx.xxx).

**Vul het formulier in via [deze link](http://hbo-ict.org/proposename)! Je moet het **publieke IP-adres** van je router invullen, dat dus **145.xxx.xxx.xxx** is (genoteerd bij de vorige opdracht), en een **domeinnaam** opgeven. Laat je creativiteit vrij, maar houd het wel netjes 😊.**

**✔️ Opdracht 3 is klaar!**

## Opdracht 4 Debian Configureren 
Je Debian heeft geen grafische interface maar alleen een CLI, bewust gekozen omdat de machine als webserver fungeert. Minimaliseren van onnodige software is cruciaal voor prestaties en beveiliging. 

De opdracht is opgesplitst in drie delen: 
-	Voorbereiding van de Debian door instellingen van de machine aan te passen.
-	De Debian configureren via de terminal.
-	SSH installeren en testen

### Voorbereiden Webserver (Debian)

**Stap 1:** Ga naar het tabblad "Implementaties" en selecteer de Debian.

**Stap 2:** Selecteer pLab-jouw studentnummer, klik op het tandwielpictogram en kies "reconfigure".

**Stap 3:** Verhoog eerst het geheugen naar 3000 MB. 

**Stap 4:** Klik op het tabblad "Network".

**Stap 5:** Klik op "Edit" (bewerken) en wijzig alleen de netwerkinterface "Default First Network" naar studentnet0. Klik vervolgens op het groene vinkje en dan op "Submit".

**Stap 6:** Klik weer op pLab-\<jouw studentnummer\> klik vervolgens op het tandwielpictogram en kies “Power cycle”.

**Stap 7:**  Klik op pLab-\<jouw studentnummer\> en klik vervolgens op het tandwielpictogram, en selecteer "connect to your remote ".

### Configuratie Via Terminal

**Stap 8:** Log in met je gebruikersnaam 'student' en het wachtwoord 'Welkom01!'.

**Stap 9:** Type ‘passwd’ en verander je wachtwoord. Let op: vul eerst het huidige wachtwoord in ('Welkom01!') en daarna het nieuwe wachtwoord. **(Niet vergeten!)**

**Stap 10:** Controleer of je verbinding hebt tot het internet `ping google.nl` (ctrl Z om te stoppen).

**Stap 11:** Type het volgende om een nieuwe gebruiker aan te maken `sudo adduser <student number>` (**vergeet je wachtwoord niet!**) Als er om meer velden gevraagd wordt (Full name, work mail, etc) kun je deze gewoon leeg laten.
 
**Stap 12:** Type het volgende om sudo rechten te geven `sudo adduser <student number> sudo`

**Stap 13:**  Voer de volgende commando’s na elkaar uit om de machine te updaten
-	 `sudo apt update`
-	 `sudo apt upgrade`
-	 `sudo apt dist-upgrade`
-	 `sudo apt autoremove`

### SSH Installeren En Testen
**Stap 14:** Voer de volgende commando’s na elkaar uit om ssh te installeren en vervolgens te kijken of ssh draait. Als alles goed is gegaan zien ja achter ssh (Listen) staan.
-	`sudo apt install openssh-server`
-	`sudo lsof -i`

**Stap 15:**  Type `sudo reboot`

**Stap 16:** Login in met de gegevens van de nieuwe gebruiker.

**Stap 17:** Type ‘ip address’ om de privéadres van de Debian te zien. Deze zou moeten beginnen met 192.168.xxx.xxx

**✔️ Opdracht 4 is klaar**

## Opdracht 5 Kali Linux configureren
Je gaat nu de Kali configureren. In tegenstelling tot Debian heeft Kali Linux wel een grafische interface. Dit is omdat je deze machine gaat gebruiken om later je firewallregels in te stellen en de beveiliging van je Debian te testen met verschillende hackingtools.

**Voer dezelfde stappen uit zoals je dat bij de Debian hebt gedaan, met uitzondering van de SSH-server, deze is niet nodig. Vergeet niet om je wachtwoorden goed te bewaren. Raadpleeg de vorige opdracht voor explicietere uitleg.**

### Voorbereiden Kali
**Stap 1:** Netwerk interface naar studentnet0 

**Stap 2:** Opnieuw opstarten van machine 

**Stap 3:** Inloggen met inloggegevens student en Welkom01! 

### Configuratie Via Terminal
**Stap 4:** Open de terminal

**Stap 5:** Wachtwoord veranderen 

**Stap 6:** Test internet verbinding

**Stap 7:** Nieuwe gebruiker aanmaken en sudo rechten geven

**Stap 8:** Machine updaten 

**Stap 9:** Machine rebooten 

**Stap 10:** Inloggen met nieuwe gebruiker.

**✔️ Opdracht 5 is klaar**

## Opdracht 6 Firewall regels
In deze taak ga je port-forwarding regels instellen op de pfSense-firewall, zodat hosts op het internet je webapplicatie kunnen bereiken. Je bent klaar wanneer je kunt inloggen op Debian met een SSH-client vanaf elke machine op het internet, buiten Skylab. Deze taak is opgedeeld in twee onderdelen:
1.	Firewall regels opstellen 
2.	SSH testen

### Firewall regels 
**Stap 1:** Log in op je Kali-machine.

**Stap 2:** Open de browser en ga naar het privéadres van je router, meestal 192.168.1.1. Als je het niet zeker weet, typ dan 'ip route' in de terminal en noteer het eerste IP-adres dat je ziet, dat van de router is.

**Stap 3:**  Klik op 'Advanced' en accepteer de risico's.

**Stap 4:** Log in met de gebruikersnaam 'admin' en het wachtwoord 'pfsense'.

**Stap 5:** Nadat je bent ingelogd, zie je een rode waarschuwing om je wachtwoord te wijzigen. Klik erop, verander het wachtwoord en sla de wijzigingen op.

**Stap 6:** Open een nieuw venster en navigeer naar Skylab, selecteer “implementaties” daar moet het Privé IP-adres van Debian zichtbaar zijn, deze heb je nodig dus houd deze bij de hand.

**Stap 7**: Open weer het venster met de Kali machine en selecteer in 'Firewall' en vervolgens 'NAT'.

**Stap 8**: Klik op 'Add' en voeg regels toe voor de poorten TCP/80 (HTTP), TCP/443 (HTTPS) en TCP/22 (SSH) één voor één:
-	Verander Destination port range (from, to) naar HTTP.
-	Verander Redirect target IP (address) naar privé-IP-adres van Debian (192.168.xxx.xxx).
-	Verander Redirect target port (port) naar HTTP.
-	Sla de veranderingen op en doe hetzelfde voor HTTPS en SSH.

### SSH 
**Stap 10:** Als je regels hebt ingesteld voor poorten TCP/80 (HTTP), TCP/443 (HTTPS) en TCP/22 (SSH) (in totaal 3), klik dan op 'Apply Changes'.

**Stap 11:** Open op je eigen laptop (niet Skylab) de opdrachtprompt. Voer de volgende opdracht uit: 'ssh studentnummer@145.publiek IP-adres'. Als je je publieke IP-adres niet weet, kijk dan bij 'Implementaties' en zoek naar pfsense, daar zou je publieke IP-adres moeten staan.

Als alles goed is gegaan heb je nu vanaf je eigen laptop toegang tot de Debian. Is dat niet gelukt, vraag dan om hulp.

**✔️ Opdracht 6 is klaar**

## Vandaag voltooide taken
- 🌐 **Netwerkconfiguratie & Domeinnaamregistratie:**
  - Configuratie van de router voor internettoegang.
  - Aanvraag ingediend voor de domeinnaam van de website.

- 🖥️ **Webserverconfiguratie met Debian:**
  - Debian geconfigureerd als host voor de webserver.

- 🔒 **Kali (Beveiligingstest):**
  - Kali opgezet voor het testen van de beveiliging van de webserver.

- 🚪 **Port Forwarding-regels:**
  - Firewallregels opgesteld om alle aanvragen naar het publieke IP-adres van de router via HTTP, HTTPS en SSH naar Debian te leiden.

- 🔗 **Bevestiging via SSH:**
  - Succesvolle verbinding gemaakt met de webserver (Debian) vanaf de eigen laptop.

- 🚀 **Klaar voor 'Deployment'-workshop:**
  - Alles is gereed om de webapplicatie live te zetten.

