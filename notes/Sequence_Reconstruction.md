# Algorithm

BFS (Topological sorting)

# Better solution 

Currently Best

## Performance:

Runtime: 28 ms, faster than 89.80% of Java online submissions for Sequence Reconstruction.

Memory Usage: 42.7 MB, less than 96.20% of Java online submissions for Sequence Reconstruction.

## Time spent:

Not Done

## Times of Wrong answer:

Many

## Solution

```java
class Solution {
    public boolean sequenceReconstruction(int[] org, List<List<Integer>> seqs) {
        if (seqs == null || seqs.size() == 0) {
            return false;
        } 
        
        int number = 0, cnt = 0;
        Queue<Integer> queue = new LinkedList<>();
        Set<Integer> set = new HashSet<>();
        
        //Notation : For each array operation, carefully take attention to                                    indexOutofBound protect graph[i] = new ArrayList<Integer>();
        int[] indegree = new int[org.length + 1];
        ArrayList<Integer>[] graph = new ArrayList[org.length + 1];
        
        for (int i = 1; i <= org.length; i++) {//
            graph[i] = new ArrayList<Integer>();
        }
        
        for (List<Integer> seq : seqs) {
            cnt += seq.size();
            //Notation : For each array operation, carefully take attention to                                    indexOutofBound, protect indegree[seq.get(i)], incase that                                seq.get(i) < 0
            if (seq.size() > org.length) {
                return false;
            }
            
            for (int i = 0; i < seq.size(); i++) {
                //Notation : For each array operation, carefully take attention to                                    indexOutofBound, protect graph[seq.get(i)]
                if (seq.get(i) > org.length) {
                    return false;
                }
                if (i + 1 < seq.size()) {
                    graph[seq.get(i)].add(seq.get(i + 1));
                }
                if (i > 0) {
                    indegree[seq.get(i)]++;
                }
            }    
        }
        
        //Dealing with corner case that [] is a sequence of [];
        if (cnt < org.length) {
            return false;
        }
        
        for (int i = 1; i <= org.length; i++) {
            if (indegree[i] == 0) {
                queue.offer(i);
                set.add(i);
            }
        }
        
        if (queue.size() != 1) {
            return false;
        }
        
        while (!queue.isEmpty()) {            
            if (queue.size() != 1) {
                return false;
            }
            
            int node = queue.poll();
            if (node != org[number]) {
                return false;
            }
            
            for (Integer seq: graph[node]) {
                indegree[seq]--;
                if (indegree[seq] == 0) {
                    queue.offer(seq);
                    set.add(seq);
                }
            }
            
            number++;
        }
        
        if (set.size() != org.length) {
            return false;
        }
        
        return true;
    }
}
```



# Time complexity

O(N + E)

# Notes and Tips

1. For each array operation, carefully take attention to indexOutofBound, make sure that the `index > 0 && index < array.length`