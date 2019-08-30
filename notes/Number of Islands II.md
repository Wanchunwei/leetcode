# Algorithm

Union Find

# Better solution

Currently Best

## Performance:

Runtime: 12 ms, faster than 56.32% of Java online submissions for Number of Islands II.

Memory Usage: 53.2 MB, less than 100.00% of Java online submissions for Number of Islands II.

## Time spent:

37 min 47 seconds 

## Times of Wrong answer:

2 - Bug 1, Bug 2

## Solution

```java

class Solution {
    public List<Integer> numIslands2(int m, int n, int[][] positions) {
        List<Integer> num = new ArrayList<>();
        if (positions == null || positions.length == 0) {
            return num;
        }
        
        int[] islands = new int[m*n + 1];
        int count = 0;
        int[] directionX = {0, -1, 0, 1};
        int[] directionY = {-1, 0, 1, 0};
        for (int i = 0; i < positions.length; i++) {
            // Bug 1 : corner case that if the positions is already a land, we don't need any operation.  
            if (islands[positions[i][0]*n + positions[i][1] + 1] == 0) {
                islands[positions[i][0]*n + positions[i][1] + 1] = 
                                         positions[i][0]*n + positions[i][1] + 1;
                count++;
                for (int j = 0; j < 4; j++) {
                    int[] neighbour = {positions[i][0] + directionX[j], 
                                       positions[i][1] + directionY[j]};
                    if (neighbour[0] < 0 || neighbour[0] >= m ||
                        neighbour[1] < 0 || neighbour[1] >= n) {
                        continue;
                    }
                
                    if (islands[neighbour[0]*n + neighbour[1] + 1] != 0) {
                        //Bug 2 : Only when we need to connect two lands, we do count--; 
                        if (connect(islands, 
                                    positions[i][0]*n + positions[i][1] + 1, 
                                    neighbour[0]*n + neighbour[1] + 1)) {
                            count--;
                        }
                    }
                }
            }
            num.add(count);
        }
        return num; 
    }
       
    private boolean connect(int[] islands, int position, int neighbour) {
        int fatherP = find(islands, position);
        int fatherN = find(islands, neighbour);
        if (fatherP != fatherN) {
            islands[fatherP] = fatherN;
            return true;
        }
        return false;
    }
    
    private int find(int[] islands, int position) {
        if (islands[position] == position) {
            return position;
        }
        
        return islands[position] = find(islands, islands[position]);
    }
}
```

# Time complexity

O(m*n + L)

# Notes and Tips

1. Corner case that if the positions is already a land, we don't need any operation.
2. Only when we need to connect two lands, we do count--; 