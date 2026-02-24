# Agent Instructions

Guidelines for AI agents working on this  codebase. For detailed rationale
behind these rules, see the [Architecture Decision Records](docs/adr/README.md).

When working on this codebase:

1. **Always use `uv`** instead of `pip` or `python -m venv`
2. **Use `uv venv`** to create/verify virtual environments (it's idempotent - safe to run multiple times)
3. **Use `uv sync`** to install dependencies from `pyproject.toml`
4. **Use `uv run`** to execute Python scripts (no activation needed)
5. **Use the Makefile** targets (`make install`, `make run`, etc.) when available


### Examples

```bash
# Setup new environment
uv venv && uv sync

# Run tests
uv run pytest

# Run the example
uv run example.py

# Or use make targets
make install
make run
make test
```

## Quick Reference

| Need | Answer |
|------|--------|
| Validate changes | `ci/validate` (mandatory, never skip) |
| Run tests | `ci/test` |


## Task Routing

| Task | Key Rules | ADRs |
|------|-----------|------|


## Architecture Overview




## Core Constraints




## Rules by Topic

### Performance

### Determinism

### Error Handling

### Code Style

### Testing

### Dependencies

## Documentation

## Validation Workflow

## Project Conventions

- Dependencies are managed in `pyproject.toml`
- Lock file is `uv.lock` (committed to repo)
- Virtual environment is `.venv/` (gitignored)
- Generated data files go in `data/` (gitignored)
- **Use Polars, not Pandas** - All data manipulation uses `polars` for performance and consistency
- Strongly prefer altair over matplotlib and pathlib over os.path
- **Tests use plain functions, not classes** - Use `def test_foo(tmp_path):` not `class TestFoo`

Be extremely concise. Sacrifice grammar for the sake of concision.