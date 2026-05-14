# Stock Predictor AI

Stock Predictor AI is a full-stack machine learning project that forecasts stock prices using deep learning models and serves results through a clean web dashboard and REST API.

The project includes:
- A Flask backend for training and inference workflows
- A model pipeline with `LSTM`, `GRU`, and `Transformer` architectures
- Technical indicator computation (RSI, MACD, Bollinger Bands, moving averages)
- A responsive frontend for analytics and model comparison

## Key Features

- Multi-model forecasting: `LSTM`, `GRU`, and `Transformer`
- Yahoo Finance market data ingestion (`yfinance`)
- End-to-end preprocessing with indicator engineering and scaling
- Evaluation metrics: `RMSE`, `MAE`, `MAPE`
- Next-day close price forecast
- API-driven training, status checks, predictions, and model comparison
- Frontend dashboard with charts and watchlist support

## Tech Stack

- Python 3.11
- Flask + Flask-CORS
- TensorFlow / Keras
- NumPy, Pandas, scikit-learn
- yfinance
- HTML, CSS, JavaScript (chart-based dashboard)
- Gunicorn (production serving)

## Project Structure

```text
Stock_Predictor/
  app.py              Flask API and static file server
  model.py            Data pipeline, model training, evaluation, forecasting
  index.html          Frontend entry page
  css/                Frontend styles
  js/                 Frontend scripts and chart logic
  results/            Saved model outputs (JSON)
  requirements.txt    Python dependencies
  Dockerfile          Container build configuration
  render.yaml         Render deployment configuration
```

## Quick Start

### Option 1: Frontend only

Open `index.html` directly in a browser to explore the UI.
Note: frontend-only mode can use simulated or fallback data.

### Option 2: Full stack (recommended)

1. Install dependencies:

```bash
pip install -r requirements.txt
```

2. Run backend:

```bash
python app.py
```

3. Open the app:

`http://localhost:5000`

## Model Training

### Train from CLI

```bash
python model.py AAPL --models LSTM GRU Transformer
```

### Train via API

```bash
curl -X POST http://localhost:5000/api/train/AAPL \
  -H "Content-Type: application/json" \
  -d '{"models": ["LSTM", "GRU", "Transformer"]}'
```

Training runs in a background thread. Use the status endpoint to check progress.

## API Reference

| Method | Endpoint | Purpose |
|---|---|---|
| `GET` | `/api/predict/<ticker>?model=LSTM` | Return latest prediction set for one model |
| `POST` | `/api/train/<ticker>` | Trigger model training for one ticker |
| `GET` | `/api/status/<ticker>` | Check whether results are ready |
| `GET` | `/api/compare/<ticker>` | Return metrics comparison across trained models |
| `GET` | `/api/indicators/<ticker>` | Return latest computed technical indicators |

Example:

```bash
curl "http://localhost:5000/api/predict/AAPL?model=LSTM"
```

## Deployment

### Docker

```bash
docker build -t stock-predictor-ai .
docker run -p 7860:7860 stock-predictor-ai
```

### Render

The project includes `render.yaml` for deployment with:
- Build command: `pip install -r requirements.txt`
- Start command: `gunicorn app:app --bind 0.0.0.0:$PORT`

## Notes and Limitations

- This project is intended for educational and research use.
- Model outputs are sensitive to data window, volatility, and retraining frequency.
- Predictions are not financial advice.

## License

No license file is currently included. Add a license before public or commercial reuse.
