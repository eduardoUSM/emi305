# Produccion de Software EMI305

Repositorio desplegable del curso **Produccion de Software EMI305**.

El material integrado actualmente contiene un modulo practico de seguridad de software con:

- apuntes y notebooks Quarto en `nbs/`
- scripts reutilizables para generar SBOMs, ejecutar CodeQL y analizar vulnerabilidades con Grype en `scripts/`
- repositorios de ejemplo configurados en `data/repos.json`
- resultados de referencia en `data/results/`
- lecturas de apoyo en `data/papers/` y `data/book/`
- un Dev Container con Python, uv, Jupyter, Syft, Grype, CodeQL y Node.js

## Inicio rapido

Con Docker y VS Code instalados, abre este repositorio en un Dev Container. El contenedor ejecuta `uv sync`, registra el kernel de Jupyter y prepara las herramientas de seguridad.

Para preparar los repositorios de ejemplo:

```bash
uv run python scripts/add_submodules.py
```

Para ejecutar los analisis:

```bash
uv run python scripts/generate_sboms.py
uv run python scripts/generate_codeql.py
uv run python scripts/generate_grype.py
```

Los resultados se guardan en `data/results/`.

## Sitio del curso

El sitio Quarto se construye desde `nbs/`:

```bash
cd nbs
uv run quarto render
```

La configuracion de publicacion apunta a:

<https://dci-courses.github.io/produccion_software_emi305/>

## Estructura

```text
.
├── .devcontainer/       # Entorno reproducible del curso
├── .github/workflows/   # CI y despliegue
├── data/
│   ├── book/            # Material base del curso
│   ├── papers/          # Lecturas de apoyo
│   ├── repos/           # Repositorios de ejemplo clonados localmente
│   ├── results/         # Resultados de referencia y salidas regenerables
│   └── repos.json       # Configuracion de repositorios de ejemplo
├── nbs/                 # Sitio Quarto, notebooks y lecturas
├── scripts/             # Automatizacion de seguridad
├── pyproject.toml       # Dependencias Python
└── uv.lock              # Lockfile de dependencias
```

## Validacion local

```bash
python3 -m compileall scripts
python3 scripts/add_submodules.py --dry-run
python3 scripts/generate_sboms.py --dry-run
python3 scripts/generate_codeql.py --dry-run
python3 scripts/generate_grype.py --dry-run
```
