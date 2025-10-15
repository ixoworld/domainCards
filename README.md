# IXO Domain Cards

LLM-usable, linked-data domain profiles for IXO digital twins — modeled as Verifiable Credentials (VC v2) in JSON‑LD 1.1.

> Domain Cards describe people, organizations, DAOs, projects, datasets, software, and services that operate as IXO “digital twins”. They are machine‑readable, verifiable, and referencable on the open Web and IXO networks.

---

## Contents

- What is a Domain Card
- Standards and compatibility
- Repository layout
- Quickstart
- Local validation
- Create a Domain Card (template)
- Recommended properties
- IXO-specific extensions
- Publishing and discovery
- LLM usage notes
- Security, privacy, and status
- Versioning policy
- Contributing, license, support

---

## What is a Domain Card

A Domain Card is a compact JSON‑LD document that:
- Identifies a real‑world entity with a DID.
- Links out to authoritative pages, datasets, code, and services.
- Provides rich semantics for LLMs and graph tools.
- Is packaged as a W3C Verifiable Credential (VC v2) and can be signed and status‑managed.

Use cases:
- Power agentic workflows (curation, RAG, orchestration).
- Index IXO entities and ecosystems into knowledge graphs.
- Provide verifiable profiles for registries, explorers, and apps.

---

## Standards and compatibility

- JSON‑LD 1.1, compacted documents with a stable `@context`.
- Verifiable Credentials Data Model v2.0 (`type: VerifiableCredential`).
- DID Core for identifiers (`credentialSubject.id` is a DID or URL).
- Proofs:
  - Data Integrity (`type: DataIntegrityProof`, e.g., `eddsa-rdfc-2022`), or
  - JOSE/COSE (VC‑JOSE‑COSE) for JWT/SD‑JWT/COSE formats.
- JSON Schema (draft 2020‑12) for data validation.
- Schema.org and PROV‑O for general semantics; IXO vocabulary for domain‑specific terms.

---

## Repository layout

Current
- `Data model/` — core models and examples
  - `domainCard.jsonld` — base model example
  - `Example/` — worked examples and assets
    - `domainCard-ixo-world.jsonld` — IXO World example
    - `domain-overview-ixoWorld.txt` — human‑readable overview
    - `Prompts/` — prompt assets for generating overviews/cards
- `schemas/` — JSON Schemas for Domain Cards
- `.github/workflows/validate.yml` — CI for schema and JSON‑LD checks
- `README.md` — this document
- `LICENSE` — MIT
- `CONTRIBUTING.md` — contribution guidelines

Recommended future additions
- `contexts/` — versioned JSON‑LD contexts for IXO terms
- `tools/` — helper scripts (validation, signing, verification)
- `tests/` — automated checks

---

## Quickstart

Prerequisites
- Node.js 18+
- npm (or pnpm/yarn)

Install useful tooling locally (optional but recommended):
```bash
npm i -D ajv ajv-formats ajv-cli jsonld-cli
```

---

## Local validation

JSON Schema (draft 2020‑12):

```bash
npx ajv validate -s schemas/ixo-domain-card-1.json -d "Data model/**/*.jsonld" --spec=draft2020
```

JSON‑LD lint/expand:

```bash
npx jsonld lint "Data model/**/*.jsonld"
npx jsonld expand "Data model/**/*.jsonld" > NUL
```

Optional canonize (useful before signing/diffing):

```bash
npx jsonld canonize "Data model/**/*.jsonld" > NUL
```

---

## Create a Domain Card (template)

Minimal, standards‑aligned template (VC v2 + JSON‑LD 1.1):

