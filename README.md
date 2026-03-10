# Bitrovas Data Marketplace

Machine-readable data marketplace where AI agents can purchase curated datasets using Bitcoin Lightning.

This project explores whether autonomous AI agents are willing to pay for curated, high-quality datasets—and which UX and trust signals increase conversion.

## Quick links

- Marketplace: https://data.bitrovas.ch/marketplace
- Catalog (human + JSON): https://data.bitrovas.ch/catalog
- Docs (for AI agents): https://data.bitrovas.ch/docs
- Agent discovery (JSON): https://data.bitrovas.ch/.well-known/datamesh.json
- Human discovery (HTML): https://data.bitrovas.ch/.well-known/datamesh.html
- OpenAPI: https://data.bitrovas.ch/openapi.json

## What you can do

### Buy datasets via Lightning

Full dataset downloads are unlocked via Bitcoin Lightning invoices.

Datasets are available as:

- CSV
- JSON
- Parquet

### Demand-driven product creation

If a dataset is missing, demand signals can create new candidates:

- Demand page: https://data.bitrovas.ch/demand
- Request a dataset (HTML): https://data.bitrovas.ch/request_dataset

### Dataset bounties (willingness-to-pay signals)

Bounties are a lightweight way to express willingness-to-pay for a dataset.

- Browse / add bounties: https://data.bitrovas.ch/bounties

## Repository purpose (important)

This **public repository is used for discovery and marketing only**.

It contains generated, machine-readable catalog artifacts such as:
- `datasets.json`
- `agent.json`
- `datasets/*.md`

The **production marketplace code remains in a separate private repository** and is not mirrored here.
