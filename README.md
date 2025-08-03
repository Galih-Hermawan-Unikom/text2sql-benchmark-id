# 🚀 Text-to-SQL Research: Comparative Evaluation of Gemini & Gemma Models

## 📊 Research Overview

This repository contains a **production-ready comparative evaluation system** for text-to-SQL generation using **Gemini API models** (Gemini 2.5 Flash, Gemini 2.5 Flash-Lite, Gemma-3-27B-IT) and **local Gemma models** (Gemma-3n-E2B). The research focuses on Indonesian language query understanding and MySQL query generation accuracy with **scientific-grade evaluation consistency**.

## 🛠️ Project Setup

### Prerequisites
- Python 3.8+
- Google Cloud account with Gemini API access
- MySQL Server (for database execution)
- Ollama (for local model execution)
- Required Python packages (install via `pip install -r requirements.txt`)

### Supported LLM Models

#### API-based Models (using `prompt_templates_v3.yaml`)
1. **Gemini 2.5 Flash** - Google's high-performance model, prioritizing accuracy and context understanding
2. **Gemini 2.5 Flash-Lite** - Lighter and faster version with comparable accuracy to Flash
3. **Gemma-3-27B-IT** - The 27B parameter version of Gemma running on Gemini API

#### Local Models (using `prompt_templates_v2.yaml`)
1. **Gemma-3n-E2B** - 7B parameter efficient model optimized via Ollama

### Installation
1. Clone the repository
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Set up your `.env` file with the following variables:
   ```
   GOOGLE_API_KEY=your_google_api_key
   MYSQL_USER=your_mysql_user
   MYSQL_PASSWORD=your_mysql_password
   MYSQL_HOST=localhost
   MYSQL_PORT=3306
   ```

## 🎯 Research Achievements

✅ **Complete 60-Scenario Benchmark**: 6 SQL categories × 2 databases × 5 scenarios each  
✅ **100% Evaluation Consistency**: Identical comprehensive evaluation structure for all models  
✅ **Gold Standard Integrity**: Verified and validated benchmark data  
✅ **Production Pipeline**: Full generation → execution → evaluation workflow  
✅ **Scientific Reporting**: Academic-ready performance metrics and analysis  


### 📊 Category-wise Performance Analysis
| Category | Description |
|----------|-------------|
| **L1** - Lookup/Filter | Simple data retrieval
| **A3** - Aggregation | COUNT, SUM, AVG operations 
| **C5** - Comparative | Comparison queries
| **S6** - Superlative | MAX, MIN, TOP-N queries
| **J2** - Join + Filter | Multi-table with conditions
| **N4** - Nested/Subquery | Complex subqueries

## 📚 Research Dataset

### 🎯 Gold Standard Benchmark (60 scenarios)
| Database | Scenarios | Focus Area | Language | Schema Description |
|----------|-----------|------------|----------|-------------------|
| **RESEP** | 30 scenarios | Indonesian cuisine domain | Indonesian → MySQL | Recipes, ingredients, and cooking methods for Indonesian dishes |
| **SAKILA** | 30 scenarios | Business/rental domain | Indonesian → MySQL | Movie rental business with customers, films, and transactions |

### 📂 Project Structure
```
# Main Scripts
├── text2sql_gemini_v2.py     # Text-to-SQL using Gemini API models
├── text2sql_ollama.py        # Text-to-SQL using local Ollama models
├── execute_llm_sqls.py       # Execute SQL from LLM outputs
├── execute_gemma_sqls.py     # Special executor for Gemma models
├── evaluate_results_v2.py    # Evaluation script for model outputs
├── generate_summary_report.py # Generate summary reports
├── analyze_evaluations.py    # Detailed analysis of evaluation results
└── update_semantic_map.py    # Update semantic mapping

# Configuration & Data
├── prompt_templates_v2.yaml  # Template config for local Ollama model
├── prompt_templates_v3.yaml  # Template config for API-based models
├── semantic_map.yaml         # Schema mapping and relationships
├── luaran-model/            # Output directory for results
├── gold-standard/           # Gold standard queries
├── .env.example             # Environment configuration
└── requirements.txt         # Python dependencies

# Analysis
└── analisis_evaluasi_v2.ipynb  # Jupyter notebook for analysis
```

