# Bitrovas Data Marketplace

Machine-readable data marketplace and agent-commerce reference system where AI agents can discover, price, pay for, and consume datasets and services using Bitcoin Lightning.

This public repository is the lightweight discovery/marketing mirror for the Bitrovas ecosystem. The production implementation lives elsewhere, but the canonical public entry points are stable and machine-readable.

## Quick links

### Core ecosystem
- Root: https://bitrovas.ch
- Bitrovas Handshake Protocol v0.1: https://bitrovas.ch/handshake-protocol-v0-1.html
- Ecosystem handshake JSON: https://bitrovas.ch/.well-known/bitrovas.json

### Marketplace
- Marketplace: https://data.bitrovas.ch/marketplace
- Catalog (human + JSON): https://data.bitrovas.ch/catalog
- Docs: https://data.bitrovas.ch/docs
- Handshake docs: https://data.bitrovas.ch/docs/handshake
- Agent quickstart: https://data.bitrovas.ch/agent-quickstart
- Marketplace handshake JSON: https://data.bitrovas.ch/.well-known/bitrovas.json
- Legacy datamesh JSON: https://data.bitrovas.ch/.well-known/datamesh.json
- Human discovery (HTML): https://data.bitrovas.ch/.well-known/datamesh.html
- OpenAPI: https://data.bitrovas.ch/openapi.json

### Clawrence
- Clawrence overview: https://clawrence.bitrovas.ch
- Clawrence handshake JSON: https://clawrence.bitrovas.ch/.well-known/bitrovas.json
- Clawrence agent.json: https://clawrence.bitrovas.ch/agent.json
- Example service (structure extract): https://clawrence.bitrovas.ch/api/structure-extract/ui

## Bitrovas Handshake Protocol v0.1

Bitrovas now exposes a public handshake standard so external AI agents do not need custom glue code for every page or service.

### Handshake phases
1. **Discovery**
2. **Capability description**
3. **Pricing**
4. **Payment**
5. **Fulfillment**
6. **Error handling**
7. **Trust / metadata**

### Canonical rule
Every AI agent **should start** with the handshake discovery endpoint:

```bash
curl https://data.bitrovas.ch/.well-known/bitrovas.json
```

This returns the machine-readable entry point for:
- service name
- service type
- version
- provider
- payment method
- supported flows
- endpoints
- input/output schema references
- pricing model
- preview / free-tier semantics
- example requests / responses

## Two service families under one standard

### 1) Marketplace / data products
The marketplace uses the handshake for:
- catalog discovery
- product manifests
- invoice creation
- payment status polling
- download fulfillment

Typical flow:

```bash
curl https://data.bitrovas.ch/.well-known/bitrovas.json
curl -H 'Accept: application/json' https://data.bitrovas.ch/catalog
curl -X POST https://data.bitrovas.ch/invoice \
  -H 'Content-Type: application/json' \
  -d '{"dataset":"world_countries_codes","version":"2026-03-09","format":"json"}'
curl 'https://data.bitrovas.ch/payment_status?payment_hash=PAYMENT_HASH'
curl -L 'https://data.bitrovas.ch/download?payment_hash=PAYMENT_HASH&format=json' -o dataset.json
```

### 2) Clawrence / agent services
Clawrence uses the same handshake logic for preview-first, Lightning-unlocked services.

Typical flow:

```bash
curl https://clawrence.bitrovas.ch/.well-known/bitrovas.json
curl -X POST https://clawrence.bitrovas.ch/api/structure-extract/preview \
  -H 'Content-Type: application/json' \
  -d '{"text":"Max Muster ...","attributes":["Vorname","Nachname","Geburtsdatum"]}'
curl -X POST https://clawrence.bitrovas.ch/api/structure-extract/invoice
curl 'https://clawrence.bitrovas.ch/api/structure-extract/status?payment_hash=PAYMENT_HASH'
curl -X POST https://clawrence.bitrovas.ch/api/structure-extract/run \
  -H 'Content-Type: application/json' \
  -d '{"payment_hash":"PAYMENT_HASH","text":"...","attributes":["Vorname","Nachname","Geburtsdatum"]}'
```

## Repository purpose (important)

This **public repository is used for discovery and marketing only**.

It contains public machine-readable or human-readable artifacts such as:
- `datasets.json`
- `agent.json`
- `datasets/*.md`

The **production marketplace and Clawrence implementation remain outside this public mirror** and are not fully reproduced here.
