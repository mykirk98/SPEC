# Python Code Style Guide

> Rules for Python projects.

---

## Naming Conventions

- Variables, functions, methods: `snake_case`
- Constants: `SCREAMING_SNAKE_CASE`, defined after imports
- Classes: `PascalCase`; private attributes/methods: prefix `_`
- Booleans: must start with `is_`, `has_`, `can_`, or `should_`
- Type aliases & Protocols: `PascalCase`, defined at module level

---

## File & Module Structure

- Group code by layer with one-way dependencies, as defined in `design-principles.md`
- One class per file; trivial classes with no added methods (plain dataclasses, bare exception subclasses) may share a file
- Split tests into `unit/` and `integration/`, mirroring the source structure with a `test_` prefix (e.g. `foo/bar.py` → `tests/unit/foo/test_bar.py`)

---

## Tooling

- Formatter: `ruff format` — governs line length and wrapping
- Linter: `ruff check` — enforces the checkable rules in this guide; see `pyproject.toml` for the enabled rule set

---

## Type Annotations

- Always annotate function parameters and return types — no exceptions
- Use `from __future__ import annotations` at the top of every file
- Use `X | None` instead of `Optional[X]`, `X | Y` instead of `Union[X, Y]` (Python 3.10+)
- Never use `Any` — use `object` for truly unknown types, narrowing with `isinstance` before use
- Use `dataclasses.dataclass` for internal structures, Pydantic `BaseModel` wherever runtime validation of external/untrusted input is needed (API schemas, config files, etc.)
- Never use plain `dict` as a return type when a structured model can be defined

---

## Functions & Methods

- One responsibility per function; max **40 lines**, max **5 parameters**
- Prefer early returns over nested conditionals
- Always catch specific exceptions — never use bare `except:`
- When re-raising, preserve the cause with `raise ... from e`
- Raise domain-specific exceptions from the business logic layer; let the entry/presentation layer handle translation to the external-facing format (e.g., HTTP status, exit code)
- Never mix sync blocking calls into async functions; use `asyncio.gather` for concurrent operations

---

## Classes

- Prefer composition over inheritance
- Use `ABC` and `abstractmethod` to define interfaces
- No multiple inheritance except for mixins
- Keep `__init__` free of logic — use class methods or factory functions for complex construction

---

## Imports

- Order: standard library → third-party → internal (absolute only)
- Never use relative imports or wildcard imports

---

## Docstrings

- Required on all public classes, methods, and functions
- Use Google-style docstrings; skip `Args`/`Returns` for simple, self-evident functions
- Write in English