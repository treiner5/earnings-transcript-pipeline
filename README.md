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
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Set up environment variables:
```bash
cp .env.example .env
# Edit .env with your credentials
```

4. Configure Streamlit secrets:
```bash
mkdir -p .streamlit
cat > .streamlit/secrets.toml << EOF
[snowflake]
user = "your_username"
password = "your_password"
account = "your_account"
warehouse = "your_warehouse"
database = "EARNINGS_CALLS"
schema = "RAW_DATA"
role = "your_role"

[fmp]
api_key = "your_fmp_api_key"
EOF
```

5. Run Snowflake setup:
```sql
-- Execute in Snowflake
CREATE DATABASE IF NOT EXISTS EARNINGS_CALLS;
USE DATABASE EARNINGS_CALLS;

CREATE SCHEMA IF NOT EXISTS RAW_DATA;
CREATE SCHEMA IF NOT EXISTS ANALYTICS;

-- Run SQL scripts in order:
-- sql/01_schema.sql
-- sql/02_tables.sql
-- sql/03_procedures.sql
-- sql/04_functions.sql
```

6. Run the app:
```bash
streamlit run streamlit_app.py
```

## Architecture

```
┌─────────────────┐     ┌──────────────┐     ┌──────────────┐
│   FMP API       │────▶│   Snowflake  │────▶│   Streamlit  │
│  (Transcripts)  │     │   Database   │     │   Dashboard  │
└─────────────────┘     └──────────────┘     └──────────────┘
                              │
                              ▼
                        ┌──────────────┐
                        │ Cortex LLM   │
                        │  Analysis    │
                        └──────────────┘
```

### Database Structure
- **Database**: EARNINGS_CALLS
- **Schemas**: 
  - RAW_DATA (transcripts, watchlist, chat_history)
  - ANALYTICS (detailed_analysis)

## Project Structure

```
earnings-transcript-pipeline/
├── streamlit_app.py            # Main application
├── requirements.txt            # Python dependencies
├── .gitignore                 # Git ignore file
├── .env.example               # Environment template
├── sql/                       # SQL scripts
│   ├── 01_schema.sql         # Database/schema creation
│   ├── 02_tables.sql         # Table definitions
│   ├── 03_procedures.sql     # Stored procedures
│   └── 04_functions.sql      # User-defined functions
├── src/                       # Source code
│   ├── fmp_client.py         # FMP API client
│   ├── snowflake_client.py   # Snowflake utilities
│   └── analysis.py           # Analysis functions
└── docs/                      # Documentation
    └── setup_guide.md        # Detailed setup
```

## Usage

### Adding Tickers to Watchlist
1. Click "➕ Add Ticker" in the sidebar
2. Enter ticker symbol and company name
3. Transcripts will automatically load from FMP API

### Analyzing Transcripts
1. Navigate to a ticker's transcript list
2. Click "🤖 Analyze" to run AI analysis
3. View comprehensive analysis including:
   - Financial performance
   - Forward guidance
   - Competitive positioning
   - Strategic initiatives
   - Risk factors
   - Management sentiment

### Querying Multiple Transcripts
1. Go to ticker detail view
2. Open "🤖 AI Query" section
3. Select date range
4. Ask questions across multiple quarters
5. Get AI-synthesized insights

## API Configuration

### FMP API Endpoints Used
- Earnings Call Transcripts: `/api/v3/earning_call_transcript/{symbol}`
- Company Quote: `/api/v3/quote/{symbol}`

### Snowflake Cortex Models
- `mixtral-8x7b` - For extraction and analysis
- `llama2-70b-chat` - For comprehensive summaries

## Environment Variables

Create a `.env` file with:
```bash
# FMP API
FMP_API_KEY=your_api_key_here

# Snowflake
SNOWFLAKE_ACCOUNT=your_account
SNOWFLAKE_USER=your_username
SNOWFLAKE_PASSWORD=your_password
SNOWFLAKE_WAREHOUSE=your_warehouse
SNOWFLAKE_DATABASE=EARNINGS_CALLS
SNOWFLAKE_SCHEMA=RAW_DATA
SNOWFLAKE_ROLE=your_role
```

## Troubleshooting

### Common Issues

1. **"Transcript loading requires FMP API integration"**
   - Ensure FMP API key is configured
   - Check API rate limits

2. **"AI analysis requires Snowflake Cortex LLM"**
   - Verify Cortex is enabled in your Snowflake account
   - Check model availability (mixtral-8x7b, llama2-70b)

3. **"Some stored procedures may not exist yet"**
   - Run SQL setup scripts in order
   - Verify procedures created successfully

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

MIT License - see LICENSE file for details

## Acknowledgments

- Financial Modeling Prep for transcript data
- Snowflake Cortex for AI analysis
- Streamlit for the dashboard framework
