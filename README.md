# LLM Repository

Canonical JSON‑LD schemas and examples for IXO Domains and LLM‑org records.

## Overview

This repository provides JSON-LD schema templates for different types of IXO domain entities. These schemas define standardized formats for representing decentralized entities in a machine-readable way that's compatible with schema.org and other semantic web standards.

## Repository Structure

- `domainCard.jsonld
- domainCard_IXOWorldTest.jsonld
- GPT_Prompt
  
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

