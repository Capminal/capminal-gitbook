---
description: >-
  The Wallet API Key system allows users and builders to securely access CAP
  wallet through a standardized authentication mechanism
---

# Wallet API Key

## Wallet API Key

The **Wallet API Key** system allows users and builders to securely access CAP services through a standardized authentication mechanism. Users can generate API Keys and import them into external clients (e.g. OpenClaw, Hermes) to execute wallet, trading, and deployment operations.

<figure><img src="../../.gitbook/assets/Screenshot 2026-06-02 at 09.53.36.png" alt=""><figcaption></figcaption></figure>

## Overview

* Secure token-based authentication
* Integration with external clients (e.g., OpenClaw)
* Support for dApp builders
* Programmatic access to wallet, trading, and deployment services

{% hint style="danger" %}
**Important Security Notice:**

Your API Key grants full access to execute trades and transfer funds from your CAP Wallet. If your API Key is compromised, unauthorized parties may drain your wallet.
{% endhint %}

## Generate an API Key

1. Go to **Settings → API Key**
2. Click **Generate New Key**
3. Copy and store the key securely

The API Key is shown only once after creation.

## Manage API Keys

Users can manage their keys in the dashboard:

* **Rotate Key**: Generate a new key to replace the current one if it is compromised or exposed.
* **Delete Key**: Permanently remove a key if it is no longer needed or has security issues.

Key rotation and deletion help maintain system security and operational safety.

## For Builders

Builders can integrate Wallet API Key into their dApps if they require:

* Wallet infrastructure
* Trading execution
* Token deployment

CAP provides the infrastructure layer while builders focus on product development.

## Authentication Example

All API requests must include the API Key in the header:

```http
CAP_API_KEY: YOUR_CAP_API_KEY
```

Example:

```bash
curl -X GET https://api.cap.network/v1/wallet \
  -H "CAP_API_KEY: YOUR_CAP_API_KEY"
```
