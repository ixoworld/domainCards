# Contributing to LLM Repository

Thank you for considering contributing to the LLM Repository! This document provides guidelines and instructions for contributing to this project.

## Getting Started

1. **Fork the Repository**: Start by forking the repository to your GitHub account.

2. **Clone Your Fork**: Clone your forked repository to your local machine.

```bash
git clone https://github.com/your-username/llm.git
cd llm
```

3. **Create a Branch**: Create a branch for your contribution.

```bash
git checkout -b feature/your-feature-name
```

## Guidelines for JSON-LD Examples

When contributing new JSON-LD examples or modifying existing ones, please adhere to these guidelines:

1. **Follow JSON-LD 1.1 Standards**:
   - Include explicit `@context` in all documents
   - Use absolute IRIs for identifiers
   - Follow the context mapping pattern (`id` → `@id`, `type` → `@type`)

2. **Use Placeholder Values**:
   - Use the `<<<placeholder>>>` format for variable content
   - Provide clear and descriptive placeholder names

3. **Domain Consistency**:
   - Ensure new domain examples are consistent with existing patterns
   - Include all required fields (id, type, name, description, etc.)
   - Add appropriate research profile sections for LLM context

4. **JSON Formatting**:
   - Use 2-space indentation
   - UTF-8 encoding only
   - LF (Unix-style) line endings

## Submitting Changes

1. **Commit Your Changes**:
   - Write clear, concise commit messages
   - Reference relevant issues in commit messages when applicable

2. **Push to Your Fork**:
```bash
git push origin feature/your-feature-name
```

3. **Create a Pull Request**:
   - Provide a clear description of the changes
   - Reference any related issues
   - Explain how your changes improve the repository

## Review Process

- All contributions will be reviewed by project maintainers
- Feedback may be provided for necessary changes
- Once approved, your contribution will be merged into the main branch

Thank you for contributing to the LLM Repository!
