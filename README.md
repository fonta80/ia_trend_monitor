# IA Trend Monitor

Sistema automático para recopilar, procesar y consultar tendencias de Inteligencia Artificial generativa, agentes (LangGraph/LangChain), RAG, automatización y consultoría.

---

## ✨ Objetivo

1. Extraer información actualizada de fuentes seleccionadas (blogs, newsletters, GitHub, papers, redes sociales).
2. Procesar y resumir el contenido con LLMs, generando embeddings y metadatos.
3. Almacenar la información de forma estructurada y vectorial para búsqueda semántica.
4. Ofrecer una interfaz (API + UI) tipo RAG para consultas y dashboards.

---

## 🗂️ Estructura inicial del proyecto

```
ia-trend-monitor/
├── airflow/
│   └── dags/
│       └── extract_pipeline.py        # DAG principal de extracción
├── src/
│   ├── extraction/
│   │   ├── rss_extractor.py           # Blogs & documentación (RSS / scraping)
│   │   ├── newsletter_parser.py       # Parsing de newsletters vía Gmail API
│   │   ├── github_extractor.py        # Repos trending y releases
│   │   ├── arxiv_extractor.py         # Papers científicos y PapersWithCode
│   │   └── twitter_extractor.py       # Hashtags y cuentas clave (tweepy)
│   ├── processing/
│   │   ├── summarizer.py              # Resumir texto con LLM (OpenAI/Gemini)
│   │   ├── classifier.py              # Clasificación temática (LangChain)
│   │   └── embeddings.py              # Generación de embeddings (OpenAI/Cohere)
│   ├── storage/
│   │   ├── vector_db.py               # ChromaDB wrapper
│   │   └── models.py                  # Esquema de documentos
│   ├── config.py                      # Variables de entorno y constantes
│   └── utils.py                       # Herramientas comunes
├── app/
│   ├── api.py                         # FastAPI endpoints (RAG)
│   └── ui.py                          # Streamlit interface
├── tests/
│   └── test_extraction.py
├── pyproject.toml                     # Configuración de Poetry
└── README.md                          # (este archivo)
```

---

## 🚀 Set‑up rápido (Poetry)

```bash
# 1. Instalar Poetry (si no está instalado)
curl -sSL https://install.python-poetry.org | python3 -

# 2. Crear entorno virtual e instalar dependencias
poetry install

# 3. Añadir dependencias adicionales
poetry add fastapi streamlit langchain langgraph openai cohere chromadb beautifulsoup4 tweepy airflow

# 4. Variables de entorno (ejemplo .env)
OPENAI_API_KEY="sk‑..."
COHERE_API_KEY="..."
TWITTER_BEARER_TOKEN="..."
GMAIL_CLIENT_SECRET_JSON="path/to/secret.json"
CHROMA_HOST="localhost"
CHROMA_PORT="8000"

# Ejecutar comandos dentro del entorno
poetry run uvicorn app.api:app --reload
poetry run streamlit run app/ui.py
```

---

## 📌 Roadmap de desarrollo

| Fase | Objetivo                                             | Estado |
| ---- | ---------------------------------------------------- | ------ |
| 1    | Implementar extractores RSS/blog (LangChain, OpenAI) | ⬜      |
| 2    | Añadir newsletter\_parser (Gmail API)                | ⬜      |
| 3    | Embeddings y ChromaDB storage                        | ⬜      |
| 4    | API RAG (FastAPI) MVP                                | ⬜      |
| 5    | UI Streamlit y despliegue Docker                     | ⬜      |
| 6    | Automatización Airflow + tests                       | ⬜      |

---

## 🛠️ Command Cheatsheet

```bash
# Ejecutar extractor RSS manualmente (debug)
poetry run python -m src.extraction.rss_extractor --source "https://openai.com/blog/rss"

# Lanzar DAG Airflow local
poetry run airflow standalone  # UI: http://localhost:8080

# Arrancar API FastAPI
poetry run uvicorn app.api:app --reload

# Ejecutar interfaz Streamlit
poetry run streamlit run app/ui.py
```

---

## 🤝 Contribución

1. Abre una issue con propuesta o bug.
2. Crea una branch y un Pull Request descriptivo.
3. Ejecuta los tests (`pytest`) antes de enviar.

---

## 🔒 Licencia

MIT License
