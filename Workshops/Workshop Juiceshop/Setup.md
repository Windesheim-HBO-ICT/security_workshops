# Handleiding voor het installeren van Docker Desktop

Deze handleiding legt uit hoe je Docker Desktop kunt installeren op zowel Windows als Mac.

## Windows

1. Ga naar de officiële Docker-website: [https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop).
2. Klik op de knop "Download Docker Desktop".
3. Het downloaden van het installatiebestand zal automatisch starten. Wacht tot het downloaden is voltooid.
4. Dubbelklik op het gedownloade installatiebestand om het installatieproces te starten.
5. Volg de instructies op het scherm om Docker Desktop te installeren.
6. Na de installatie wordt Docker Desktop automatisch gestart.

## Mac

1. Ga naar de officiële Docker-website: [https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop).
2. Klik op de knop "Download Docker Desktop".
3. Het downloaden van het installatiebestand zal automatisch starten. Wacht tot het downloaden is voltooid.
4. Dubbelklik op het gedownloade installatiebestand om het installatieproces te starten.
5. Sleep het Docker Desktop-pictogram naar de map "Toepassingen" om Docker Desktop te installeren.
6. Open de map "Toepassingen" en dubbelklik op het Docker Desktop-pictogram om Docker Desktop te starten.

Gefeliciteerd! Je hebt Docker Desktop succesvol geïnstalleerd op zowel Windows als Mac. Je kunt nu aan de slag met het gebruik van Docker voor het bouwen en uitvoeren van containers.


# Handleiding voor het installeren van de Juice Shop

Deze handleiding legt uit hoe je de Juice Shop kunt installeren met behulp van Docker.

1. Open een nieuw Terminal-venster.
2. Voer het volgende commando uit om de Juice Shop te downloaden en te starten:

```
docker run --rm -p 3000:3000 bkimminich/juice-shop
```

3. Wacht tot de Juice Shop is gedownload en gestart.
4. Open een webbrowser en ga naar [http://localhost:3000](http://localhost:3000) om de Juice Shop te openen.
5. Gefeliciteerd! Je hebt de Juice Shop succesvol geïnstalleerd.
6. Sluit het Terminal-venster om de Juice Shop te stoppen.


## Mogelijke error's 

```
docker: Error response from daemon: dial unix docker.raw.sock: connect: no such file or directory.
```

### Oplossing:

Zorg ervoor dat Docker Desktop is geïnstalleerd en actief is. Als Docker Desktop al actief is, probeer het dan opnieuw te starten.