# Workshop Skylab
In de workshop "SkyLab" wordt de acceptatieomgeving van de DTAP-buildstraat geconfigureerd. Na afloop van deze workshop hebben de studenten de router, Debian, Kali en de firewallregels ingesteld. De workshop is opgedeeld in 6 opdrachten, hieronder worden ze beschreven en eventuele aandachtspunten worden genoemd.

## Opdracht 1 Setup Omgeving 
De student moet een SE lab, Debian 12, Kali Linux en pfSense aanvragen. Alles is in orde wanneer alles zichtbaar is onder "Implementaties". Houd er rekening mee dat het even kan duren voordat de aanvragen zijn verwerkt.
## Opdracht 2 Router 
De student configureert nu de pfSense-router. De WAN-interface is al goed ingesteld als 'Transit'. De LAN-interface met het default network wordt gewijzigd naar 'student01'. Daarna moeten de interfaces via de router worden gekoppeld. Alles is goed als er met succes wordt gepinged naar bijvoorbeeld 'google.nl'. 
## Opdracht 3 Domeinnaam Aanvragen 
De student moet een domeinnaam aanvragen, zodat de webapplicatie later niet alleen via het publieke IP-adres bereikbaar is, en ook om een TLS-certificaat aan te vragen. Het goedkeuringsproces voor de domeinnaam kan echter enkele dagen duren.
## Opdracht 4 Debian
De student configureert Debian door eerst de netwerkinterface te wijzigen naar student01. Daarna moet de student het standaardwachtwoord wijzigen, een nieuwe gebruiker aanmaken en SSH installeren. De Debian heeft geen gebruiker interface.
## Opdracht 5 Kali 
De student configureert Kali op dezelfde manier als Debian, met uitzondering van SSH.
## Opdracht 6 Firewall
De student stelt de firewall in door eerst het standaardwachtwoord te wijzigen en vervolgens de portforwarding-regels van de firewall aan te passen voor de poorten TCP/80 (HTTP), TCP/443 (HTTPS) en TCP/22 (SSH) zodat deze verzoeken worden doorgestuurd naar Debian. Na het instellen van de regels kan de student via SSH verbinding maken met zijn Debian.

