```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<Integer> list = new ArrayList<>();
        List<List<Integer>> result = new ArrayList<>();
        
        subsethelper(result, list, nums, 0);
        
        return result;
    }
    
    public void subsethelper(List<List<Integer>> result,
                     List<Integer> list,
                     int[] nums,
                     int pos){
        result.add(new ArrayList<>(list));
        
        for(int i = pos; i < nums.length; i++){
            list.add(nums[i]);
            subsethelper(result, list, nums, i + 1);
            list.remove(list.size() - 1);
        }
    }
}
```
