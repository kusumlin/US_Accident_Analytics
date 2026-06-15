# US Accident Analytics Dashboard

A full-stack web application for analyzing and visualizing US traffic accident data with interactive maps, charts, and statistical insights. This project features a **custom-built DataFrame implementation** and CSV parser, providing a lightweight alternative to pandas for data manipulation and analysis.

## Custom Functions & Implementation

This project's core strength lies in its **custom-built data processing framework** implemented from scratch:

### Custom DataFrame Class (`app/functions.py`)

A lightweight DataFrame implementation that provides pandas-like functionality:

- **Data Manipulation**: `filter()`, `select()`, `drop()`, `sort()`, `join()` (inner, left, right, outer)
- **Aggregations**: `groupby()`, `aggregate()` with support for sum, mean, count, min, max
- **Column Operations**: `add_column()`, `rename_columns()`, `fillna_column()`, `convert_column_type()`, `round_column()`
- **Data Inspection**: `head()`, `tail()`, `shape()`, `copy()`
- **GroupBy Operations**: Full support for grouped aggregations with `GroupBy` class

### Custom CSV Parser

- **`read_csv()`**: Single-threaded CSV parser with:
  - Quoted field handling (commas inside quotes)
  - Automatic type inference (int, float, string)
  - Chunked reading for memory efficiency
  - Progress indicators

- **`read_csv_parallel()`**: Multi-process CSV parser for large files:
  - Parallel processing using multiprocessing
  - Automatic chunking and distribution across CPU cores
  - Optimized for files several GB in size
  - Significantly faster than single-threaded parsing

### Key Features

- **Zero external data dependencies**: No pandas, numpy, or other heavy libraries required for core functionality
- **Memory efficient**: Columnar storage and optimized data structures
- **Type-safe operations**: Automatic type inference and conversion
- **Production-ready**: Used throughout the backend API for all data operations

## Getting Started

### Prerequisites

- Python 3.8 or higher
- Node.js 14 or higher and npm

### Data Setup

Due to file size limitations, the data files are hosted on Google Drive.

1. **Download the data:**
   - Download `data.zip` from [Google Drive Link](https://drive.google.com/file/d/1hsKbnboeKkd8PAH9RF3Cgfui9dBgOPnS/view?usp=sharing)
   - Extract the zip file to the project root directory
   - Ensure the `data/` folder contains:
     - `us_accidents_clean.csv`
     - `us_accidents_city_summary.csv`
     - `us_accidents_state_year.csv`
     - `us_accidents_state_weather.csv`

### Installation

1. **Install Python dependencies:**
   ```bash
   pip install -r app/backend/requirements.txt
   ```

2. **Install frontend dependencies:**
   ```bash
   cd app/frontend
   npm install
   cd ../..
   ```

### Running the Application

The application requires two separate terminals — one for the backend API server and one for the frontend development server.

#### Terminal 1: Backend Server

```bash
cd app/backend
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

The backend server will:
- Start loading all datasets on startup using `read_csv_parallel()` (takes 1-2 minutes)
- Be available at `http://localhost:8000`
- Provide API documentation at `http://localhost:8000/docs`

#### Terminal 2: Frontend Server

```bash
cd app/frontend
npm start
```

The frontend will:
- Start on `http://localhost:3000`
- Automatically open in your browser
- Show a loading screen until backend data is ready
- Give it a minute or two for all the stats to be displayed on the frontend

### Testing

To test the custom DataFrame functions and operations, open `app/test.ipynb` in Jupyter Notebook. The notebook contains tests for all major functions including filtering, aggregation, joins, and data manipulation operations using the actual accident datasets.

## Application Overview

This application provides an interactive dashboard for exploring US traffic accident data from 2016–2023. Users can:

- **View interactive heatmaps** of accident locations across US cities
- **Analyze severity distributions** and trends over time
- **Explore weather conditions** and their correlation with accidents
- **Compare statistics** across states and cities
- **Filter data** by severity, time of day, and geographic location

### Workflow

1. **Data Loading**: On backend startup, all CSV datasets are loaded into memory using `read_csv_parallel()` for fast multi-process parsing
2. **API Requests**: Frontend makes HTTP requests to FastAPI endpoints for different analytics
3. **Data Processing**: Backend services filter, aggregate, and transform data using custom DataFrame operations
4. **Visualization**: React components render interactive charts, maps, and tables
5. **User Interaction**: Filter changes trigger new API requests and chart updates

### Tech Stack

**Backend:**
- FastAPI — Modern Python web framework
- Uvicorn — ASGI server
- **Custom DataFrame implementation** — Lightweight data manipulation library (no pandas dependency)

**Frontend:**
- React — UI framework
- Leaflet & React-Leaflet — Interactive maps
- Leaflet.Heat — Heatmap visualization

**Data Processing:**
- **Custom CSV parser** with multiprocessing support (`read_csv_parallel`)
- **In-memory DataFrame operations** (filter, groupby, join, aggregate)
- Efficient single-pass aggregations