```json
{
  "@context": [
    "https://www.w3.org/ns/credentials/v2",
    "https://w3id.org/ixo/context/v1",
    {
      "schema": "https://schema.org/",
      "ixo": "https://w3id.org/ixo/vocab/v1",
      "prov": "http://www.w3.org/ns/prov#",
      "xsd": "http://www.w3.org/2001/XMLSchema#",
      "id": "@id",
      "type": "@type",
      "ixo:vector": { "@container": "@list", "@type": "xsd:double" },
      "@protected": true
    }
  ],
  "id": "did:ixo:example.org#dmn",
  "type": ["VerifiableCredential", "ixo:DomainCard"],
  "issuer": { "id": "did:ixo:issuer:example" },
  "validFrom": "2025-01-01T00:00:00Z",
  "credentialSchema": {
    "id": "https://example.org/schemas/ixo-domain-card-1.json",
    "type": "JsonSchema"
  },
  "credentialSubject": {
    "id": "did:ixo:entity:example",
    "type": ["ixo:EntityIdentity", "schema:Organization"],
    "name": "Example Domain",
    "url": "https://example.org",
    "sameAs": [
      "https://twitter.com/example",
      "https://github.com/example"
    ]
  }
}
```

Notes
- Use real, resolvable URLs for `url` and `sameAs`.
- Always set `credentialSubject.id` (DID or URL).
- Keep the `@context` list short and versioned.

---

## Recommended properties

Required
- `@context` includes VC v2 context.
- `type` includes `VerifiableCredential` and `ixo:DomainCard`.
- `issuer` (string DID or object with `id`).
- `validFrom`.
- `credentialSubject.id` (DID/URL).
- `credentialSchema` (JSON Schema URL and type).

Strongly recommended
- `url`, `sameAs[]`, `logo`/`image`.
- `keywords[]`, `knowsAbout[]`.
- `address`, `areaServed`, `contactPoint[]`.
- `composition.hasPart[]` with stable `id`s.
- `relationships` (memberships, partners, funding).
- `events[]`, `agents[]`.
- `researchProfile` with `seedQueries`, `citation`, and optional embeddings (use `@list` for ordered vectors).

---

## IXO-specific extensions (optional)

Define in the IXO context (`https://w3id.org/ixo/context/v1`) and document ranges:
- `ixo:chain` (e.g., `impacthub`, `testnet`)
- `ixo:daoId`
- `ixo:contractAddress` (CosmWasm)
- `ixo:tokenSymbol`, `ixo:tokenAddress`
- Treasury accounts or safe addresses
- Links to IXO Explorer pages

Prefer lowerCamelCase, stable meanings, and resolvable documentation URLs.

---

## Publishing and discovery

Recommended hosting
- Commit Domain Cards to this repo (or your domain repository).
- Also publish at a stable HTTPS URL (`Content-Type: application/vc+ld+json`).
- Optionally pin to IPFS and reference the CID from your DID Document or registry.

Discovery
- Link from your website footer and `humans.txt`.
- Add the card URL to your DID Document service endpoints.
- Register in IXO registries/indexers as needed.

Caching contexts
- Host IXO contexts via w3id and serve with long cache lifetimes; never change semantics of previously published terms.

---

## LLM usage notes

- Every major node (`credentialSubject`, `hasPart`, `agents`, `events`) should have an `id`.
- Prefer concise `name` + `description`, plus `keywords` and `knowsAbout`.
- Make external links resolvable and stable.
- Keep the `@context` minimal and versioned to avoid term drift.
- Avoid embedding documentation in instances; place documentation in schemas and this README.

---

## Security, privacy, and status

Proofs
- Data Integrity (`DataIntegrityProof` + cryptosuite, e.g., `eddsa-rdfc-2022`) or
- JOSE/COSE (JWT/SD‑JWT/COSE) per VC‑JOSE‑COSE.

Credential status (revocation/suspension)
- Add `credentialStatus` (e.g., Bitstring Status List); publish and update lists.

PII minimization
- Avoid unnecessary personal data. If needed, reference DPV terms and document processing purposes.

---

## Versioning policy

- Semantic Versioning for JSON Schemas and contexts.
- Never change the meaning of an existing context term; add new terms instead.
- Use `v1`, `v1.1`… paths for contexts; deprecate with clear guidance.

---

## Contributing, license, support

- See `CONTRIBUTING.md` for workflows and code style.
- License: MIT (`LICENSE`).
- Issues and discussions: GitHub Issues in this repository.

