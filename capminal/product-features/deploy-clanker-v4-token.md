---
description: >-
  Capminal is a Clanker UI, here is our guideline to prompt and deploy token on
  Clanker V4
---

# Deploy Clanker V4 Token

## Clanker V4 Introduction

Clanker V4 has been released with numerous exciting features, enabling flexible configuration of Uniswap V4 pools, particularly for diverse liquidity provision across specific ranges and optimizing pool reward distribution.

Additionally, pool fees are now highly customizable, supporting up to 7 addresses for fee distribution. Unlike V3’s fixed 1% fee, fees can now be dynamically set from 0% to 30% or vary by liquidity range, depending on whether Static or Dynamic Hooks are used.

Clanker V4 introduces an extension system, offering extensive customization for Clanker Token. Alongside the DevBuy extension, it includes ClankerVault and ClankerAirdrop, each with unique functionalities. For more details, check the official [Clanker Documentation](https://clanker.gitbook.io/clanker-documentation/core-contracts/v4.0.0).

## What types of configurations does Capminal support

Since Capminal is an AI Agent and users will deploy tokens via prompting on our client, we have simplified the configuration process for launching Clanker V4 tokens.&#x20;

We will allow customization of the following two configurations:

1. **Pool Fee (default: 1%)**: Supports configuration from **1%** to **10%** and only supports static hooks (applying the same fee across all liquidity).
2. **Initial Buy (default: zero)**: Allows creators to execute the first transaction with a specified amount of ETH.
3. **Reward Recipient:** Currently, when fees are generated from a transaction, we maintain three fixed reward recipients: **Clanker Team** (currently fixed 0.2% at protocol level), Capminal Team, and Creator. We will support configuring additional reward recipients in the future.

{% hint style="warning" %}
We have observed that pool fees above 10% are highly risky for swappers. We recommend deploying tokens with a **1%** to **3%** fee. A 10% fee means that when a user swaps $1000, they pay $100 in fees, which discourages swapping, especially in specific cases.
{% endhint %}

## Deploy prompt

```
Deploy token DackieSwap, token symbol DACKIE
```

```
Deploy token Capminal, token symbol CAP, with pool fee is 3%
```

```
Deploy token DackieVerse, token symbol VERSE then initial buy 1 ETH
```

## Fee Structure

With the Clanker V4 update, the Clanker Team now earns **0.2%** at the protocol level for all transactions. The generated swap fees will be distributed to the Capminal Team and Creator according to the rates in the table below.

<table><thead><tr><th width="139.05078125">#</th><th width="196.828125">% separated </th><th>Example: </th></tr></thead><tbody><tr><td></td><td>In 1% Trading Fee</td><td>If Swap Volume is $10,000 -> Trading Fee is $100</td></tr><tr><td>Creator</td><td><strong>70%</strong></td><td>Earn <strong>70$</strong></td></tr><tr><td>Capminal</td><td><strong>30%</strong></td><td>Earn <strong>30$</strong></td></tr></tbody></table>

