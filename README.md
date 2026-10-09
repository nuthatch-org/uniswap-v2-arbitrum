# uniswap-v2-arbitrum

A [nuthatch](https://github.com/nuthatch-org/nuthatch) nest: **Uniswap V2 on Arbitrum**.

As `uniswap-v2`, re-pointed at Arbitrum.

One binary, one config file, no graph-node, no gateway, no query fees.

## What it indexes

**Chain:** `arbitrum-one`. **1 contract**, **5 tables**.

| alias | address |
|---|---|
| `factory` | `0xf1d7cc64fb4452f05c498126312ebe29f30fbcf9` |

## Verified

Indexed blocks **496,878,106 to 497,273,932** and sealed **6 events**. Every table below is generated from the vendored ABIs, and the run above is what this nest actually decoded, not an estimate.

## Read this before trusting it

- Quiet chain: 6 events in the 400,000-block verification window, though the factory has **8,775 pairs** historically. The nest is correct; recent activity is thin.

## Run it

```sh
nuthatch init --from https://github.com/nuthatch-org/uniswap-v2-arbitrum
cd uniswap-v2-arbitrum
nuthatch dev --dir . --backfill 50000 --seal-direct
nuthatch sql --dir . "SELECT count(*) FROM \"factory__pair_created\""
```

The endpoint in `nuthatch.toml` is keyless and public, so this file is publishable: a `nuthatch.toml` is pinned into the nest's content address and must never carry a credential. It is enough to follow the tip. A **backfill** wants archive depth it may not have: pass your own with `--rpc`, and check it first with `nuthatch doctor --rpc <url>`.

## Tables

```
factory__pair_created
pair__burn
pair__mint
pair__swap
pair__sync
```
