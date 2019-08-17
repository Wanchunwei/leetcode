# Algorithm

Two Pointers



Analysis:

1. With three variables in an array, make sure one parameter and do two Pointer search for other two variables. 

# Better solution

Currently Best

## Performance:

Runtime: 35 ms, faster than 48.44% of Java online submissions for 3Sum.

Memory Usage: 46.8 MB, less than 90.81% of Java online submissions for 3Sum.

## Time spent:

9 min 37 seconds 

## Times of Wrong answer:

1

## Solution

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> results = new ArrayList<>();
        Arrays.sort(nums);
        for (int i = 0; i < nums.length - 2; i++) {
            if (i > 0 && nums[i] == nums[i - 1]) {
                continue;
            }
            twoSum(i, i + 1, nums.length - 1, nums, results);
        }
        return results;
    }
    
    private void twoSum(int targetIndex, 
                        int startIndex, 
                        int endIndex, 
                        int[] nums,
                        List<List<Integer>> results) {
        int target = 0 - nums[targetIndex];
        while (startIndex < endIndex) {
            
            if (startIndex < endIndex && nums[startIndex] + nums[endIndex] == target) {
                List<Integer> temp = new ArrayList<>();
                temp.add(nums[targetIndex]);
                temp.add(nums[startIndex]);
                temp.add(nums[endIndex]);
                results.add(temp);
                // Bug 1 : Remember to remove duplicate both in threeSum and twoSum. 
                while (startIndex < endIndex && 
                       nums[startIndex] == nums[startIndex + 1]) {
                    startIndex++;
                }
                startIndex++;
            } else if (startIndex < endIndex && 
                       nums[startIndex] + nums[endIndex] < target) {
                startIndex++;
            } else {
                endIndex--;
            }
        }
    }
}
```

# Time complexity

O(n^2)

# Notes and Tips

1. Remember to remove duplicate both in `threeSum` and `twoSum`. 