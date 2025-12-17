---
description: Capminal x402 Oschestrator
---

# x402 Orchestrator

x402 Orchestrator is a new capability of Capminal AI Agent that enables users to discover and execute x402 APIs directly from the terminal using natural language prompts.

With x402 Orchestrator, Capminal users can:

* Discover x402 APIs from any supported endpoint
* Understand required methods, parameters, and payment details
* Execute x402 APIs seamlessly with their Capminal wallet

x402 Orchestrator supports both x402 V1 and x402 V2 APIs.

## x402 Discovery Action

The **Discovery Action** allows users to inspect any x402-enabled API and retrieve its full metadata, including:

* Supported x402 version
* Network and payment requirements
* HTTP method (GET / POST)
* Required and optional parameters
* API Prepaid Cost

#### Example Prompt

```
discover x402 api https://www.capminal.ai/api/x402/deploy
```

#### Example Response

```json
[
  {
    "x402Version": 2,
    "network": "eip155:8453",
    "maxAmountRequired": "500000",
    "resource": "https://www.capminal.ai/api/x402/deploy",
    "description": "Flash Clanker Token Deployment API",
    "payTo": "0xF9D1D63F362bBF1EE08aB9AcB36fe74aFC48d5f1",
    "asset": "0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913",
    "method": "POST",
    "properties": {
      "body": {
        "name": { "type": "string", "description": "Token name" },
        "symbol": { "type": "string", "description": "Token symbol" },
        "description": { "type": "string", "description": "Token description" },
        "imageUrl": { "type": "string", "description": "Token image URL" },
        "fee": { "type": "string", "description": "Token fee" },
        "marketCap": { "type": "string", "description": "Token market cap" },
        "ownerAddress": { "type": "string", "description": "Token owner address" },
        "telegramLink": { "type": "string", "description": "Telegram link" },
        "twitterLink": { "type": "string", "description": "Twitter link" },
        "farcasterLink": { "type": "string", "description": "Farcaster link" },
        "websiteLink": { "type": "string", "description": "Website link" }
      }
    },
    "exampleParams": {
      "name": "<your_value_here>",
      "symbol": "<your_value_here>",
      "description": "<your_value_here>",
      "imageUrl": "<your_value_here>",
      "fee": "<your_value_here>",
      "marketCap": "<your_value_here>",
      "ownerAddress": "<your_value_here>",
      "telegramLink": "<your_value_here>",
      "twitterLink": "<your_value_here>",
      "farcasterLink": "<your_value_here>",
      "websiteLink": "<your_value_here>"
    },
    "required": [
      "body.name",
      "body.symbol",
      "body.fee",
      "body.marketCap",
      "body.ownerAddress"
    ]
  }
]
```

#### How to Use the Discovery Result

From the discovery response, users can identify:

* The correct **HTTP method** (GET / POST)
* All **required and optional parameters**
* The **maximum payment amount** required for the API call

⚠️ **Important:**\
Always review `maxAmountRequired` to avoid overpaying when executing the API.

The discovered information is used directly in the execution step below.

## x402 Execution Action

The **Execution Action** allows users to call an x402 API after discovery by providing:

* API URL
* HTTP method
* Parameters
* Required USDC balance in the Capminal wallet

Capminal automatically handles payment signing and execution via x402.

#### Prerequisites

* Ensure your **Capminal wallet** has sufficient **USDC**
* Use parameters that match the discovery output

#### Example Prompt

```
call x402 API https://www.capminal.ai/api/x402/deploy
method: POST
params:
{
  "name": "CAP",
  "symbol": "CAP",
  "marketCap": "high",
  "fee": "1%",
  "ownerAddress": "0xbA8C4xxxxxxxxxxxxxxxxxxxx082720",
  "privyId": "did:privy:cmxxxxxxxxxxxxxxxn96",
  "imageUrl": "https://example.com/example.jpg"
}
```

#### Example Response

```json
{
  "success": true,
  "message": "x402 API called successfully",
  "data": {
    "<response_data_of_this_x402_api>"
  }
}
```

## Summary

With **x402 Orchestrator**, Capminal unifies:

* **Discovery** → understanding x402 APIs
* **Execution** → securely calling paid APIs

All from a single terminal interface, powered by AI.

> **Discover. Decide. Execute.**\
> That is x402 Orchestrator in Capminal.
