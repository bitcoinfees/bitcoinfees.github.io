---
title: FAQ
layout: default
permalink: /faq/
navactive: FAQ
---

## Frequently Asked Questions

### Why is there a graph for a 12 min wait time, but not for 10 min?

At difficulty equilibrium (unchanging hashrate; difficulty neither increasing nor decreasing),
blocks arrive every 10 minutes on average. The best average wait time possible for a transaction
is thus 10 minutes.

In real world conditions, however, hashrate is changing all the time. If hashrate is decreasing,
the average inter-block time would be more than 10 minutes. Regardless of how high a fee you pay, you
would not be able to attain an average wait time of 10 minutes.

A 10 min fee graph would, therefore, occasionally have an undefined value. To avoid this, we use
12 minutes instead.

### Is there a way to resize the graph axes?

Yes! Click and drag a box over the graph to set the viewing range. Double clicking on the graph
then resets the axes.

### Why does the fee graph seem to have a floor of 5000 satoshis/kB?

The floor is determined by the minrelaytxfee setting of my Bitcoin node. It's possible you
could get confirmations at a lower fee rate, but my node wouldn't be able to tell.

### The mempool size doesn't seem to correspond with other sites.

The mempool size graph discounts transactions with fee rate lower than minrelaytxfee. The graph
thus reflects the queue of fee-paying transactions, which is what we're interested in.

To see the mempool size vs fee rate, refer to [this graph](/misc/profile).

### What is "capacity byterate"?

It's the estimated average blockmaxsize of the network, times the estimated block rate.
It represents the capacity of the network, not taking into account the min fee rate of miners.
In practice the actual capacity depends on the fee rates of transactions and the
min fee rate policies that the miners choose.

For the distribution of max block size and min fee rate, see [here](/misc/mining). 

### I still have questions!

Feel free to [contact me!](mailto:bitcoinfees@gmail.com)
