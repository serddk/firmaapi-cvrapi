# FirmaAPI til Claude

Danske virksomhedsdata fra CVR-registret direkte i Claude: stamdata, regnskaber, ejere, ledelse, personer og produktionsenheder.

## Det får du

- **34 værktøjer** via FirmaAPI's hostede MCP-server (`https://firmaapi.dk/mcp`): opslag, søgning med 30+ filtre, regnskabstal, ejerkæder, markedsanalyse og mere.
- **3 skills**, der lærer Claude at bruge værktøjerne til hele opgaver:
  - `firmaapi-virksomhedsoversigt`: faktuel oversigt over en virksomhed før et møde eller en aftale.
  - `firmaapi-leadliste`: liste over virksomheder, der matcher en kundeprofil.
  - `firmaapi-ejerkaede`: hvem der ejer en virksomhed, gennem holdingselskaber og koncernstruktur.

## Sådan kommer du i gang

1. Installer pluginet.
2. Første gang Claude bruger FirmaAPI, bliver du bedt om at logge ind med din FirmaAPI-konto og godkende adgangen. Har du ingen konto, kan du oprette en gratis undervejs.

Der er ingen API-nøgle at kopiere. Claude bruger din plan og din månedlige kvote, og du kan til enhver tid fjerne adgangen under Forbundne apps i dit dashboard på [firmaapi.dk/dashboard](https://firmaapi.dk/dashboard).

## Data og privatliv

Pluginet sender de forespørgsler, Claude laver på dine vegne, til FirmaAPI. Oplysningerne er offentlige registerdata fra Erhvervsstyrelsen. FirmaAPI kan ikke se dine samtaler. Privatlivspolitik: [firmaapi.dk/privatlivspolitik](https://firmaapi.dk/privatlivspolitik).

Oplysningerne er registerdata og beregnede nøgletal, ikke vurderinger eller anbefalinger. Virksomheder kan være reklamebeskyttede; hvordan du bruger oplysningerne, er dit ansvar.

## Hjælp

- Vejledning: [firmaapi.dk/mcp](https://firmaapi.dk/mcp)
- Dokumentation: [firmaapi.dk/dokumentation](https://firmaapi.dk/dokumentation)
- Priser og planer: [firmaapi.dk/priser](https://firmaapi.dk/priser)

## Installation i Claude Code

```
/plugin marketplace add serddk/firmaapi-cvrapi
/plugin install firmaapi@firmaapi
```
