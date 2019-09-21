# Algorithm 

DP

# Better solution 

Currently Best

# Solution 

```java
class Solution {
    public int coinChange(int[] coins, int amount) {
        if (coins == null || coins.length == 0) {
            return -1;
        }
        
        int[] numOfCoins = new int[amount + 1];
        for (int i = 1; i <= amount; i++) {
            numOfCoins[i] = Integer.MAX_VALUE;
            for (int j = 0; j < coins.length; j++) {
                //Notation : Corner case, if i - coins[j] can not be made up by coins
                if (i - coins[j] >= 0 && numOfCoins[i - coins[j]] != Integer.MAX_VALUE) {
                    numOfCoins[i] = Math.min(numOfCoins[i], numOfCoins[i - coins[j]] + 1);
                }
            }
        }
        
        if (numOfCoins[amount] == Integer.MAX_VALUE) {
            return -1;
        }
        return numOfCoins[amount];
    }
}
```



# Time complexity

O(n^2)

# Notes and Tips

1. Corner case : i - i - coins[j] < 0 and if i - coins[j] can not be made up by coins