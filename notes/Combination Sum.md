# Algorithm 

DFS

# Better solution

Currently Best

## Performance:

Runtime: 5 ms, faster than 47.08% of Java online submissions for Combination Sum.

Memory Usage: 38.1 MB, less than 99.06% of Java online submissions for Combination Sum.

## Time spent:

21 min 40 seconds

## Times of Wrong answer:

None

# Solution 

https://leetcode.com/problems/combination-sum/

```java
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> results = new ArrayList<>();
        List<Integer> temp = new ArrayList<>();
        if (candidates == null) {
            return results;
        }
        
        Arrays.sort(candidates);
        helper(candidates, target, results, temp, 0);
        return results;
    }
    
    private void helper(int [] candidates,
                        int remainTarget,
                        List<List<Integer>> results,
                        List<Integer> temp,
                        int startIndex) {
        if (remainTarget == 0) {
            results.add(new ArrayList<Integer>(temp));
            return;
        }
        
        if (remainTarget < 0) {
            return;
        }
        
        for (int i = startIndex; i < candidates.length; i++) {
            if (i > startIndex && candidates[i] == candidates[i - 1]) {
                continue;
            }
            
            temp.add(candidates[i]);
            helper(candidates, remainTarget - candidates[i], results, temp, i);
            //Notation : Remember to remove `candidates[i]`  for next loop after adding it.
            temp.remove(temp.size() - 1);
        }
    }
}
```

```python
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        results, comb = [], []
        candidates.sort()
        self.dfs(candidates, comb, results, 0, target)
        return results
    
    def dfs(self, candidates, comb, results, start_index, remain_target):
        if remain_target == 0:
            results.append(list(comb))
            return 0
        
        if remain_target < 0:
            return 0
        
        for i in range(start_index, len(candidates)):
            comb.append(candidates[i])
            self.dfs(candidates, comb, results, i, remain_target - candidates[i])
            comb.pop()
```



# Time complexity

O(n)

# Note and tips

1. Remember to remove `candidates[i]`  for next loop after adding it.

# Python

1. list.sort(cmp=None, key=None, reverse=False)
   sorted(iterable, cmp=None, key=None, reverse=False)
   cmp -- 可选参数, 如果指定了该参数会使用该参数的方法进行排序。
   key -- 主要是用来进行比较的元素，只有一个参数，具体的函数的参数就是取自于可迭代对象中，指定可迭代对象中的一个元素来进行排序。
   reverse -- 排序规则，reverse = True 降序， reverse = False 升序（默认）

2. python list.pop() == java ArrayList.remove()

   python list.append() == java ArrayList.add()

   python list(list) = new ArrayList<T>(arraylist)