### 📋 SQL Complexity Categories
| Category | Code | Description | Scenarios |
|----------|------|-------------|-----------|------------|
| **Lookup/Filter** | L1 | Simple SELECT with WHERE | 10 |
| **Aggregation** | A3 | COUNT, SUM, AVG, GROUP BY | 10 |
| **Join + Filter** | J2 | Multi-table with conditions | 10 |
| **Comparative** | C5 | Comparison operations | 10 |
| **Nested/Subquery** | N4 | Complex subqueries | 10 |
| **Superlative** | S6 | MAX, MIN, TOP-N queries | 10 |

### 🗄️ Database Schema Overview

#### RESEP Database (Indonesian Recipe Domain)
```sql
-- Main entities for Indonesian cuisine
masakan (kode_masakan, nama_masakan, kategori, asal_daerah, level_pedas)
resep (id_resep, kode_masakan, waktu_masak, tingkat_kesulitan, teknik_masak)
bahan (id_bahan, nama_bahan, kategori_bahan, satuan_default)
resep_bahan (id_resep, id_bahan, jumlah, satuan_override)  -- Junction table
```

#### SAKILA Database (Business Domain)
```sql
-- Core business entities
film, actor, customer, category, language, store, staff
film_actor, film_category  -- Many-to-many relationships
rental, payment, inventory  -- Business transactions
address, city, country  -- Location hierarchy
```

## 🔄 Production-Ready Evaluation Pipeline

### 🚀 Complete Workflow

#### 1️⃣ SQL Generation
```bash
# For API-based models (Gemini)
python text2sql_gemini_v2.py --model-id gemini-2.5-flash --id SCENARIO_ID
# Alternative: process a category of scenarios
python text2sql_gemini_v2.py --model-id gemini-2.5-flash --category A3
# Alternative: process all scenarios
python text2sql_gemini_v2.py --model-id gemini-2.5-flash --all

# For local models (Ollama)
python text2sql_ollama.py --id SCENARIO_ID
# Alternative: process a category of scenarios
python text2sql_ollama.py --category A3
# Alternative: process all scenarios
python text2sql_ollama.py --all
```

#### 2️⃣ SQL Execution  
```bash
# For all LLM outputs (processes all JSON files in luaran-model directory)
python execute_llm_sqls.py

# For Gemma model outputs specifically (processes only Gemma files)
python execute_gemma_sqls.py
```

#### 3️⃣ Evaluation & Analysis
```bash
# Run evaluation (processes all execution results automatically)
python evaluate_results_v2.py

# Generate summary report (creates CSV from all evaluations)
python generate_summary_report.py

# Detailed analysis with optional filtering
python analyze_evaluations.py
# Filter by specific model
python analyze_evaluations.py --model gemini-2.5-flash
# Filter by error type
python analyze_evaluations.py --error-type execution_failed
```

#### 4️⃣ Semantic Map Update
```bash
# Update semantic mapping based on evaluation reports (processes all reports by default)
python update_semantic_map.py

# Process evaluation reports with filtering options
python update_semantic_map.py --model gemini-flash-lite
python update_semantic_map.py --reports-dir evaluation-reports
python update_semantic_map.py --semantic-map semantic_map.yaml

# Process a single evaluation report file
python update_semantic_map.py --test-file evaluation-reports/RES-A3-01_gemini-flash_detailed_evaluation.json

# Dry run to see changes without updating
python update_semantic_map.py --dry-run
```

### 📊 Scientific Evaluation Metrics

#### 🎯 Comprehensive Evaluation Framework
Our evaluation system produces detailed metrics across multiple dimensions:

