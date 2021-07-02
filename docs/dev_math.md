---
id: dev_math
title: HydraDX Math Crate
---

## Overview

https://github.com/galacticcouncil/HydraDX-math

The HydraDX math crate contains all the mathematical formulas for the various implementations of AMM pools.

The main goal of having this math functionality as a separate crate is to make it possible to easily compile it into WebAssembly which allows us to  use the wasm library directly on the frontend. 

This way, we can compute everything that is needed on the frontend side in the same way that it is calculated when a transaction is submitted using
same math and without the need to talk to the node.

Another benefit which domes from this approach - it is easily testable.

### xyk

XYK implementation can be found in amm.rs. It consists of following methods:

```rust
pub fn calculate_spot_price(in_reserve: Balance, out_reserve: Balance, amount: Balance) -> Result<Balance, MathError> {}
pub fn calculate_out_given_in(in_reserve: Balance, out_reserve: Balance, amount_in: Balance) -> Result<Balance, MathError> {}
pub fn calculate_in_given_out(out_reserve: Balance, in_reserve: Balance, amount_out: Balance) -> Result<Balance, MathError> {}
pub fn calculate_liquidity_in(asset_a_reserve: Balance, asset_b_reserve: Balance, amount: Balance) -> Result<Balance, MathError> {}
pub fn calculate_liquidity_out(asset_a_reserve: Balance,
    asset_b_reserve: Balance,
    amount: Balance,
    total_liquidity: Balance,
) -> Result<(Balance, Balance), MathError> {}
```


### HDX

The HydraDX Omnipool math implementation can be found in the hdx module.

It has similar methods as xyk but different parameters are needed.

```rust
pub fn calculate_spot_price(
    in_reserve: Balance,
    out_reserve: Balance,
    in_weight: Balance,
    out_weight: Balance,
    amount: Balance,
) -> Result<Balance, MathError> {}

pub fn calculate_out_given_in(
    in_reserve: Balance,
    out_reserve: Balance,
    in_weight: Balance,
    out_weight: Balance,
    amount: Balance,
) -> Result<Balance, MathError> {}

pub fn calculate_in_given_out(
    in_reserve: Balance,
    out_reserve: Balance,
    in_weight: Balance,
    out_weight: Balance,
    amount: Balance,
) -> Result<Balance, MathError> {}

pub fn calculate_liquidity_in(
    asset_reserve: Balance,
    core_asset_reserve: Balance,
    asset_weight: Balance,
    core_asset_weight: Balance,
    amount: Balance,
) -> Result<Balance, MathError> {}

pub fn calculate_liquidity_out(
    asset_reserve: Balance,
    core_asset_reserve: Balance,
    asset_weight: Balance,
    core_asset_weight: Balance,
    amount: Balance,
) -> Result<(Balance, Balance), MathError> {}

```
