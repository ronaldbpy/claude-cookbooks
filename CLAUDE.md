# Claude Cookbooks

## Qué es
Colección de Jupyter notebooks y ejemplos Python para construir con la Claude API. Recurso de referencia para developers — snippets listos para copiar e integrar.

## Cómo se levanta
```bash
uv sync --all-extras          # instalar deps
uv run pre-commit install     # instalar hooks
cp .env.example .env          # agregar ANTHROPIC_API_KEY
uv run jupyter lab            # abrir notebooks
```

## Stack
- Python 3.12 + uv
- Jupyter notebooks
- Claude API (anthropic SDK)
- Ruff (formatter + linter)
- pytest

## Estructura
```
capabilities/      — RAG, clasificación, summarización
evals/             — patrones de evaluación y benchmarks
tool_use/          — tool use e integraciones
multimodal/        — visión, imágenes
extended_thinking/ — razonamiento extendido
cost_optimization/ — optimización de costos
third_party/       — Pinecone, VoyageAI, Wikipedia
scripts/           — validación
.claude/           — commands y skills de Claude Code
```

## Reglas de este proyecto
- Modelos: alias sin fecha siempre (`claude-sonnet-5`, `claude-haiku-4-5`, `claude-opus-4-8`). Nunca IDs con fecha como `claude-sonnet-4-6-20250514`.
- Bedrock: prefijo `anthropic.` o `global.anthropic.` — formato diferente al API directo.
- Deps: solo con `uv add <package>`. Nunca editar `pyproject.toml` directo.
- API keys: nunca commitear `.env`. Usar `dotenv.load_dotenv()` + `os.environ`.
- Notebooks: mantener outputs (son demos). Un concepto por notebook. Deben correr top-to-bottom sin errores.
- Correr `make check` antes de commitear.
- Branches: `<username>/<feature-description>`. Commits: Conventional Commits.
- Notebook nuevo: agregar entrada en `registry.yaml` + autor en `authors.yaml`.

## Slash Commands
- `/notebook-review` — revisar calidad de notebook
- `/model-check` — validar referencias de modelos Claude
- `/link-review` — verificar links en archivos modificados

## Cosas que ya intentamos y no funcionaron
- IDs de modelo con fecha en código — se desactualizan; el alias sin fecha es siempre el correcto.
- Editar `pyproject.toml` directo — rompe el lock file de uv.
