# Algorithm

Sliding Window (Two pointer)



Analysis : 

1. Two pointer : one for `buy`, one for `prices[i]`
2. if (prices[i] > buy). then we compare it with our profit and record it.
3. if (prices[i] <= buy). then this is a possible `buy`, we set `buy` to `prices[i]`

# Better solution

Currently Best

## Performance:

Runtime: 1 ms, faster than 88.95% of Java online submissions for Best Time to Buy and Sell Stock.

Memory Usage: 37.4 MB, less than 100.00% of Java online submissions for Best Time to Buy and Sell Stock.

## Time spent:

7 min 51 seconds 

## Times of Wrong answer:

None

## Solution

```java
class Solution {
    public int maxProfit(int[] prices) {
        if (prices == null ||prices.length == 0) {
            return 0;
        }
        
        int buy = prices[0], profit = 0;
        for (int i = 1; i < prices.length; i++) {
            if (prices[i] <= buy) {
                buy = prices[i];
                continue;
            }
            
            if (prices[i] > buy && prices[i] - buy > profit) {
                profit = prices[i] - buy;
            }
        }
        
        return profit;
    }
}
```

# Time complexity

O(n)

# Notes and Tips

