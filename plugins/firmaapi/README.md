# FirmaAPI for Claude

Danish company data from the CVR register (the Danish Central Business Register) in Claude: master data, financial statements, owners, management, people and production units.

## In English

**What it does.** The plugin connects Claude to FirmaAPI's hosted MCP server at `https://firmaapi.dk/mcp` (34 read-only tools) and adds three skills that teach Claude to use them for whole tasks: a factual company overview, a lead list matching a customer profile, and an ownership chain. The skills are written in Danish, because the data and the users are Danish.

**Sign-in.** The first time Claude uses FirmaAPI you sign in with your FirmaAPI account (OAuth 2.1 with PKCE) and approve access. There is no API key to copy. A free account can be created during sign-in. You can remove access at any time under Forbundne apps in your dashboard at https://firmaapi.dk/dashboard.

**What it sends.** The plugin runs no code on your machine. It sends the tool calls Claude makes on your behalf (for example a CVR number or search filters) to `https://firmaapi.dk/mcp`, and nothing else. FirmaAPI does not receive your conversations. Calls count against the plan and monthly quota of your FirmaAPI account. The data returned is public register data from the Danish Business Authority. Privacy policy: https://firmaapi.dk/privatlivspolitik. Terms: https://firmaapi.dk/vilkaar. Contact: kontakt@firmaapi.dk.

The data is register data and calculated key figures, not assessments or recommendations.

## På dansk

Danske virksomhedsdata fra CVR-registret direkte i Claude: stamdata, regnskaber, ejere, ledelse, personer og produktionsenheder.

### Det får du

- **34 værktøjer** via FirmaAPI's hostede MCP-server (`https://firmaapi.dk/mcp`): opslag, søgning med 30+ filtre, regnskabstal, ejerkæder, markedsanalyse og mere.
- **3 skills**, der lærer Claude at bruge værktøjerne til hele opgaver:
  - `firmaapi-virksomhedsoversigt`: faktuel oversigt over en virksomhed før et møde eller en aftale.
  - `firmaapi-leadliste`: liste over virksomheder, der matcher en kundeprofil.
  - `firmaapi-ejerkaede`: hvem der ejer en virksomhed, gennem holdingselskaber og koncernstruktur.

### Sådan kommer du i gang

1. Installer pluginet.
2. Første gang Claude bruger FirmaAPI, bliver du bedt om at logge ind med din FirmaAPI-konto og godkende adgangen. Har du ingen konto, kan du oprette en gratis undervejs.

Der er ingen API-nøgle at kopiere. Claude bruger din plan og din månedlige kvote, og du kan til enhver tid fjerne adgangen under Forbundne apps i dit dashboard på [firmaapi.dk/dashboard](https://firmaapi.dk/dashboard).

### Data og privatliv

Pluginet sender de forespørgsler, Claude laver på dine vegne, til FirmaAPI. Oplysningerne er offentlige registerdata fra Erhvervsstyrelsen. FirmaAPI kan ikke se dine samtaler. Privatlivspolitik: [firmaapi.dk/privatlivspolitik](https://firmaapi.dk/privatlivspolitik).

Oplysningerne er registerdata og beregnede nøgletal, ikke vurderinger eller anbefalinger. Virksomheder kan være reklamebeskyttede; hvordan du bruger oplysningerne, er dit ansvar.

### Hjælp

- Vejledning: [firmaapi.dk/mcp](https://firmaapi.dk/mcp)
- Dokumentation: [firmaapi.dk/dokumentation](https://firmaapi.dk/dokumentation)
- Priser og planer: [firmaapi.dk/priser](https://firmaapi.dk/priser)

## Install in Claude Code

```
/plugin marketplace add serddk/firmaapi-cvrapi
/plugin install firmaapi@firmaapi
```
