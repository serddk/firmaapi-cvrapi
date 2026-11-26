# FirmaAPI — Dansk CVR API for udviklere

Den hurtigste vej til dansk virksomhedsdata. CVR-opslag, regnskaber, ejere, personrelationer og meget mere via en moderne REST API.

**[firmaapi.dk](https://firmaapi.dk)** · [Dokumentation](https://firmaapi.dk/dokumentation) · [Priser](https://firmaapi.dk/priser) · [Opret gratis konto](https://firmaapi.dk/register)

---

## Hvad er FirmaAPI?

FirmaAPI er en dansk REST API der giver adgang til data om 2+ millioner danske virksomheder fra det Centrale Virksomhedsregister (CVR). API'en er bygget til udviklere og virksomheder der har brug for pålidelig, hurtig virksomhedsdata.

- **Under 50ms** gennemsnitlig server-responstid
- **Alle selskabsformer** — A/S, ApS, IVS, enkeltmandsvirksomheder, foreninger m.fl.
- **Regnskabsdata** med nøgletal og vækstberegninger
- **Ejere og ledelse** med historik
- **Personprofiler** — find alle virksomhedstilknytninger for en person
- **Webhooks** — få besked når virksomheder ændrer status, fusionerer eller går konkurs
- **MCP-server** — giv din AI-assistent direkte adgang til CVR-data

## Hurtig start

### 1. Hent en API-nøgle

Opret en gratis konto på [firmaapi.dk/register](https://firmaapi.dk/register). Du får en API-nøgle der starter med `cvr_live_`.

### 2. Lav dit første opslag

```bash
curl -H "X-API-Key: cvr_live_din_nøgle" \
  https://firmaapi.dk/api/v1/company/10150817
```

### 3. Se resultatet

```json
{
  "cvr": "10150817",
  "name": "LEGO System A/S",
  "address": "Aastvej 1",
  "zipcode": "7190",
  "city": "Billund",
  "status": "aktiv",
  "company_type": "Aktieselskab",
  "industry": "Fremstilling af spil og legetøj",
  "employees": "ANTAL_ANSATTE_INTERVAL_10000+",
  "founded": "1981-01-05",
  "phone": "79506070",
  "email": "LEGO@LEGO.com",
  "website": "http://www.LEGO.com",
  "owners": [...],
  "management": [...],
  "...": "..."
}
```

## Endpoints

| Endpoint | Beskrivelse | Plan |
|----------|-------------|------|
| `GET /api/v1/company/{cvr}` | Opslag på CVR-nummer | Gratis |
| `GET /api/v1/company/search?q={query}` | Søg virksomheder på navn | Gratis |
| `GET /api/v1/search/advanced` | Avanceret søgning med 19+ filtre | Gratis |
| `POST /api/v1/company/batch` | Batch-opslag af flere CVR-numre | Basis |
| `GET /api/v1/production-unit/{p}` | Opslag på P-nummer | Standard |
| `GET /api/v1/person/{id}` | Personprofil med tilknytninger | Professionel |
| `GET /api/v1/person/search?q={query}` | Søg efter personer | Professionel |
| `GET /api/v1/industries` | Branchekoder (DB07) | Gratis |
| `GET /api/v1/municipalities` | Kommuneliste med koder | Gratis |
| `GET/POST/PATCH/DELETE /api/v1/webhooks` | Webhook-administration | Standard |

Se fuld API-reference i [dokumentationen](https://firmaapi.dk/dokumentation).

## Autentifikation

Send din API-nøgle i headeren:

```
X-API-Key: cvr_live_din_nøgle
```

eller

```
Authorization: Bearer cvr_live_din_nøgle
```

## Kodeeksempler

### JavaScript / Node.js

```javascript
const response = await fetch("https://firmaapi.dk/api/v1/company/10150817", {
  headers: { "X-API-Key": "cvr_live_din_nøgle" },
});

const company = await response.json();
console.log(company.name); // "LEGO System A/S"
```

### Python

```python
import requests

response = requests.get(
    "https://firmaapi.dk/api/v1/company/10150817",
    headers={"X-API-Key": "cvr_live_din_nøgle"},
)

company = response.json()
print(company["name"])  # "LEGO System A/S"
```

### PHP

```php
$ch = curl_init("https://firmaapi.dk/api/v1/company/10150817");
curl_setopt($ch, CURLOPT_HTTPHEADER, ["X-API-Key: cvr_live_din_nøgle"]);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

$company = json_decode(curl_exec($ch), true);
echo $company["name"]; // "LEGO System A/S"
```

### C# / .NET

```csharp
using var client = new HttpClient();
client.DefaultRequestHeaders.Add("X-API-Key", "cvr_live_din_nøgle");

var response = await client.GetAsync("https://firmaapi.dk/api/v1/company/10150817");
var company = await response.Content.ReadFromJsonAsync<JsonElement>();

Console.WriteLine(company.GetProperty("name").GetString()); // "LEGO System A/S"
```

### Go

```go
req, _ := http.NewRequest("GET", "https://firmaapi.dk/api/v1/company/10150817", nil)
req.Header.Set("X-API-Key", "cvr_live_din_nøgle")

resp, _ := http.DefaultClient.Do(req)
defer resp.Body.Close()

var company map[string]interface{}
json.NewDecoder(resp.Body).Decode(&company)
fmt.Println(company["name"]) // "LEGO System A/S"
```

## Avanceret søgning

Find virksomheder med præcise filtre:

```bash
# Alle aktive IT-virksomheder i København med omsætning over 10 mio
curl -H "X-API-Key: cvr_live_din_nøgle" \
  "https://firmaapi.dk/api/v1/search/advanced?city=København&industry=620100&revenue_min=10000000&status=aktiv"
```

Tilgængelige filtre: `city`, `zipcode`, `municipality`, `industry`, `company_type`, `status`, `employees`, `revenue_min`, `revenue_max`, `capital_min`, `capital_max`, `founded_after`, `founded_before`, `has_financials`, `ad_protected`, `has_phone`, `has_email`, `has_website`.

Se alle parametre i [dokumentationen](https://firmaapi.dk/dokumentation).

## Regnskabsdata

Hent regnskaber med nøgletal og vækstberegninger via `include=finance`:

```bash
curl -H "X-API-Key: cvr_live_din_nøgle" \
  "https://firmaapi.dk/api/v1/company/10150817?include=finance"
```

Returnerer bl.a. omsætning, resultat, egenkapital, aktiver, soliditetsgrad, afkastningsgrad, overskudsgrad og år-over-år vækst.

## Webhooks

Få besked i realtid når virksomheder ændrer sig. Understøttede hændelser:

- Statusændringer (aktiv → ophørt)
- Konkurser og tvangsopløsninger
- Fusioner og spaltninger
- Adresseændringer
- Brancheændringer
- Ejerskifter
- Navneændringer

```bash
curl -X POST -H "X-API-Key: cvr_live_din_nøgle" \
  -H "Content-Type: application/json" \
  -d '{"url": "https://din-app.dk/webhook", "event_types": ["status_change", "bankruptcy"]}' \
  https://firmaapi.dk/api/v1/webhooks
```

Se webhook-dokumentation på [firmaapi.dk/dokumentation](https://firmaapi.dk/dokumentation).

## AI-integration (MCP)

FirmaAPI har en officiel [MCP-server](https://firmaapi.dk/dokumentation) der giver AI-assistenter direkte adgang til CVR-data. Understøtter Claude Desktop, Claude Code, Cursor og andre MCP-kompatible klienter.

Hurtigst er den hostede server: tilføj `https://firmaapi.dk/mcp` som connector i din AI-klient og log ind med din FirmaAPI-konto. Ingen API-nøgle og ingen installation.

```bash
# Claude Code
claude mcp add --transport http firmaapi https://firmaapi.dk/mcp

# Eller som plugin med connector og skills
/plugin marketplace add serddk/firmaapi-cvrapi
/plugin install firmaapi@firmaapi
```

Vil du hellere køre serveren lokalt med en API-nøgle:

```bash
npx firmaapi-mcp-server
```

Se den fulde [MCP-opsætningsguide](MCP.md) for begge muligheder.

Læs mere: [npm-pakke](https://www.npmjs.com/package/firmaapi-mcp-server) · [MCP-opsætningsguide](MCP.md)

## Priser

Se aktuelle planer, priser og features på [firmaapi.dk/priser](https://firmaapi.dk/priser).

## Links

- [firmaapi.dk](https://firmaapi.dk) — Hjemmeside
- [Dokumentation](https://firmaapi.dk/dokumentation) — Fuld API-reference
- [Priser](https://firmaapi.dk/priser) — Planer og features
- [Opret konto](https://firmaapi.dk/register) — Gratis at komme i gang
- [OpenAPI spec](https://firmaapi.dk/api/openapi) — Maskinlæsbar API-specifikation
- [LLM-reference](https://firmaapi.dk/llms.txt) — Til AI-integration
- [Status](https://firmaapi.dk/status) — Oppetid og systemstatus
- [Blog](https://firmaapi.dk/blog) — Nyheder og artikler
- [FAQ](https://firmaapi.dk/faq) — Ofte stillede spørgsmål
- [MCP-server (npm)](https://www.npmjs.com/package/firmaapi-mcp-server) — AI-assistent integration

## Licens

MIT
