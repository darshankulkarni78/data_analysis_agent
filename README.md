# File Understanding Agent

## Overview

This project is a multi-functional data analysis and visualization agent that can:

- Accept and parse different file formats (CSV, Excel, PDF, Word, Image, Text).
- Extract text or tabular data.
- Perform data analysis on tabular data.
- Generate visualizations.
- Query LLMs using Together AI API for insights.

## Setup

1. **Clone Repository**

Clone this codebase to your local machine.

2. **Install Dependencies**

Install required Python packages:
```
pip install pandas numpy matplotlib seaborn pytesseract python-docx pdfplumber pymupdf python-dotenv requests
```
Note: Tesseract OCR must be installed on your system for image processing.

3. **Create Environment File**

Create a `.env` file in the root directory:
```
TOGETHER_API_KEY=your_together_ai_api_key
```
Replace `your_together_ai_api_key` with your actual Together AI API key.

4. **Create Figures Directory**

Create a folder `figures` in the root directory to store generated plots.


## Code Components

### File Upload & Extraction

- `upload_file(file_bytes, filename)`: Detects file type, parses content, and standardizes data.
- Supports:
  - `.csv`, `.xlsx` → Tabular data extraction using pandas.
  - `.pdf` → Text extraction using pdfplumber and pymupdf fallback.
  - `.docx` → Text extraction using python-docx.
  - `.txt` → Direct text extraction.
  - `.png`, `.jpg`, etc. → OCR text extraction using pytesseract.

### Large Language Model (LLM) Query

- Uses Together AI's Llama-4 model for question answering.
- `ask_llm(question, context)`:
  - Accepts a question and data context.
  - Sends request to Together AI and returns generated answer.

### Data Analysis Functions

- `analyze_data(data, analysis_type, params)`:
  - `describe`: Summary statistics.
  - `correlation`: Correlation matrix for numeric columns.
  - `groupby`: Grouping and aggregation.
  - `zscore_anomaly`: Outlier detection based on Z-score.

### Visualization Functions

- `generate_visualization(data, chart_type, params)`:
  - Supports chart types: `hist`, `bar`, `scatter`, `box`, `heatmap`.
  - Saves visualizations inside `figures/` folder.

### Chat Agent Class

- `ChatAgent`: Maintains conversation state, stores uploaded context, analysis history.

### Notes

- Always verify the columns and data types before running correlation or z-score analysis.

- For new visualizations, ensure correct parameters are provided.

- LLM calls consume Together AI credits.

- File parsing handles multiple formats but assumes clean data for processing.
