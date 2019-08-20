# Algorithm

Two Pointers

# Better solution

Currently Best

## Performance:

Runtime: **0 ms**

Memory Usage: **35.1 MB**

## Time spent

12 min 

## Times of Wrong answer:

1 - Bug 1

## Solution

```java
class Solution {
    public void sortColors(int[] nums) {
        if (nums == null || nums.length == 0) {
            return;
        }
        
        int index = 0, left = 0, right = nums.length - 1;
        while (index <= right) {
            if (nums[index] == 0) {
                int temp = nums[index];
                nums[index] = nums[left];
                nums[left] = temp;
                left++;
                //Bug 1 : Remember to do `index++` if `left > index`
                if (index < left) {
                    index++;
                }
            } else if (nums[index] == 2) {
                int temp = nums[index];
                nums[index] = nums[right];
                nums[right] = temp;
                right--;
            } else {
                index++;
            }
        }
        
        return;
    }
}
```

# Time complexity

O(n)

# Notes and Tips

1. Remember to do `index++` if `left > index`