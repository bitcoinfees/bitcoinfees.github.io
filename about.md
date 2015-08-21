---
title: About
layout: default
permalink: /about/
navactive: About
---

## What is this?

This site diplays real-time estimates of required Bitcoin transaction fees (i.e. miner's fee). The estimates are
given in satoshis per kB of transaction size ("fee rate"), and with respect to a given expected wait time
(time spent waiting to be included in a block).

The estimated are updated every minute.

## How are the estimates obtained?

The estimates are obtained by Monte Carlo simulation of a queueing model of the Bitcoin network.
Both miner selection policy and transaction arrival statistics are modeled and estimated.

From the simulations we can obtain the transient distribution of the wait time of a transaction with
a given fee rate, conditioned on the current mempool state, and hence derive the fee estimates.

The simulation software is open source and can be found [here](https://github.com/bitcoinfees/bitcoin-feemodel).

## How accurate are the results?

For each new transaction, the program predicts a wait time distribution based on its
feerate. When the transaction has entered a block, the p-value corresponding to the
observed wait time is recorded. Under the null hypothesis of the model, the p-value is
uniformly distributed in the interval `[0, 1]`. By comparing the empirical distribution
of p-values to the uniform distribution, we can gauge the model validity; the plots
are shown [here](/misc/pvals).

---

## Model overview

### [Mining](/misc/mining)

* Block discovery occurs as a Poisson process.
* Miners select transactions greedily by highest feerate, subject to a minimum feerate
and a maximum block size
* "Orphan" transactions (transactions with mempool dependencies) are considered only after
its parent has been selected (i.e. no child-pays-for-parent).
* No modeling of minimum and priority block size, for simplicity.
* The min fee rate and max block size parameters for each block are modeled as independent random variables.

### [Transaction arrivals](/misc/profile)

* Arrivals occur as a Poisson process.
* Each transaction is represented by `(feerate, size)`, independently drawn from a certain joint distribution.

## Parameter estimation overview

### Mining

* Overall hashrate is estimated over an interval of 2 weeks.
* Max block size policy distribution is taken from the actual block size empirical distribution, when mempool size is relatively large.
* Min fee rate policy distribution is taken from the "stranding fee rate" empirical distribution, when mempool size is relatively small.
* The "stranding fee rate" is an estimate of the minimum fee rate needed to get into a particular block.

### Transaction arrivals

* Transaction statistics estimated using a exponential moving average with a halflife of 1 hour.
