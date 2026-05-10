# Niocess External API Simulator

Small external API simulator for Niocess benchmark/demo scenarios.

It exposes predictable API endpoints with configurable response delay, so JMeter or k6 can compare direct calls against calls protected by the Niocess execution layer.

## Endpoints

- `GET /health`
- `GET /metrics`
- `POST /metrics/reset`
- `GET /external/pricing?productId=123&delayMs=500`
- `GET /external/risk-score?userId=456&delayMs=500`
- `GET /external/analytics/report?tenantId=123&period=30d&delayMs=1000`
- `POST /external/ai/summary?delayMs=1000`

## Delay Controls

Use a query parameter for per-request delay:

```bash
curl "http://localhost:8090/external/pricing?productId=123&delayMs=500"
```

Or use environment variables:

```bash
EXTERNAL_API_DELAY_MS=500 npm start
```

For random delay:

```bash
EXTERNAL_API_MIN_DELAY_MS=100 EXTERNAL_API_MAX_DELAY_MS=1000 npm start
```

## Run Locally

```bash
npm start
```

## Run With Docker

```bash
docker compose up --build
```

## Benchmark Use

Direct scenario:

```text
JMeter -> Spring App -> Niocess External API Simulator
```

With Niocess layer:

```text
JMeter -> Spring App -> Niocess Layer -> Niocess External API Simulator
```

The most important metric is the difference between incoming client requests and actual calls received by this simulator, visible through `GET /metrics`.
