# LLM Repository

Canonical JSON‑LD schemas and examples for IXO Domains and LLM‑org records.

## Overview

This repository provides JSON-LD schema templates for different types of IXO domain entities. These schemas define standardized formats for representing decentralized entities in a machine-readable way that's compatible with schema.org and other semantic web standards.

## Repository Structure

- `Domain Cards/` — Example JSON-LD templates for domain types:
  - `Domain_Profile_dao.jsonld` - DAO profile template
  - `Domain_Profile_group` - Group entity template
  - `DomainProfile_asset.jsonld` - Digital/physical asset template
  - `DomainProfile_deed.jsonld` - Deed ownership record template
  - `DomainProfile_oracle.jsonld` - Oracle service template
  - `DomainProfile_pod.jsonld` - Persistent operational domain template
  - `DomainProfile_project.jsonld` - Project entity template
  - `DomainProfile_protocol.jsonld` - Protocol specification template

## Domain Schemas

Each domain template follows JSON-LD 1.1 standards and includes:

- Entity identification (`id`, `type`, `name`, `description`)
- Web presence and social identifiers
- Contact information
- Relationships with other entities
- Research profile for LLM context generation
- Domain-specific properties

## JSON-LD Guidelines

- Use explicit `@context` in all documents
- Map `id` → `@id` and `type` → `@type` in context
- Use absolute IRIs for identifiers; avoid relative paths
- Use ISO-8601 for dates
- Use BCP-47 for language codes
- Only use whitelisted contexts

## Usage

These schemas provide templates for creating domain profiles that can be used as context by LLMs. Replace placeholder values `<<<text>>>` with actual entity data to create valid instances.

## License

This project is licensed under the MIT License - see the LICENSE file for details.
