---
title: FAQ
layout: default
permalink: /faq/
navactive: FAQ
---

### Frequently Asked Questions

#### Do you have an API for the data?

Unfortunately, no. This is just a hobby and I can't commit to maintaining a reliable API.

#### The mempool size doesn't seem to correspond with other sites.

This is probably due to different minrelaytxfee and/or maxmempool settings.

To see the mempool size vs fee rate, refer to [this graph](/misc/profile).

#### What are the color bands in the [mempool graph](/#1m)?
The color bands divide up the mempool size according to the fee rates shown in the upper graph.
For example, the blue portion is the size of all transactions with fee rate greater than the
upper blue graph, at any point in time.

This can be used, for example, to gauge a transaction's position in the mempool backlog, or to
assess whether the fee estimates are reasonable.

#### Why does the fee graph seem to have a floor of 5000 satoshis/kB?

The floor is determined by the minrelaytxfee setting of my Bitcoin node. It's possible you
could get confirmations at a lower fee rate, but my node wouldn't be able to tell.

#### What is "capacity byterate"?

It's the estimated average blockmaxsize of the network, times the estimated block rate.
It represents the capacity of the network, not taking into account the min fee rate of miners.
In practice the actual capacity depends on the fee rates of transactions and the
min fee rate policies that the miners choose.

#### Is there a way to resize the graph axes?

Yes! Click and drag a box over the graph to set the viewing range. Double clicking on the graph
then resets the axes.

For the distribution of max block size and min fee rate, see [here](/misc/mining).

#### I still have questions!

Feel free to [contact me!](mailto:bitcoinfees@gmail.com)
