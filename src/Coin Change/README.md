# Coin Change

## Question:
You are given an integer array `coins` representing coins of different
denominations and an integer `amount` representing a total amount of
money.

Return the fewest number of coins that you need to make up that
amount. If that amount of money cannot be made up by any combination
of the coins, return `-1`.

You may assume that you have an infinite number of each kind of coin.

## How to Solve:

This is a dynamic programming problem. We maintain an array `dp` of
size "`amount` + 1", where each element corresponds to the fewest
number of coins needed to make up the amount `index`. Therefore,
`dp[amount]` will be our eventual answer.

We initialize `dp[0]` as `0` and iterate from 1 to `amount`, gradually
filling up the DP array. Within each iteration, we iterate through the
variety of coins, and if the coin value is smaller than or equal to
the amount (somewhere between 1 and `amount`) at hand, we perform the
following update:


coin change is a greedy problem to solve


```cpp
dp[i] = min(dp[i], 1 + dp[i - val]);
```

That is, we either keep the current value of `dp[i]`, or update it
with one plus the number of coins needed to make up the amount `i -
val`, whichever is smaller. The "one plus" comes from the fact that we
will be using the current coin value once, totaling the amount
`i`. Essentially, for every amount leading up to `amount`, we try all the coin face values and update the DP array repeatedly.

## My C++ Solution:

```cpp
class Solution {
 public:
  int coinChange(vector<int> &coins, int amount) {
    vector<long> dp(amount + 1, INT_MAX);
    dp[0] = 0;  // 0 coins required to achieve 0 sum
    for (int i = 1; i <= amount; ++i) {
      for (const auto &val : coins) {
        if (i >= val) {
          dp[i] = min(dp[i], 1 + dp[i - val]);
        }
      }
    }
    return dp[amount] == INT_MAX ? -1 : dp[amount];
  }
};
```