- **SQL Similarity Score**: Semantic and syntactic similarity to gold standard queries
- **Execution Success Rate**: Percentage of queries that execute without database errors  
- **Result Accuracy**: Row-by-row comparison with expected query results
- **Efficiency Metrics**: Response latency, token usage, and cost analysis
- **Statistical Validation**: Wilcoxon signed-rank and McNemar tests with FDR correction

#### 📈 Multi-Level Analysis Structure
Each scenario generates comprehensive evaluation data:

1. **Comprehensive Multi-Dimensional Evaluation**: Complete performance metrics per scenario
2. **Summary Report**: Aggregated results in `evaluation-reports/summary_report.csv`
3. **Statistical Analysis**: Advanced analytics in `analisis_evaluasi_v2.ipynb` and `analisis_evaluasi_v2.pdf`
4. **Error Categorization**: Systematic classification of failure modes
5. **Cross-Model Comparison**: Statistical significance testing across all models

## 📊 Results and Analysis

### Performance Comparison
Based on comprehensive evaluation of 60 scenarios across 4 models, with results documented in `evaluation-reports/summary_report.csv` and statistical analysis in `analisis_evaluasi_v2.pdf`:

| Model | SQL Similarity | Execution Success | Mean Latency (ms) | Token Usage | Cost per Query ($) |
|-------|---------------|-------------------|-------------------|-------------|---------------------|
| Gemini 2.5 Flash | 0.875 | 82% | 4,707 | 3,452 | 0.00121 |
| Gemini 2.5 Flash-Lite | 0.871 | 80% | 1,249 | 2,901 | 0.00020 |
| Gemma-3-27B-IT | 0.852 | 77% | 5,684 | 2,637 | 0.00000* |
| Gemma-3n-E2B | 0.783 | 52% | 159,818 | 1,556 | 0.00008** |

\* *Open-source model with no API costs*  
\** *Local deployment costs (electricity/hardware)*

#### Statistical Significance Testing
**Methodology**: Wilcoxon signed-rank tests with Benjamini-Hochberg FDR correction (α = 0.05)

- **SQL Similarity**: Gemini 2.5 Flash, Gemini 2.5 Flash-Lite, and Gemma-3-27B-IT show no statistically significant differences (p > 0.05)
- **Execution Success**: Gemma-3n-E2B significantly underperforms all other models (25-30pp difference, p < 0.002)  
- **Efficiency Trade-offs**: Gemini 2.5 Flash-Lite provides optimal balance of accuracy and speed (~4x faster than Flash with equivalent quality)
- **Efficiency**: Models show clear trade-offs between accuracy, latency, and cost

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Google for the Gemini API
- The Ollama team for their open-source models
- The open-source community for various utilities and libraries

### 🔬 Research Methodology
- **Consistent Evaluation**: 100% identical structure between Ollama and Gemini
- **Numeric Normalization**: Fixed type mismatches (e.g., 46.0 → "46")
- **Bilingual Support**: Indonesian questions → English SQL comments
- **Error Classification**: Systematic failure analysis for improvement
- **Reproducible Results**: Deterministic evaluation with temperature=0.0

## 📊 Scientific Evaluation Results Format

### 🎯 Comprehensive Multi-Dimensional Analysis Structure
Each scenario evaluation generates a detailed JSON file containing complete performance metrics:

