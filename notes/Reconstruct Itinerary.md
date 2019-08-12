# Algorithm

DFS

# Better solution

```java
public List<String> findItinerary(String[][] tickets) {
    for (String[] ticket : tickets)
        targets.computeIfAbsent(ticket[0], k -> new PriorityQueue()).add(ticket[1]);
    visit("JFK");
    return route;
}

Map<String, PriorityQueue<String>> targets = new HashMap<>();
List<String> route = new LinkedList();

void visit(String airport) {
    while(targets.containsKey(airport) && !targets.get(airport).isEmpty())
        visit(targets.get(airport).poll());
    route.add(0, airport);
}
```



## Performance:

Runtime: 9 ms, faster than 35.64% of Java online submissions for Reconstruct Itinerary.

Memory Usage: 41.8 MB, less than 74.63% of Java online submissions for Reconstruct Itinerary.

## Times of Wrong answer:

Bug 1

## Solution

```java
class Solution {
    Boolean isReturned = false;
    List<String> re = new ArrayList<>();
    public List<String> findItinerary(List<List<String>> tickets) {
        List<String> results = new ArrayList<>();
        Map<String, List<String>> map = new HashMap<>();
        for (List<String> list : tickets) {
            if (!map.containsKey(list.get(0))) {
                map.put(list.get(0), new ArrayList<String>());
            }
            
            map.get(list.get(0)).add(list.get(1));
        }
        
        for (String str : map.keySet()) {
            Collections.sort(map.get(str));
        }
        
        results.add("JFK");
        helper(results, tickets.size(), map, "JFK");
        return re;
    }
    
    private void helper(List<String> results, 
                        int nums, 
                        Map<String, List<String>> map,
                        String position) {
        
        if (nums == 0 && !isReturned) {
            for (String s : results) {
                re.add(s);
            }
            isReturned = true;
            return;
        }
    
        if (!map.containsKey(position) || isReturned) {
            return;
        }
        
        //Bug 1 : Here we can not directly write "for (String str : map.get(position))" due to "ConcurrentModificationException" when doing "remove" operation. Detailed Reason:https://blog.csdn.net/qq_35056292/article/details/79751233
        List<String> list = map.get(position);
        for (int i = 0; i < list.size(); i++) {
            String neighbor = list.get(i);
            results.add(neighbor);
            list.remove(i);
            helper(results, nums - 1, map, neighbor);
            list.add(i, neighbor);
            results.remove(results.size() - 1);
        }
    }
}
```

# Time complexity

O(n)

# Notes and Tips

1. Bug 1 : We can not directly write `for (String str : map.get(position))` due to `ConcurrentModificationException` when doing `remove` operation in `ArrayList, LinkedList, HashMap...`. Detailed Reason:https://blog.csdn.net/qq_35056292/article/details/79751233