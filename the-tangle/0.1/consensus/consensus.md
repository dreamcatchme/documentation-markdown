# MCMC

The white paper suggests a distributed approach, which gives a probabilistic

answer. This is similar to Bitcoin and other distributed ledgers, where at any given time

a transaction has a _confirmation confidence_, which is an indication of its

acceptance level.



## Determining Confirmation

In order to know the confirmation confidence for a particular transaction, we

perform the tip selection algorithm 100 times, as described. We then measure how

many of the 100 selected tips reference the transaction in question. If it is

referenced by 80 tips of 100, for example, we say it is 80% confirmed.

The idea is the following: if it is very likely for a chosen tip to reference

a transaction, then new transactions coming in will probably approve it. This

effect will only increase with time, since the weighted walk causes large branches

to grow and small branches to get abandoned.



The number 100 is arbitrary; if you need more accuracy, you may run the walk

more times. Note that different nodes might see different confidence rates

for the same transaction: this is because their view of the tangle is not

identical, and their walks will reach different tips.