```json
{
  "model": "gemini",
  "model_version": "gemini-2-5-flash",
  "evaluation_timestamp": "2025-01-23T14:29:50.123456",
  
  "input_data": {
    "question_indonesian": "Tampilkan 5 film dengan genre Action terpopuler",
    "question_english": "Show 5 most popular Action genre films",
    "database": "sakila",
    "category": "A3_Aggregation", 
    "scenario_id": "RES-A3-01"
  },
  
  "gold_standard": {
    "expected_sql": "SELECT f.title FROM film f JOIN film_category fc...",
    "expected_rows": [...],
    "expected_row_count": 5
  },
  
  "model_performance": {
    "generated_sql": "SELECT title FROM film WHERE...",
    "sql_explanation": "Query selects top-rated Action films",
    "generation_time_ms": 4707,
    "execution_success": true,
    "execution_time_ms": 45,
    "actual_row_count": 5,
    "result_accuracy": "exact_match"
  },
  
  "similarity_analysis": {
    "token_similarity": 0.85,
    "structural_similarity": 0.90,
    "semantic_similarity": 0.95,
    "overall_similarity": 0.875
  },
  
  "final_evaluation": {
    "performance_rating": "excellent",
    "success": true,
    "score": 95.0,
    "category_performance": "excellent",
    "model_confidence": 0.98
  },
  
  "resource_utilization": {
    "input_tokens": 1892,
    "output_tokens": 1560,
    "total_tokens": 3452,
    "estimated_cost": 0.00121
  },
  
  "error_analysis": {
    "syntax_errors": [],
    "execution_errors": [],
    "logical_errors": [],
    "improvement_suggestions": []
  }
}
```

### 📈 Batch Performance Summary
Cross-model evaluation summaries available in `evaluation-reports/summary_report.csv`:

```csv
Model,Category,Database,Success_Rate,Avg_Similarity,Avg_Latency_ms,Avg_Tokens,Scenarios_Count
gemini-2-5-flash,Overall,All,82.0,0.875,4707,3452,60
gemini-flash-lite,Overall,All,80.0,0.871,1249,2901,60
gemma-27b,Overall,All,77.0,0.852,5684,2637,60
gemma-3n-e2b,Overall,All,52.0,0.783,159818,1556,60
```

#### Performance Categories by Complexity
```json
{
  "category_breakdown": {
    "L1_Lookup": {"avg_success": 95.0, "difficulty": "basic"},
    "A3_Aggregation": {"avg_success": 85.0, "difficulty": "intermediate"},
    "J2_Join": {"avg_success": 75.0, "difficulty": "intermediate"},
    "C5_Comparative": {"avg_success": 80.0, "difficulty": "advanced"},
    "N4_Nested": {"avg_success": 55.0, "difficulty": "complex"},
    "S6_Superlative": {"avg_success": 70.0, "difficulty": "advanced"}
  },
  
  "database_analysis": {
    "resep": {"avg_success": 78.3, "domain": "recipe_management"},
    "sakila": {"avg_success": 72.5, "domain": "video_rental"}
  }
}

## 🛠️ Technical Setup & Usage

### 📋 Prerequisites
```bash
# 1. Install Python dependencies
pip install mysql-connector-python requests pyyaml pandas numpy matplotlib seaborn scipy statsmodels

# 2. Setup MySQL databases
mysql -u root -p < db/sakila-schema.sql
mysql -u root -p < db/sakila-data.sql
mysql -u root -p < db/resep.v1.2025-07.sql

# 3. Configure environment variables
cp .env.example .env
# Edit .env with your MySQL credentials and API keys
```

### ⚙️ Model Configuration

#### Ollama Setup (Local Models)
```yaml
# Configuration for Gemma-3n-E2B (7B parameter model)
model: "gemma-3n-e2b"
temperature: 0.0
max_tokens: 500
base_url: "http://localhost:11434"
prompt_template: "prompt_templates_v2.yaml"
```

#### Gemini API Setup (Cloud Models)
```yaml
# Configuration for Gemini 2.5 Flash series and Gemma-3-27B-IT
models:
  - "gemini-2.5-flash"      # High-performance flagship model
  - "gemini-2.5-flash-lite" # Optimized speed-accuracy balance  
  - "gemma-3-27b-it"        # 27B parameter open-source model via API

