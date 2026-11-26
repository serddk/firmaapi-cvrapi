# FirmaAPI MCP Server — Opsætningsguide

Giv din AI-assistent direkte adgang til dansk virksomhedsdata fra [FirmaAPI](https://firmaapi.dk) via Model Context Protocol (MCP).

MCP-serveren lader AI-assistenter som Claude Desktop, Claude Code og Cursor slå virksomheder op, søge i CVR-registret, hente regnskaber, finde ejere og meget mere — uden at du selv skal skrive API-kald.

## Hurtigst: log ind, ingen API-nøgle

MCP-serveren kører hostet på `https://firmaapi.dk/mcp`. Tilføj adressen som connector i din AI-klient og log ind med din FirmaAPI-konto. Der er intet at installere, og kaldene bruger din plan og kvote som ellers.

**Claude (web, computer og mobil):** Settings, Connectors, Add custom connector. Indsæt `https://firmaapi.dk/mcp` og klik Connect.

**Claude Code:**

```bash
claude mcp add --transport http firmaapi https://firmaapi.dk/mcp
```

Skriv derefter `/mcp` i Claude Code og log ind.

**Claude Code som plugin** (connector og tre skills i ét):

```
/plugin marketplace add serddk/firmaapi-cvrapi
/plugin install firmaapi@firmaapi
```

**Cursor:** tilføj til `.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "firmaapi": { "url": "https://firmaapi.dk/mcp" }
  }
}
```

Forbundne apps kan du se og fjerne i dit [dashboard](https://firmaapi.dk/dashboard). Flere klienter: [firmaapi.dk/mcp](https://firmaapi.dk/mcp#installation).

Resten af guiden beskriver den lokale server med API-nøgle, til scripts, servere og klienter uden login.

## Forudsætninger

- **Node.js 20+** installeret
- En **FirmaAPI API-nøgle** — [opret gratis konto](https://firmaapi.dk/register)

## Installation

### Claude Desktop

Tilføj til din `claude_desktop_config.json`:

**macOS:** `~/Library/Application Support/Claude/claude_desktop_config.json`
**Windows:** `%APPDATA%\Claude\claude_desktop_config.json`

```json
{
  "mcpServers": {
    "firmaapi": {
      "command": "npx",
      "args": ["-y", "firmaapi-mcp-server"],
      "env": {
        "FIRMAAPI_KEY": "cvr_live_din_nøgle_her"
      }
    }
  }
}
```

Genstart Claude Desktop efter ændringen.

### Claude Code

```bash
claude mcp add firmaapi -e FIRMAAPI_KEY=cvr_live_din_nøgle_her -- npx -y firmaapi-mcp-server
```

### Cursor

Tilføj til `.cursor/mcp.json` i dit projekt:

```json
{
  "mcpServers": {
    "firmaapi": {
      "command": "npx",
      "args": ["-y", "firmaapi-mcp-server"],
      "env": {
        "FIRMAAPI_KEY": "cvr_live_din_nøgle_her"
      }
    }
  }
}
```

### Windsurf

Tilføj til din MCP-konfiguration:

```json
{
  "mcpServers": {
    "firmaapi": {
      "command": "npx",
      "args": ["-y", "firmaapi-mcp-server"],
      "env": {
        "FIRMAAPI_KEY": "cvr_live_din_nøgle_her"
      }
    }
  }
}
```

### Andre MCP-klienter

Enhver MCP-kompatibel klient kan bruge serveren. Konfigurationen er den samme:

- **Command:** `npx`
- **Args:** `["-y", "firmaapi-mcp-server"]`
- **Environment:** `FIRMAAPI_KEY=cvr_live_...`

## Tilgængelige tools

MCP-serveren eksponerer 9 tools som din AI-assistent kan bruge:

### firmaapi_lookup_company

Slå en virksomhed op via CVR-nummer.

| Parameter | Type | Beskrivelse |
|-----------|------|-------------|
| `cvr` | string | 8-cifret CVR-nummer (påkrævet) |
| `include` | string | Kommasepareret: `finance`, `history`, `events`, `production_units`, `relations` |

Returnerer stamdata, adresse, kontaktinfo, branche, ejere, ledelse, revisorer og meget mere. Brug `include` for ekstra datablokke som regnskaber, historik og koncernrelationer.

### firmaapi_search_companies

Søg virksomheder på navn eller nøgleord.

| Parameter | Type | Beskrivelse |
|-----------|------|-------------|
| `query` | string | Søgestreng, min. 2 tegn (påkrævet) |
| `limit` | number | Maks resultater, 1–100 (default 10) |

### firmaapi_advanced_search

Avanceret søgning med 19+ filtre — by, branche, omsætning, ansatte, selskabsform, kommune, reklamebeskyttelse og meget mere.

| Parameter | Type | Beskrivelse |
|-----------|------|-------------|
| `q` | string | Navnesøgning (brug `*` for alle) |
| `city` | string | Bynavn |
| `zipcode` | string | Postnummer |
| `municipality` | string | Kommunenavn eller -kode |
| `industry` | string | Branchekode eller branchetekst |
| `company_type` | string | Selskabsform, fx `ApS`, `A/S` |
| `status` | string | `aktiv`, `ophoert` m.fl. |
| `employees` | string | Interval, fx `10-49`, `100+` |
| `revenue_min` / `revenue_max` | number | Omsætningsinterval i DKK |
| `capital_min` / `capital_max` | number | Selskabskapital i DKK |
| `founded_after` / `founded_before` | string | Stiftelsesdato (YYYY-MM-DD) |
| `has_financials` | boolean | Kun med regnskabsdata |
| `ad_protected` | string | Reklamebeskyttelse |
| `has_phone` / `has_email` / `has_website` | boolean | Kontaktfiltre |
| `limit` | number | Maks resultater (default 20) |
| `offset` | number | Pagination offset |

### firmaapi_batch_lookup

Slå flere virksomheder op på én gang. Kræver [Basis-plan](https://firmaapi.dk/priser) eller højere.

| Parameter | Type | Beskrivelse |
|-----------|------|-------------|
| `cvr_numbers` | string | Kommasepareret liste af CVR-numre (påkrævet) |

### firmaapi_get_person

Hent en personprofil med alle virksomhedstilknytninger. Kræver [Professionel-plan](https://firmaapi.dk/priser).

| Parameter | Type | Beskrivelse |
|-----------|------|-------------|
| `id` | string | Person UUID (påkrævet) |

### firmaapi_search_persons

Søg efter personprofiler på navn. Kræver [Professionel-plan](https://firmaapi.dk/priser).

| Parameter | Type | Beskrivelse |
|-----------|------|-------------|
| `query` | string | Personnavn, min. 2 tegn (påkrævet) |
| `limit` | number | Maks resultater, 1–50 (default 10) |

### firmaapi_production_unit

Slå produktionsenhed op via P-nummer. Kræver [Standard-plan](https://firmaapi.dk/priser).

| Parameter | Type | Beskrivelse |
|-----------|------|-------------|
| `p_number` | string | 10-cifret P-nummer (påkrævet) |

### firmaapi_industries

Hent danske branchekoder (DB07) med hierarki og antal virksomheder.

| Parameter | Type | Beskrivelse |
|-----------|------|-------------|
| `filter` | string | Filtrer på navn eller kode |

### firmaapi_municipalities

Hent danske kommuner med koder.

| Parameter | Type | Beskrivelse |
|-----------|------|-------------|
| `filter` | string | Filtrer på kommunenavn |

## Eksempler på brug

Når MCP-serveren er konfigureret, kan du bede din AI-assistent om:

- *"Slå Novo Nordisk op og vis deres seneste regnskab"*
- *"Find alle aktive IT-virksomheder i Aarhus med omsætning over 10 millioner"*
- *"Hvem ejer CVR 34824770?"*
- *"Vis koncernrelationer for Dansk Supermarked"*
- *"Find alle virksomheder Lars Larsen er tilknyttet"*
- *"Vis alle ikke-reklamebeskyttede virksomheder stiftet i dag"*
- *"Slå disse CVR-numre op på én gang: 24256790, 10150817"*
- *"Find branchekoden for IT-konsulenter"*
- *"Hvilke kommuner findes der i Region Nordjylland?"*
- *"Sammenlign regnskaberne for de 5 største revisionshuse"*

## Planer og adgang

Forskellige MCP-tools kræver forskellige planer:

| Tool | Mindste plan |
|------|-------------|
| `firmaapi_lookup_company` | Gratis |
| `firmaapi_search_companies` | Gratis |
| `firmaapi_advanced_search` | Gratis |
| `firmaapi_industries` | Gratis |
| `firmaapi_municipalities` | Gratis |
| `firmaapi_batch_lookup` | Basis (79 kr/md) |
| `firmaapi_production_unit` | Standard (299 kr/md) |
| `firmaapi_get_person` | Professionel (899 kr/md) |
| `firmaapi_search_persons` | Professionel (899 kr/md) |

Regnskabsdata via `include=finance` kræver Standard-plan. Se alle planer på [firmaapi.dk/priser](https://firmaapi.dk/priser).

## Links

- [firmaapi.dk](https://firmaapi.dk) — Hjemmeside
- [Dokumentation](https://firmaapi.dk/dokumentation) — Fuld API-reference med MCP-sektion
- [Opret konto](https://firmaapi.dk/register) — Gratis at komme i gang
- [npm-pakke](https://www.npmjs.com/package/firmaapi-mcp-server) — firmaapi-mcp-server
- [Blog](https://firmaapi.dk/blog) — Nyheder og artikler
- [Status](https://firmaapi.dk/status) — Oppetid og systemstatus
