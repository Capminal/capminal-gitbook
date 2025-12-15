---
description: Capminal x402 AI‑powered Token Deep Research API
---

# Reseach API (paused)

{% hint style="danger" %}
This API is currently on hold because its response is too slow and not compatible with the x402 standard.
{% endhint %}

AI‑powered token deep research delivered on demand, paid per request via x402.

## Endpoint

* Host: `https://capminal.ai/api/x402/`
* Method: `GET`
* Path: `/research`

## Authentication (payment)

* This endpoint is protected by x402 micropayments.
* First call without `X-PAYMENT` → you’ll receive `402 Payment Required` with live payment instructions.
* Pay, then retry with `X-PAYMENT: <payment-proof>`.

## Pricing

* ~~**$0.5**~~ **$0.01** per successful request on **Base**
* Query parameters:
  * `chainId` (string, required): EVM chain id. Example: `8453` for Base
  * `tokenAddress` (string, required): Token contract, `0x` + 40 hex chars

## Headers

* `X-PAYMENT` (string): Cryptographic proof of payment sent on retry

## Request/response

1. Initial request (expect 402):

```bash
curl -X GET \
  'https://capminal.ai/api/x402/research?chainId=8453&tokenAddress=0xdAC17F958D2ee523a2206206994597C13D831ec7'
```

Example 402 response (shape may include additional fields):

```json
{
  "success": false,
  "message": "Payment Required",
  "statusCode": 402,
  "paymentRequirements": {
    "scheme": "exact",
    "network": "base",
    "price": { "display": "$0.5", "amount": "500000", "currency": "USDC", "decimals": 6 },
    "resource": "https://<your-host>/x402/research?chainId=8453&tokenAddress=...",
    "maxTimeoutSeconds": 300,
    "extra": {
      "inputSchema": {
        "type": "object",
        "required": ["chainId", "tokenAddress"]
      }
    }
  }
}
```

2. Retry with payment proof:

```bash
curl -X GET \
  -H 'X-PAYMENT: <facilitator-payment-proof>' \
  'https://capminal.ai/api/x402/research?chainId=8453&tokenAddress=0xdAC17F958D2ee523a2206206994597C13D831ec7'
```

Success (200) response:

```json
{
  "success": true,
  "message": "Token research completed successfully",
  "data": {
    "tokenInfo": {
      "id": "...",
      "type": "token",
      "attributes": {
        "address": "0x...",
        "name": "...",
        "symbol": "...",
        "gt_score": 0,
        "holders": { "count": 0 }
      }
    },
    "analysis": "AI‑generated analysis text."
  }
}
```

## Errors

* `400 Bad Request`: Missing/invalid `chainId` or `tokenAddress`&#x20;
* `402 Payment Required`: Missing/invalid payment or not yet paid
* `503 Service Unavailable`: Upstream data source temporarily unavailable

## Tips

* Keep the request URL identical between the first call and the retry
* Show a wallet deep link/QR for quick payment UX
* Cache inputs so users don’t retype on retry