# Shared configuration
temperature: 0.0
max_tokens: 1000
api_key: "YOUR_GEMINI_API_KEY"
prompt_template: "prompt_templates_v3.yaml"
```

#### Model Selection Guidelines
| Use Case | Recommended Model | Rationale |
|----------|------------------|-----------|
| **Interactive Applications** | Gemini 2.5 Flash-Lite | 4x faster with equivalent accuracy |
| **Batch Processing** | Gemini 2.5 Flash | Maximum accuracy for offline analysis |
| **On-Premise/Privacy** | Gemma-3-27B-IT | API-based but open-source, good performance |
| **Resource-Constrained** | Gemma-3n-E2B | Local deployment, minimal hardware requirements |

## 🔬 Research Contributions & Findings

### 🎯 Key Scientific Achievements

#### 1. **First Comprehensive Indonesian Text-to-SQL Evaluation Framework**
- **Novel Benchmark**: 60-scenario evaluation suite specifically designed for Indonesian language nuances
- **Cross-Database Validation**: Testing on both RESEP (recipe management) and SAKILA (video rental) domains
- **Cultural Context Handling**: Addresses Indonesian linguistic structures and cultural references in SQL generation

#### 2. **Rigorous Statistical Analysis Methodology**
- **Statistical Testing**: Wilcoxon signed-rank tests with Benjamini-Hochberg FDR correction (α = 0.05)
- **Comprehensive Multi-Dimensional Evaluation Structure**: Complete metrics ensuring reproducible scientific results
- **Cross-Model Consistency**: 100% identical evaluation structure eliminating comparative bias

#### 3. **Multi-Dimensional SQL Complexity Analysis**
- **6-Category Difficulty Progression**: L1 (Lookup) → N4 (Nested) complexity assessment
- **Performance Intelligence**: Systematic identification of model strengths and failure patterns
- **Error Taxonomy**: Granular classification enabling targeted model improvements

### 📊 Performance Intelligence & Model Rankings

#### 🥇 **Tier 1: Premium Performance Models**
**Gemini 2.5 Flash & Gemini 2.5 Flash-Lite**
- **Statistical Equivalence**: No significant differences in SQL similarity and execution success (p > 0.05)
- **Speed-Accuracy Trade-off**: Flash-Lite delivers 4x faster response with equivalent quality
- **Use Case**: Flash-Lite optimal for interactive applications; Flash for batch processing requiring maximum accuracy

#### 🥈 **Tier 2: Viable Open-Source Alternative**
**Gemma-3-27B-IT**
- **Performance Position**: Competitive performance with no significant difference from Gemini models in similarity scores
- **Deployment Advantages**: Zero API costs, complete data privacy, customizable deployment
- **Requirements**: Substantial GPU resources (24GB+ VRAM recommended)

#### 🥉 **Tier 3: Efficiency-Focused Model**
**Gemma-3n-E2B**
- **Resource Optimization**: Lowest token usage, fully local deployment, minimal hardware requirements
- **Performance Trade-off**: Significantly lower performance compared to other models (p < 0.002)
- **Use Case**: Resource-constrained environments where accuracy can be traded for efficiency

### 🔍 **Category-Specific Performance Insights**

#### 📈 **Universal Strength Areas**
- **L1 Lookup Queries**: High success rates across all models for simple data retrieval
- **A3 Aggregation**: Strong performance with GROUP BY operations and statistical functions
- **S6 Superlative**: Consistent handling of ORDER BY/LIMIT combinations

#### ⚠️ **Challenge Areas**
- **N4 Nested Queries**: Universal complexity challenge across all models
- **C5 Comparative**: Advanced logical reasoning requirements
- **J2 Join Operations**: Variable performance depending on relationship complexity

#### 🗃️ **Database Domain Analysis**
- **RESEP Database**: Higher success rates due to familiar domain vocabulary
- **SAKILA Database**: Lower success rates due to complex business relationships

### 🏆 **Research Impact & Practical Recommendations**

#### 💼 **Production Deployment Guidance**
1. **Interactive Applications**: Gemini 2.5 Flash-Lite (optimal speed-accuracy balance)
2. **High-Accuracy Batch Processing**: Gemini 2.5 Flash (maximum quality)
3. **On-Premise/Privacy-Critical**: Gemma-3-27B-IT (best open-source option)
4. **Resource-Constrained Environments**: Gemma-3n-E2B (minimal requirements)

#### 📊 **Cost-Performance Analysis**
- **Gemini 2.5 Flash**: Premium accuracy with higher operational costs
- **Gemini 2.5 Flash-Lite**: Optimal cost-performance balance with significantly lower API costs
- **Gemma Models**: Minimal to zero operational costs for appropriate use cases

#### 🎯 **Scientific Contributions to Field**
- **First bilingual (Indonesian-English) Text-to-SQL benchmark**: Enabling future research in multilingual SQL generation
- **Comprehensive model comparison framework**: Reproducible methodology for academic research
- **Open-source evaluation tools**: Complete pipeline available for research community replication


### 🔬 Technical Innovations

#### 1. **Enhanced Semantic Mapping**
- Column similarity detection for flexible result comparison
- Handles different SQL approaches to same logical outcome
- Numeric type normalization (e.g., 46.0 → "46")

#### 2. **Comprehensive Error Analysis**
- Generation errors vs execution errors separation
- Schema confusion detection and classification
- Improvement pathway identification

#### 3. **Production-Ready Architecture**
- Clean 19-file core system (71% workspace reduction)
- Archived 68 experimental files safely preserved
- Zero performance regression during optimization

## � Future Research Directions

### 🎯 Immediate Opportunities
1. **N4 Category Enhancement**: Targeted prompt engineering for nested queries
2. **Cross-Model Expansion**: Additional LLM architectures (Claude, LLaMA, etc.)
3. **Real-Time Evaluation**: Live performance monitoring system

### 🔬 Advanced Research Areas
1. **Multilingual Extension**: English, Indonesian, regional languages
2. **Schema Complexity Scaling**: Enterprise database complexity testing
3. **Query Optimization Analysis**: Performance vs correctness trade-offs
4. **Human Evaluation Integration**: User study for practical applicability

### 🚀 Industry Applications
1. **Business Intelligence Integration**: Real-world BI tool incorporation
2. **Educational Platform**: Indonesian SQL learning system
3. **Cultural Data Analysis**: Southeast Asian database query systems

## 📚 Academic Impact

### 🎓 Publications Ready
- **Methodology Paper**: Bilingual text-to-SQL evaluation framework
- **Performance Analysis**: LLM comparison in Indonesian context
- **Technical Report**: Comprehensive multi-dimensional evaluation structure specification

### 🏆 Research Significance
- **First Indonesian Text-to-SQL Benchmark**: Academic priority
- **Evaluation Consistency Innovation**: Eliminates comparison bias
- **Cultural AI Application**: Southeast Asian language technology

---

## 📇 Contact & Contribution

### 👤 Author & Maintainer

* \*\*Galih Hermawan\*\*— Lecturer & Researcher, Informatics Department, Universitas Komputer Indonesia (UNIKOM)
  E-mail: [galih.hermawan@email.unikom.ac.id](mailto:galih.hermawan@email.unikom.ac.id)
  ORCID: [https://orcid.org/0000-0002-8476-5996](https://orcid.org/0000-0002-8476-5996)
  GitHub: [@](https://github.com/Galih-Hermawan-Unikom)Galih-Hermawan-Unikom

### 🤝 Contributing

* **Submit issues** for evaluation bugs or improvements
* **Open pull requests** to add new benchmark scenarios or model evaluation scripts
* **Share results** from evaluating other models (attach JSON/CSV in your PR or discussion)

### 📧 Research Collaboration

For academic collaboration, dataset sharing, or methodology discussion, please open an issue or start a discussion thread in this repository. We welcome joint experiments and comparative studies.


