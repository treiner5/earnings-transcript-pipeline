# Earnings Transcript Pipeline

A Streamlit application for managing and analyzing earnings call transcripts using Snowflake and AI.

## Features
- 📊 Automated transcript loading from Financial Modeling Prep (FMP) API
- 🤖 AI-powered analysis using Snowflake Cortex
- 📈 Sentiment scoring and trend analysis
- 🔍 Multi-quarter transcript search and comparison
- 📋 Interactive dashboard for portfolio monitoring

## Setup

### Prerequisites
- Python 3.8+
- Snowflake account with Cortex enabled
- FMP API key

### Installation

1. Clone the repository:
```bash
git clone https://github.com/yourusername/earnings-transcript-pipeline.git
cd earnings-transcript-pipeline

2. Install dependencies:

```bashpip install -r requirements.txt

3. Set up environment variables
```cp .env.example .env

4. Run Snowflake setup:
```# Execute SQL files in order
snowsql -f sql/01_schema.sql
snowsql -f sql/02_tables.sql
snowsql -f sql/03_procedures.sql
snowsql -f sql/04_functions.sql

5. Run the app:
```streamlit run streamlit_app.py
