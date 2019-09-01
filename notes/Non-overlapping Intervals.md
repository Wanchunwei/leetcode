# Algorithm

Greedy

## Best Solution:

Currently Best

## Performance:

Runtime: 5 ms, faster than 65.89% of Java online submissions for Non-overlapping Intervals.

Memory Usage: 36.2 MB, less than 62.50% of Java online submissions for Non-overlapping Intervals.

## Time spent:

Not Done

## Times of Wrong answer:

None

## Solution

```java
class Solution {
     public int eraseOverlapIntervals(int[][] intervals) {
        if (intervals.length <= 1) return 0;
        Arrays.sort(intervals, new Comparator<int[]>(){
            public int compare(int[] a, int[] b){
                return a[1]-b[1];
            }
        });
        
        int count=1, end=intervals[0][1];
        for (int i=1;i<intervals.length;i++){
            if (intervals[i][0]>=end){
                count++;
                end = intervals[i][1];
            }   
        }
        return intervals.length-count;
    }
}
```



# Time complexity

O(n)

# Notes and Tips

1. Java comparator when sorting: 

   ```java
   Arrays.sort(intervals, new Comparator<int[]>(){
       public int compare(int[] a, int[] b){
           return a[1]-b[1]; //From small to large
       }
   });
   ```

   