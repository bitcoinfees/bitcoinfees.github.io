---
title: About
layout: default
permalink: /about/
navactive: About
---

## What is this?

This site shows the results of [a program](https://github.com/bitcoinfees/bitcoin-feemodel)
which runs simulations on a queueing model of the Bitcoin network, in order to determine
the transient distribution of transaction wait times (i.e. time spent in the mempool) as a function
of fee rate, conditioned on:

* The current mempool state.
* Estimates of:
    1. Current transaction arrival statistics.
    2. Mining pool hashrates and transaction selection policies.

The result is a real-time prediction of transaction wait times, updated every minute.


### How's this different from Bitcoin Core's smart fees?

Bitcoin Core's estimates are based on aggregating past wait time measurements, and
at the moment do not allow conditioning on the current mempool state (a large mempool backlog,
for example, would result in longer wait times), or take into account variations in the
transaction arrival rate.

These are possible with the model-based approach employed here; the main tradeoff, however,
is the dependence on the model assumptions, the most tricky of which are the assumptions
about the way miners select block transactions.

Both approaches, however, are useful and serve to validate each other.


### How accurate are the results?

For each new transaction, the program predicts a wait time distribution based on its
feerate. When the transaction has entered a block, the p-value corresponding to the
observed wait time is recorded. Under the null hypothesis of the model, the p-value is
uniformly distributed in the interval `[0, 1]`. By comparing the empirical distribution
of p-values to the uniform distribution, we can gauge the model validity; the plots
are shown [here](/misc/pvals).

---

### Model overview

#### [Mining pools](/misc/pools)

* Block discovery occurs as a Poisson process.
* Miners select transactions greedily by highest feerate, subject to a minimum feerate
and a maximum block size.
* "Orphan" transactions (transactions with mempool dependencies) are considered only after
its parent has been selected (i.e. no child-pays-for-parent).
* No modeling of minimum and priority block size, for simplicity.

#### [Transaction arrivals](/misc/profile)

* Arrivals occur as a Poisson process.
* Each transaction is represented by `(feerate, size)`, independently drawn from a certain joint distribution.

### Parameter estimation overview

Coming soon...
