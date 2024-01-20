# Workshop SAST

## Voorwaarden deelname

Voor opdracht 3 is het nodig om je website gedeployed te hebben, de andere opdrachten vereisen dat je code op github staat.

Deze workshop is een zelfstudie workshop.

## Beschrijving

Er zijn veel externe veiligheids analyse tools beschikbaar om de veiligheid van je applicatie bij te houden. In deze workshop kijken we naar een aantal tools en wordt er beschreven hoe je deze kunt gebruiken.

## Eindresultaat

Na het afronden van de workshop beschik je over het volgende eindresultaat:

- Een workflow om dependencies up to date te houden.
- Een workflow om de applicatie te scannen op veiligheidsrisico's.
- Je live website handmatig gescand op veiligheidsrisico's.

## Opdracht 1: Automatisch updaten van dependencies

Om je applicatie veilig te houden is het belangrijk om regelmatig updates uit te voeren. Het makkelijkste is om dit te automatiseren, door bijvoorbeeld gebruik te maken van Github actions.

In deze opdracht ga je een eigen workflow toevoegen waarmee je automatisch je dependencies kunt updaten.

**Stap 1:** Zoek een action die bij je type project past. Voor dotnet zou je bijvoorbeeld <https://github.com/marketplace/actions/dotnet-dependency-update> kunnen gebruiken.

Voor iets anders dan dotnet kun je zoeken op dependency update: <https://github.com/marketplace?category=&type=actions&verification=&query=dependency+update>

**Stap 2:** In je eigen project maak de folder structuur \<Projectroot\>/.github/workflows/DependencyUpdater.yml

**Stap 3:** In het DependencyUpdater.yml bestand plak je de code die bij Usage vermeld staan. Probeer het moment waarop de action runt naar een logische waarde te wijzigen. Denk bijvoorbeeld aan 1 keer per week.

**Stap 4:** Test de action door deze eenmalig handmatig te runnen.

**✔️ opdracht 1 is klaar!**

## Opdracht 2: Github CodeQL

[Github CodeQL](https://codeql.github.com/) is een code analyse tool, die je helpt met het ontdekken van veiligheidsrisico's en problemen in je code. Dit wordt gedaan door een [statische analyse](https://en.wikipedia.org/wiki/Static_application_security_testing) van je code te doen. Hierbij wordt je code niet uitgevoerd, maar wordt er gezocht naar bekende patronen of kenmerken van veiligheidsrisico's. M

et deze opdracht voeg je een Github action toe, waarmee je CodeQL uitvoert. Let op: deze action is alleen beschikbaar als je repository op public staat. Voor alternatieven die ook werken op private repositories check onderaan bij resources.

**Stap 1:** Ga naar de GitHub pagina van je applicatie en klik op het actions tabje.

**Stap 2:** Klik op New Workflow en zoek naa codeql.

**Stap 3:** Klik op configure bij *"CodeQL Analysis By GitHub"*.

**Stap 4:** Github probeert automatisch het workflow bestand voor jouw project te configureren. Er staan veel dingen goed, maar er moeten een paar dingen gewijzigd worden.

- on: Zet hier de *schedule* naar een logische tijd. Er wordt gebruikgemaakt van de [POSIC cron syntax](https://pubs.opengroup.org/onlinepubs/9699919799/utilities/crontab.html#tag_20_25_07)

- on: Voeg hier ook "*workflow_dispatch*" toe, dit geeft je de mogelijkheid om de workflow handmatig af te vuren.

- strategy: Controleer hier of de language goed staat. Gebruik `csharp` en `javascript-typescript`.

**Stap 5:** Commit dit bestand.

Als je hebt gecommit naar je main branch, gaat de workflow automatisch runnen. Je kunt de voortgang zien bij actions --> CodeQL.

**Stap 6:** Als de workflow klaar is, kun je de resultaten vinden onder het *🛡️Security* Tabje van GitHub. Klik op Code scanning om de resultaten te zien.

**Stap 7:** Klik een item aan om hier meer informatie over in te zien. Er wordt getoond welke fout is gevonden, waar dit in de code staat en meer informatie. Bij een groot aantal problemen zijn er referenties naar externe resources die het probleem dieper uitleggen en aangeven hoe dit opgelost kan worden.

**Stap 8:** Kies wat je met het gevonden probleem gaat doen. Kies ervoor om de alert te negeren ("Dismiss alert") of een issue aan te maken.

**✔️ opdracht 2 is klaar!**

## Opdracht 3: Live website analyseren

Op het internet bestaan er verschillende tools om te kijken of er informatie over je website te vinden is die eigenlijk niet zichtbaar moet zijn. In deze opdracht kijken we naar [pentest-tools](https://pentest-tools.com/) en [ssl labs](https://www.ssllabs.com/).

**Stap 1:** Pentest-tools heeft verschillende scans om op je website te proberen. We starten met de [Website Vulnerability Scanner](https://pentest-tools.com/website-vulnerability-scanning/website-scanner). Deze tool scant op XSS, SQL injection, Command injection, XXE en andere mogelijke problemen. Klik op de link om te starten.

**Stap 2:** Voer de url van je eigen website in (YOURNAME.hbo-ict.org) en klik op ▶️*Start scan*.

**Stap 3:** Maak een screenshot, deze kun je in het portfolio gebruiken of later vergelijken met een nieuwe scan.

**Stap 4:** Volg dezelfde stappen met de [Network Vulnerability Scanner](https://pentest-tools.com/network-vulnerability-scanning/network-security-scanner-online-openvas). Deze tool scant op Log4Shell, OMIGOD, ProxyShell en andere security issues.

**Stap 5:** Je kunt dezelfde stappen volgen met [ssl labs](https://www.ssllabs.com/ssltest/). Deze scan probeert ook diepere informatie te vinden en kan daarom ook langer duren.

**✔️ opdracht 3 is klaar!**

## Resources

- [Github CodeQl documentatie](https://codeql.github.com/docs/)
- [Deepsource](https://deepsource.com) is een statische code analyseer tool, gratis voor persoonlijke projecten. Deepsource is niet open source, maar is wel een goed alternatief op Sonarqube.
- [Codegrip](https://www.codegrip.tech/) voor automatische code reviews.
- [Watermelon tools](https://www.watermelontools.com/) is een large language model die je code analyseert en een statische code analyse uitvoert.
[Asvs for dummies](https://asvs-for-dummies.pages.dev/) kun je gebruiken om bij te houden welke securitymaatregelen je al aangepakt hebt en welke informatie hierover te vinden is.

## Vandaag voltooide taken

- Een workflow toegevoegd om dependencies up to date te houden.
- Een workflow toegevoegd om de applicatie te scannen op veiligheidsrisico's.
