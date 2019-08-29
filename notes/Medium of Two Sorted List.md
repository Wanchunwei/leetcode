# Algorithm

Merge Sort

# Better solution

Currently Best

## Performance:

Runtime: 2 ms, faster than 100.00% of Java online submissions for Median of Two Sorted Arrays.

Memory Usage: 46.1 MB, less than 92.36% of Java online submissions for Median of Two Sorted Arrays.

## Time spent:

30 min 21 seconds 

## Times of Wrong answer:

2 - Bug 1, Bug 2

## Solution

```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        if ((nums1.length + nums2.length) % 2 != 0) {
            return findKth(nums1, 0, nums2, 0, (nums1.length + nums2.length) / 2 + 1);
        }
        //Bug 1 : Here we must write 2.0 rather than 2 because we return a double value
        return (findKth(nums1, 0, nums2, 0, (nums1.length + nums2.length) / 2) + 
               findKth(nums1, 0, nums2, 0, (nums1.length + nums2.length) / 2 + 1)) / 2.0;
    }
    
    private int findKth(int[] nums1, int start1, int[] nums2, int start2, int k) {
        if (k == 1) {
            if (start1 >= nums1.length) {
                return nums2[start2];
            }
            
            if (start2 >= nums2.length) {
                return nums1[start1];
            }
            
            return Math.min(nums1[start1], nums2[start2]);
        }
        
        // Bug 2 : Be careful of the corner case that if the remaining length of one of the two arrays is length than k/2  
        if (nums1.length - start1 < k/2) {
            start2 = start2 + k/2;
        } else if (nums2.length - start2 < k/2) {
            start1 = start1 + k/2;
        } else if (nums1[start1 + k/2 - 1] > nums2[start2 + k/2 - 1]) {
            start2 = start2 + k/2;
        } else {
            start1 = start1 + k/2;
        }
        
        return findKth(nums1, start1, nums2, start2, k - k/2);
    }
}
```

# Time complexity

O(n*log(k))

# Notes and Tips

1. Here we must write 2.0 rather than 2 because our function returns a double value
2. Be careful of the corner case that if the remaining length of one of the two arrays is length than k/2