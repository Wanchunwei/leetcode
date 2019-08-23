# Algorithm

Two pointers



Analysis : 

1. Use two pointers: start and end to represent a window.
2. Move end to find a valid window.
3. When a valid window is found, move start to find a smaller window.

# Better solution

Tips : 

Using a counter and an int array to store characters of the substring 

and do ```map[s_array[end]] --``` to avoid compare of t and the substring. 

```java
if(map[s_array[end]] > 0) {
	count--;
}
map[s_array[end]] --;
```

rather than an extra O(k) function to judge whether current substring is a valid substring.  



```java
public String minWindow(String s, String t) {
    char[] s_array = s.toCharArray();
    char[] t_array = t.toCharArray();
    int[] map = new int[256];
    int end = 0;
    int start = 0;
    int min_length = Integer.MAX_VALUE;
    for(int i = 0; i < t_array.length; i++) // store t character and its count ----< means the lack number
        map[t_array[i]] ++;
    int count = t_array.length;
    int min_start = 0;
    
    // for those Characters t doesn't have, map[thisCharacter] are at most 0
    while(end < s_array.length)
    {
        if(map[s_array[end]] > 0)   // t has this character
        {
            count--;
        }
        map[s_array[end]] --;
        while(count == 0)   //window matches
        {
            if((end - start + 1) < min_length)
            {
                min_length = end - start + 1;
                min_start = start;
            }
            map[s_array[start]] ++;     // start go left
            if(map[s_array[start]] > 0){    // remove a character which t has
                count ++;           //Cause for those Characters t doesn't have, map[thisCharacter] are at most 0
            }
            start++;
        }
        end ++;

    }
    if( min_start+min_length > s_array.length)
        return "";
    return s.substring(min_start, min_start+min_length);
}
```

Here we can come up with a **template to solve most substring problem** : 

```java
int findSubstring(string s){
        int[] map = new int[256];
        int counter; // check whether the substring is valid
        int begin=0, end=0; //two pointers, one point to tail and one  head
        int d; //the length of substring

        for() { /* initialize the hash map here */ }

        while(end<s.size()){

            if(map[s[end++]]-- ?){  /* modify counter here */ }

            while(/* counter condition */){ 
                 
                 /* update d here if finding minimum*/

                //increase begin to make it invalid/valid again
                
                if(map[s[begin++]]++ ?){ /*modify counter here*/ }
            }  

            /* update d here if finding maximum*/
        }
        return d;
  }
```



## Performance:

Runtime: 59 ms, faster than 6.80% of Java online submissions for Minimum Window Substring.

Memory Usage: 38.7 MB, less than 81.92% of Java online submissions for Minimum Window Substring.

## Time spent:

31 min 

## Times of Wrong answer:

1 - Bug 1

## Solution

```java
class Solution {
    public String minWindow(String s, String t) {
        if (s == null || s.length() == 0 || t.length() > s.length() || t.length() == 0) {
            return "";
        }
        
        int start = 0, end = 0;
        String min = s;
        Map<Character, Integer> map = new HashMap<>();
        for (int i = 0; i < t.length(); i++) {
            if (!map.containsKey(t.charAt(i))) {
                map.put(t.charAt(i), 1);
            } else {
                map.put(t.charAt(i), map.get(t.charAt(i)) + 1);
            }
        }
        
        Map<Character, Integer> container = new HashMap<>();
        while (start < s.length()) {
            // Bug 1 : Be careful of the corner case that we can not find a substring in String s
            if (start == 0 && end == s.length() && !isAllContain(container, map)) {
                return "";
            } 
            
            //Notation : If end is already at the end of String s, and substrin g(start, end) is not a valid answer, then we can break cause that all every substring(index, end) that index > start is not valid.  
            if (end == s.length() && !isAllContain(container, map)) {
                break;
            }
            
            if (!isAllContain(container, map)) {
                if (!container.containsKey(s.charAt(end))) {
                    container.put(s.charAt(end), 1);
                } else {
                    container.put(s.charAt(end), container.get(s.charAt(end)) + 1);
                }
                end++;
            } else {
                if (min.length() > (end - start) && start < end) {
                    min = s.substring(start, end);
                }

                if (container.containsKey(s.charAt(start))) {
                    if (container.get(s.charAt(start)) == 1) {
                        container.remove(s.charAt(start));
                    } else {
                        container.put(s.charAt(start), container.get(s.charAt(start)) - 1);
                    }
                }
                
                start++;
            }
        }
      
        return min;
    }
    
    private boolean isAllContain(Map<Character, Integer> container,
                                 Map<Character, Integer> map) {
        for (Character c : map.keySet()) {
            if (!container.containsKey(c) || container.get(c) < map.get(c)) {
                return false;
            }
        }
        return true;
    }
}
```

# Time complexity

O(nk)

# Notes and Tips

1. Be careful of the corner case that we can not find a substring in String s
2. Notation : If end is already at the end of String s, and substrin g(start, end) is not a valid answer, then we can break cause that all every substring(index, end) that index > start is not valid.  
3. **Tips : Using a counter and an int array to store characters of the substring and do ```map[s_array[end]] --``` to avoid compare of t and the substring, which is O(k) time. **