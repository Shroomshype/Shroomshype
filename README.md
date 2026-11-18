<div align="center">

# Shrooms

**A game layer over Uniswap on Robinhood Chain.**

Provide liquidity to a curated Uniswap pool, stake the position here, and earn
SPORES on top of the fees that pool already pays you — funded by real fee
income, never printed from an emission schedule.

[Contracts](https://github.com/Shroomshype/shrooms-robinhood-contracts) ·
[Web](https://github.com/Shroomshype/shrooms-robinhood-web) ·
[Keeper](https://github.com/Shroomshype/shrooms-robinhood-keeper) ·
[X](https://x.com/Shroomshype) ·
[Telegram](https://t.me/shroomshype)

</div>

---

### The short version

Most farm tokens die the same way: emissions outrun demand, price falls, yields
look worse, stakers leave, and the whole thing unwinds.

Shrooms has no emissions. SPORES is minted only against ETH the treasury has
already received in fees, so supply is an output of real activity rather than a
policy. Every SPORES is redeemable for a slice of that treasury, and the
redemption floor can never fall — it is asserted on chain, not merely intended.

Spending SPORES on in-game boosts burns it and leaves the ETH behind. The
players who play make the token worth more for the players who leave.

---

## v4.0 — Robinhood Chain

The current build. We run no pools of our own: every strain is a real Uniswap
pool, and what the farm custodies is the **position NFT** you get back from
Uniswap. Positions are read through a per-venue adapter, so Uniswap v3 and v4
share one copy of the reward accounting instead of a farm each.

| | |
|---|---|
| [**shrooms-robinhood-contracts**](https://github.com/Shroomshype/shrooms-robinhood-contracts) | Solidity, venue adapters, 109 tests, deploy and simulation scripts |
| [**shrooms-robinhood-web**](https://github.com/Shroomshype/shrooms-robinhood-web) | Six static pages, no build step |
| [**shrooms-robinhood-keeper**](https://github.com/Shroomshype/shrooms-robinhood-keeper) | Unwraps fee income, drips, splits rewards, starts each period |

Three things worth knowing before reading the code:

- **Weight is in-range liquidity.** A position outside the current price gives
  the pool nothing, so it earns nothing here. Crediting is re-checkpointed by a
  permissionless `poke`, because price moves without any transaction touching
  the contract.
- **Rewards come in two streams that cannot mix.** SHROOMS pairs are funded by
  trading fees on SHROOMS; partner pools by swap fees this interface earns.
  Paying partner liquidity out of SHROOMS fee income would hand SHROOMS
  holders' rewards to people who never bought SHROOMS, so the contract refuses.
- **Every APR on the site is Uniswap's own**, not ours. We don't pay it and
  can't control it, and the pages say so where the numbers appear.

**Status:** running on **Robinhood Chain testnet** (`46630`). **Unaudited** —
testnet only, and the figures on the site are simulations until there is
trading to measure.

---

## v3.0 — Elysium

The previous build, kept for reference. Same treasury design, different chain,
and the farm ran its own pools with a fungible LP token rather than custodying
Uniswap positions.

| | |
|---|---|
| [shrooms-contracts](https://github.com/Shroomshype/shrooms-contracts) | Solidity, tests, deployment and simulation scripts |
| [shrooms-web](https://github.com/Shroomshype/shrooms-web) | The five-page front end |
| [shrooms-keeper](https://github.com/Shroomshype/shrooms-keeper) | Calls the permissionless weekly drip |

Not maintained. Start with v4 above.
