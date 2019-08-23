# Algorithm

Two pointers

# Better solution

Currently Best 

More concise solution : 

```java
class Solution {
    public int shortestWay(String source, String target) {
        int t = 0;
        int ans = 0;
        while (t < target.length()) {
            int pt = t;
            
            for (int s = 0; s < source.length(); s++) {
                if (t < target.length() && source.charAt(s) == target.charAt(t)) {
                    t++;
                }
            }
            
            if (t == pt) {
                return -1;
            }
            ans++;
        }
        
        return ans;
    }
}
```



## Performance:

Runtime: 2 ms, faster than 84.20% of Java online submissions for Shortest Way to Form String.

Memory Usage: 34.2 MB, less than 100.00% of Java online submissions for Shortest Way to Form String.

## Time spent:

30 min

## Times of Wrong answer:

None

## Solution

```java
class Solution {
    public int shortestWay(String source, String target) {
        int start = 0, end = 0, count = 0, position = -1;
        while (end < target.length()) {
            if (position < source.length() - 1 && 
                find(position + 1, source, target.charAt(end)) >= 0) {
                position = find(position + 1, source, target.charAt(end));
                end++;
            } else {
                if (find(0, source, target.charAt(end)) < 0) {
                    return -1;
                }
                count++;
                position = -1;
                start = end;
            }
            
            if (end == target.length()) {
                count++;
                break;
            }
        }
        
        return count;
    }
    
    private int find(int start, String source, char c) {
        for (int i = start; i < source.length(); i++) {
            if (source.charAt(i) == c) {
                return i;
            }
        }
        return -1;
    }
}
```



# Time complexity

O(nk)

# Notes and Tips

# Follow Up

1. The time complexity is better than O (MN), should be O(logM * N) 

```java
public int shortestWay(String source, String target) {
	char[] cs = source.toCharArray(), ts = target.toCharArray();
	int res = 1;
	List<Integer>[] idx = new List[26];
	for (int i = 0; i < 26; i++) idx[i] = new ArrayList<>();
	for (int i = 0; i < cs.length; i++) idx[cs[i] - 'a'].add(i);
	int j = 0;
	for (int i = 0; i < ts.length; ) {
		List<Integer> tar = idx[ts[i] - 'a'];
		if (tar.isEmpty()) return -1;
		int k = Collections.binarySearch(tar,j);
		if (k < 0) k = -k - 1;
		if (k == tar.size()) {
			res++;
			j = 0;
		} else {
			j = tar.get(k) + 1;
			i++;
		}

	}
	return res;
}
```

2. Could you improve it to O(n)

```java
public int shortestWay(String source, String target) {
	char[] cs = source.toCharArray(), ts = target.toCharArray();
	int[][] idx = new int[26][cs.length];
	for (int i = 0; i < cs.length; i++) idx[cs[i] - 'a'][i] = i + 1;
	for (int i = 0; i < 26; i++) {
		for (int j = cs.length - 1, pre = 0; j >= 0; j--) {
			if (idx[i][j] == 0) idx[i][j] = pre;
			else pre = idx[i][j];
		}
	}
	int res = 1, j = 0;
	for (int i = 0; i < ts.length; i++) {
		if (j == cs.length) {
			j = 0;
			res++;
		}
		if (idx[ts[i] - 'a'][0] == 0) return -1;
		j = idx[ts[i] - 'a'][j];
		if (j == 0 ) {
			res++;
			i--;
		}
	}
	return  res;
}
```

3.  if we assume which can copy a array to another array with 26 length in constant time. could u implement it with O(M + N)

   ```java
   public int shortestWay(String source, String target) {
   	char[] cs = source.toCharArray(), ts = target.toCharArray();
   	int[][] idx = new int[cs.length][26];
   	idx[cs.length - 1][cs[cs.length - 1] - 'a'] = cs.length; 
   	for (int i = cs.length - 2; i >= 0; i--) {
   		idx[i] = Arrays.copyOf(idx[i + 1],26);
   		idx[i][cs[i] - 'a'] = i + 1; 
   	}
   	int j = 0, res = 1;
   	for (int i = 0; i < ts.length; i++) {
   		if (j == cs.length) {
   			j = 0;
   			res++;
   		}
   		j = idx[j][ts[i] - 'a'];
   		if (idx[0][ts[i] - 'a'] == 0) return -1;
   		if (j == 0) {
   			res++;
   			i--;
   		}
   	}
   	return res;
   }
   ```

   

   