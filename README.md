# Text-to-SQL Benchmark Indonesia

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![DOI](https://img.shields.io/badge/DOI-10.30591%2Fjpit.v10i4.9047-green.svg)](https://jestec.taylors.edu.my/Special%20Issue%20INCITEST%202025/INCITEST2025_02.pdf)

A lightweight, fully reproducible benchmark to evaluate large language models (LLMs) on **natural-language-to-SQL** generation for Indonesian-language queries. Covers two open databases (Sakila and Resep), six query categories, and 30 scenarios with 240 model evaluation outputs.

## Why This Benchmark?

Indonesian-language Text-to-SQL evaluation resources are scarce. Most benchmarks focus on English, leaving a gap for researchers and practitioners working with Bahasa Indonesia. This repository fills that gap by providing:

- **Bilingual scenarios** — every question has Indonesian (`question_id`) and English (`question_en`) versions
- **Domain diversity** — Sakila (film rental, English schema) and Resep (Indonesian recipes, Indonesian schema)
- **Transparent evaluation** — gold-standard SQL, expected output rows, and semantic column mappings included
- **Multi-model comparison** — results across 4 LLM variants for direct reproducibility

## Models Evaluated

| Model | Provider | Type |
|-------|----------|------|
| `gemini-2.5-flash` | Google | Proprietary |
| `gemini-flash-lite` | Google | Proprietary |
| `gemma-3n-e2b` | Google | Open-weight |
| `gemma-online` | Google | Open-weight |

## Query Categories (6 × 5 scenarios × 2 databases = 30 scenarios)

| Code | Category | Example Skill |
|------|----------|---------------|
| A3 | Aggregation | COUNT, AVG, GROUP BY |
| C5 | Comparison | Filtering, WHERE conditions |
| J2 | Join | Multi-table JOINs |
| L1 | Lookup | Simple SELECT with filters |
| N4 | Nested | Subqueries, IN/EXISTS |
| S6 | Sorting | ORDER BY, LIMIT, ranking |

## Project Structure

```
├── db/                        # Database schemas & seed data
│   ├── sakila-schema.sql      #   Sakila schema (film rental)
│   ├── sakila-data.sql        #   Sakila seed data
│   └── resep.v1.2025-07.sql   #   Resep database (Indonesian recipes)
├── gold-standard/             # 12 gold-standard files (per category × DB)
│   ├── RES-A3.json            #   Resep: Aggregation scenarios
│   ├── SAK-A3.json            #   Sakila: Aggregation scenarios
│   └── ...
├── gold-standard.json         # Combined gold-standard (all 30 scenarios)
├── luaran-model/              # 240 model output files
│   ├── RES-A3-01_gemini-2.5-flash.json
│   ├── RES-A3-01_gemma-3n-e2b.json
│   └── ...
├── prompt_templates_v2.yaml   # Prompt config v2 (interpretive extraction)
├── prompt_templates_v3.yaml   # Prompt config v3 (literal extraction)
├── semantic_map.yaml          # Column-name alias mapping per model/scenario
├── CONTRIBUTING.md            # Contribution guidelines
├── CITATION.cff               # Machine-readable citation metadata
└── LICENSE                    # MIT License
```

## Quick Start

### 1. Clone & Set Up Database

```bash
git clone https://github.com/Galih-Hermawan-Unikom/text2sql-benchmark-id.git
cd text2sql-benchmark-id

# Set up Sakila (requires MySQL/MariaDB)
mysql -u root -p < db/sakila-schema.sql
mysql -u root -p sakila < db/sakila-data.sql

# Set up Resep
mysql -u root -p < db/resep.v1.2025-07.sql
```

### 2. Run a Scenario

Each scenario in `gold-standard.json` contains:
- `question_id` — the Indonesian natural-language question
- `solution_sql` — the ground-truth SQL
- `expected_rows` — the expected query result
- `category` — the query complexity category

To evaluate a model, send `question_id` with the database schema (from `prompt_templates_v2.yaml`) to your LLM, then compare the generated SQL against `solution_sql`.

### 3. Compare with Existing Results

Model outputs are in `luaran-model/`. Each file contains the LLM's raw response for a specific scenario. Use `semantic_map.yaml` to normalize column-name differences across models before comparing.

## Adding Your Own Model

1. Run each scenario from `gold-standard.json` against your model
2. Save outputs to `luaran-model/` as `{SCENARIO_ID}_{your-model-name}.json`
3. If your model uses different column names, add mappings to `semantic_map.yaml`
4. Submit a Pull Request with your results

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines.

## Citation

If you use this benchmark in your research, please cite:

```bibtex
@article{Hermawan2026Evaluating,
  author    = {Hermawan, Galih and Rainarli, Ednawati and Ravshanovna, Radjabova Inobat},
  title     = {{Evaluating Gemini and Gemma Language Models for Indonesian Text-to-SQL Tasks}},
  journal   = {Journal of Engineering Science and Technology (JESTEC), Special Issue on INCITEST 2025},
  volume    = {21},
  number    = {2},
  pages     = {9--16},
  year      = {2026},
  url       = {https://jestec.taylors.edu.my/Special%20Issue%20INCITEST%202025/INCITEST2025_02.pdf}
}
```

A `CITATION.cff` file is also included for automatic citation tools (Zotero, GitHub citation button, etc.).

## Contact & Maintainer

**Galih Hermawan** — Lecturer & Researcher, Informatics Engineering, Universitas Komputer Indonesia (UNIKOM)

- Email: [galih.hermawan@email.unikom.ac.id](mailto:galih.hermawan@email.unikom.ac.id)
- ORCID: [0000-0002-8476-5996](https://orcid.org/0000-0002-8476-5996)
- GitHub: [@Galih-Hermawan-Unikom](https://github.com/Galih-Hermawan-Unikom)

### Contributors

- **Ednawati Rainarli** — Lecturer & Researcher, Informatics Engineering, UNIKOM

## Contributing

We welcome contributions! See [CONTRIBUTING.md](CONTRIBUTING.md) for how to submit scenarios, share model results, or improve documentation.

Open an issue or discussion for research collaboration, dataset exchange, or methodology talks.
