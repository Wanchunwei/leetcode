# Algorithm

Binary Search with two pointer

# Better solution 

Binary Search (Find start point for K closest elements)

Analysis (for better solution):

1. Find start point 0 and end point arr.lengh - k for start element
2. Find the condition that can throw half of the array
   - if x < arr[mid], then the start element should also smaller than arr[mid]. 
   - if x > arr[mid], but x - arr[mid] > arr[mid + k] - x, then the start point should be larger than arr[mid] 
   - else the start point should still be smaller than arr[mid]

```java
public List<Integer> findClosestElements(List<Integer> arr, int k, int x) {
    int lo = 0, hi = arr.size() - k;
    while (lo < hi) {
        int mid = (lo + hi) / 2;
        if (x - arr.get(mid) > arr.get(mid+k) - x)
            lo = mid + 1;
        else
            hi = mid;
    }
    return arr.subList(lo, lo + k);
}
```

## Performance:

Runtime: 6 ms, faster than 47.27% of Java online submissions for Find K Closest Elements.

Memory Usage: 40.1 MB, less than 88.31% of Java online submissions for Find K Closest Elements.

## Time spent:

Not Done

## Times of Wrong answer:

2 - Bug 1, Bug 2

## Solution

```java
class Solution {
    public List<Integer> findClosestElements(int[] arr, int k, int x) {
        List<Integer> results = new ArrayList<>();
        if (arr == null || arr.length == 0 || k == 0) {
            return results;
        }
        
        int start = 0, end = arr.length - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (arr[mid] > x) {
                end = mid;
            } else if (arr[mid] < x) {
                start = mid;
            } else {
                start = mid;
            }
        }
        
        if (arr[start] == x) {
            results = findCloestk(start, start, arr, x, k);
        } else if (arr[end] == x) {
            results = findCloestk(end, end, arr, x, k);
        } else {
            results = findCloestk(start, end, arr, x, k);
        }
        
        return results;
    }
    
    private List<Integer> findCloestk(int start, int end, int[] arr, int x, int k) {
        List<Integer> results = new ArrayList<>();
        List<Integer> resultsSmall = new ArrayList<>();
        List<Integer> resultsLarge = new ArrayList<>();
        if (k <= 0) {
            return results;
        }
        
        if (start == end) {
            start--;
        }        
        
        while (k > 0) {
            if (start < 0) {
                resultsLarge.add(arr[end]);
                end++;
            } else if (end >= arr.length) {
                resultsSmall.add(arr[start]);
                start--;
            } else {
                if (x - arr[start] <= arr[end] - x) {
                    resultsSmall.add(arr[start]);
                    start--;
                } else {
                    resultsLarge.add(arr[end]);
                    end++;
                }
            }
            
            k--;      
        }
        
        for (int i = resultsSmall.size() - 1; i >= 0; i--) {
            results.add(resultsSmall.get(i));
        }
        
        for (int i = 0; i < resultsLarge.size(); i++) {
            results.add(resultsLarge.get(i));
        }
        
        return results;
    }
}
```

# Time complexity

log (n) + k

# Notes and Tips

