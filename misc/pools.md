---
title: Mining Pools
layout: default
permalink: /misc/pools/
navactive: Misc Stats
---

## Sorry, this data is no longer available.

I've moved to a new method of estimating mining policies that does not require
block attribution to mining pools. This is preferable because:

1. Block attribution is not a trivial problem - relying on coinbase tags is problematic for various reasons.  Policy estimates are not very robust with respect to attribution errors.

2. More importantly, it was being observed that there often is significant variation of mining policy within the same pool, suggesting that pools are running multiple mining servers with different policies. In this case, the assumption that a pool has a uniform policy over a period of time breaks down, producing poor estimates.

The new method is non-parametric - it doesn't attempt to group blocks by mining pool. Graphs can be found [here](/misc/mining/); detailed explanation will be available when there is demand.
