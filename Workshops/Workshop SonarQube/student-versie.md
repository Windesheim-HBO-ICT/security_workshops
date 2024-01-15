# Workshop SonarQube

## Voorwaarden deelname

TODO

Alternatieven op sonarqube:

- <https://deepsource.com>
- <https://www.codegrip.tech/>
- <https://www.watermelontools.com/>

## Beschrijving

Er zijn veel externe veiligheids analyse tools beschikbaar om de veiligheid van je applicatie bij te houden. In deze workshop kijken we naar een aantal tools en wordt er beschreven hoe je deze kunt gebruiken.

## Eindresultaat

Na het afronden van de workshop beschik je over het volgende eindresultaat:

- TODO

## Notes

- TODO

## Opdracht 1: Automatisch updaten van dependencies

Om je applicatie veilig te houden is het belangrijk om regelmatig updates uit te voeren. Het makkelijkste is om dit te automatiseren, door bijvoorbeeld gebruik te maken van Github actions.

In deze opdracht ga je een eigen workflow toevoegen waarmee je automatisch je dependencies kunt updaten.

**Stap 1:** Zoek een action die bij je type project past. Voor dotnet zou je bijvoorbeeld <https://github.com/marketplace/actions/dotnet-dependency-update> kunnen gebruiken.

Voor iets anders dan dotnet kun je zoeken op dependency update: <https://github.com/marketplace?category=&type=actions&verification=&query=dependency+update>

**Stap 2:** In je eigen project maak de folder structuur \<Projectroot\>/.github/workflows/DependencyUpdater.yml

**Stap 3:** In het DependencyUpdater.yml bestand plak je de code die bij Usage vermeld staan. Probeer het moment waarop de action runt naar een logische waarde te wijzigen.

**Stap 4:** Test de action door deze eenmalig handmatig te runnen.

**✔️ opdracht 1 is klaar!**

## Vandaag voltooide taken

- TODO
