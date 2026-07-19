# Documentation

Directives for keeping documentation accurate and aligned with actual behavior.

## README

- Update the README only when it documents something that actually changed: installation, usage, configuration, or commands.
- Do not add README content for internal implementation details no user or developer needs.

## Accuracy of Instructions

- Configuration, usage, and development instructions in docs must remain accurate and runnable.
- Verify documented commands actually work as written before leaving them in place — do not document an assumed or aspirational command.

## Changelog

- Add a changelog entry when the repository maintains one and the change is user-facing.
- Do not introduce a changelog into a repository that doesn't already have one.
- Follow the existing changelog's format and tone exactly.

## Architecture Decision Records (ADRs)

- Write a short ADR for significant architectural decisions only when the repository already has an established ADR convention or directory.
- Do not introduce ADRs into a repository that doesn't use them.

## General Principle

- Keep documentation aligned with observable behavior, not internal implementation details.
- Document what a user or developer needs to know to use or work on the system — nothing more, nothing stale.
