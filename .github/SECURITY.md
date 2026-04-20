# Sikkerhedspolitik · FirmaAPI

FirmaAPI drives af **Briix Internet Company** (CVR 34824770), Mågevej 22, 2400 København NV.

Vi tager sikkerhed alvorligt og sætter pris på ansvarlig offentliggørelse af sårbarheder fundet i `firmaapi.dk`, vores API, eller relateret kildekode.

## Rapportér en sårbarhed

Send en e-mail til **kontakt@firmaapi.dk** med:

- En beskrivelse af sårbarheden og dens potentielle effekt
- Trin til reproduktion (gerne en proof-of-concept)
- Dit navn/alias hvis du ønsker kreditering

Du kan også bruge GitHub's [private vulnerability reporting](https://github.com/serddk/firmaapi-cvrapi/security/advisories/new).

**Svartid:** Vi bekræfter din rapport inden for **3 hverdage** og giver statusopdatering senest **14 dage** efter.

## Scope

**In scope:**
- `firmaapi.dk` og alle subdomæner
- FirmaAPI REST API (`api.firmaapi.dk` / `firmaapi.dk/api`)
- Officielle klientbiblioteker og MCP-server publiceret under `@firmaapi`

**Out of scope:**
- Tredjepartstjenester vi integrerer med (CVR-registret, Datafordeleren, Virk.dk)
- Social engineering af vores ansatte eller kunder
- Denial-of-service (DoS/DDoS) angreb
- Fysiske angreb mod infrastruktur
- Automatiserede scanner-rapporter uden manuel verificering

## Safe Harbor

Vi forfølger ikke juridiske krav mod sikkerhedsforskere der:

- Handler i god tro og undgår krænkelse af privatliv, dataødelæggelse og serviceafbrydelser
- Kun tilgår egne testkonti eller data fra kontoindehavere der har givet samtykke
- Giver os rimelig tid til at rette sårbarheden før offentliggørelse
- Overholder dansk og EU-lovgivning

## Anerkendelse

Forskere der rapporterer gyldige sårbarheder ansvarligt krediteres (efter ønske) i vores [security advisories](https://github.com/serddk/firmaapi-cvrapi/security/advisories) på GitHub.

---

*Senest opdateret: 2026-04-20*
