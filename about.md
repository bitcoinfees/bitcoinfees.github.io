---
title: About
layout: default
permalink: /about/
navactive: About
---

## What is this?

This site shows the results of [Feesim](https://github.com/bitcoinfees/feesim),
a Bitcoin fee estimation program. The goal is to estimate the fee rate that a
transaction needs to pay in order to be confirmed within N blocks, and with a
given probability P (currently 90%).

### About Bitcoin transaction fees

The reason to pay transaction fees is to get included in a block ("confirmed")
in a timely manner. There are basically two scenarios in which a low fee will
result in delays.

The first is because the space for transactions in a block is limited. As of May
2016, each block can contain roughly 2000 transactions at the most. If there are
more than 2000 transactions waiting to be confirmed, then miners will choose
those which pay a higher fee, and the remaining transactions will have to wait
for subsequent blocks.

However, because block space has a byte limit rather than a "number of
transactions" limit, the transaction size in bytes has to be taken in account.
Each transaction is typically around 500 bytes, but this number can vary,
depending on how many [outputs](https://en.bitcoin.it/wiki/Transaction) it has,
for example. Thus, miners don't consider the fee paid, but instead the "fee
rate", which is the fee divided by the transaction size.

The second scenario occurs if the transaction fee rate falls below a miner's
minimum fee rate. Each miner typically sets a minimum fee rate that a
transaction must pay; if the fee rate is below this, then the transaction won't
be included even if blocks aren't full. If a transaction's fee rate is less than
most miners' minimum fee rates, the transaction could remain unconfirmed
for a long time.

### Fee estimation algorithm

The algorithm used is model-based:

* Block discovery and transaction arrivals are modeled as Poisson processes
* Miners' are assumed to select transactions greedily by fee rate, subject to a
  maximum block size and minimum fee rate
* The max block size and min fee rate parameters of each block are independent
  random variables
* Transaction arrivals are represented by `(feerate, size)`, obtained from a
  certain joint distribution.

The algorithm estimates the model parameters using mempool data, and then runs
Monte Carlo simulations to obtain the fee estimates. Some of the estimated
parameters can be seen in the [mining policy](/misc/mining) and [wait
profile](/misc/profile) graphs.

In addition, the Feesim program validates the fee estimates by [keeping
tally](/misc/predictscores) of the proportion of transactions which were
confirmed within the predicted number of blocks. If the model is accurate, the
proportions should be close to 90%.

Please see the [project page](https://github.com/bitcoinfees/feesim) for more
details.
