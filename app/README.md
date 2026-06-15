# US Accident Analytics Dashboard

A full-stack web application for analyzing and visualizing US traffic accident data with interactive maps, charts, and statistical insights.

## Getting Started

### Prerequisites

- Python 3.8 or higher
- Node.js 14 or higher and npm
- CSV data files in the `../data/` directory:
  - `us_accidents_clean.csv`
  - `us_accidents_city_summary.csv`
  - `us_accidents_state_year.csv`
  - `us_accidents_state_weather.csv`

### Installation

1. **Install Python dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

2. **Install frontend dependencies:**
   ```bash
   cd frontend
   npm install
   cd ..
   ```

### Running the Application

The application requires two separate terminals - one for the backend API server and one for the frontend development server.

#### Terminal 1: Backend Server

```bash
cd backend
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

The backend server will:
- Start loading all datasets on startup (takes 1-2 minutes)
- Be available at `http://localhost:8000`
- Provide API documentation at `http://localhost:8000/docs`

#### Terminal 2: Frontend Server

```bash
cd frontend
npm start
```

The frontend will:
- Start on `http://localhost:3000`
- Automatically open in your browser
- Show a loading screen until backend data is ready
- Give it a minute or two for all the stats to be displayed on the frontend

### Testing

To test the custom DataFrame functions and operations, open `test.ipynb` in Jupyter Notebook. The notebook contains tests for all major functions including filtering, aggregation, joins, and data manipulation operations using the actual accident datasets.

## Application Overview

This application provides an interactive dashboard for exploring US traffic accident data from 2016-2023. Users can:

- **View interactive heatmaps** of accident locations across US cities
- **Analyze severity distributions** and trends over time
- **Explore weather conditions** and their correlation with accidents
- **Compare statistics** across states and cities
- **Filter data** by severity, time of day, and geographic location

### Workflow

1. **Data Loading**: On backend startup, all CSV datasets are loaded into memory using parallel processing
2. **API Requests**: Frontend makes HTTP requests to FastAPI endpoints for different analytics
3. **Data Processing**: Backend services filter, aggregate, and transform data using custom DataFrame operations
4. **Visualization**: React components render interactive charts, maps, and tables
5. **User Interaction**: Filter changes trigger new API requests and chart updates

### Tech Stack

**Backend:**
- FastAPI - Modern Python web framework
- Uvicorn - ASGI server
- Custom DataFrame implementation - Lightweight data manipulation library

**Frontend:**
- React - UI framework
- Leaflet & React-Leaflet - Interactive maps
- Leaflet.Heat - Heatmap visualization

**Data Processing:**
- Custom CSV parser with multiprocessing support
- In-memory DataFrame operations
- Efficient single-pass aggregations

