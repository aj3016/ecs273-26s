# Homework 4 Client

This folder contains the React frontend for ECS 273 Homework 4. It is based on the Homework 3 JavaScript visualization app and now loads stock data from the FastAPI backend instead of reading local CSV/JSON files directly.

## What This Client Shows

- Stock overview line chart
- t-SNE scatter plot
- News list for the selected stock
- Stock dropdown populated from the backend

When a stock is selected, the frontend requests updated stock prices, t-SNE data, and news from the FastAPI API running on port `8000`.

## Folder Notes

The active frontend is the JavaScript version:

```text
Homework4/client/
├── src/
├── package.json
├── vite.config.js
└── README.md
```

Use the root `Homework4/client` app for the Homework 4 submission.

## Prerequisites

Install Node.js and npm.

The backend must also be running before the frontend can load data. The frontend expects the API at:

```text
http://localhost:8000
```

## Install Client Dependencies

From this folder:

```powershell
cd C:\Users\ajink\Downloads\ECS273\hw3\ecs273-26s\Homework4\client
npm install
```

## Run the Client

Start the Vite development server:

```powershell
npm run dev
```

Open the local URL shown in the terminal, usually:

```text
http://localhost:5173/
```

## Required Backend Steps

In a separate terminal, start MongoDB locally.

Then install and run the server from:

```powershell
cd C:\Users\ajink\Downloads\ECS273\hw3\ecs273-26s\Homework4\server
pip install -r requirements.txt
python import_data.py
uvicorn main:app --reload
```

The import script loads data into the MongoDB database:

```text
stock_agothankar
```

Run `python import_data.py` again if the data folder changes or if MongoDB has been cleared.

## API Endpoints Used

The frontend calls these backend endpoints:

```text
GET /stock_list
GET /stock/{ticker}
GET /tsne/
GET /stocknews/{ticker}
```

## Troubleshooting

If the page says the stock list was not found, make sure MongoDB is running and run:

```powershell
python import_data.py
```

If the browser console shows failed requests to `localhost:8000`, make sure the FastAPI backend is running:

```powershell
uvicorn main:app --reload
```

If port `5173` is already in use, Vite will show another local URL in the terminal. Open that URL instead.

## Assumptions

- MongoDB runs locally on the default port `27017`.
- FastAPI runs locally on port `8000`.
- Stock data, news files, and `tsne.csv` are stored under `Homework4/server/data/`.
- The frontend is intentionally not reading local stock files directly for the main visualizations.
