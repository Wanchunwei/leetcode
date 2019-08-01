# Algorithm 

BFS

# Better solution

Divide conquer (Just remember as a template)

```java
public class Codec {
    public String serialize(TreeNode root) {
        if (root == null) return "#";
        return root.val + "," + serialize(root.left) + "," + serialize(root.right);
    }

    public TreeNode deserialize(String data) {
        Queue<String> queue = new LinkedList<>(Arrays.asList(data.split(",")));
        return helper(queue);
    }
    
    private TreeNode helper(Queue<String> queue) {
        String s = queue.poll();
        if (s.equals("#")) return null;
        TreeNode root = new TreeNode(Integer.valueOf(s));
        root.left = helper(queue);
        root.right = helper(queue);
        return root;
    }
}
```



## Performance:


Total runtime 1849 ms

Your submission beats 9.80% Submissions!

## Time spent:

Not Done

## Times of Wrong answer:

2

# Solution 

```java
/**
 * Definition of TreeNode:
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left, right;
 *     public TreeNode(int val) {
 *         this.val = val;
 *         this.left = this.right = null;
 *     }
 * }
 */


public class Solution {
    /**
     * This method will be invoked first, you should design your own algorithm 
     * to serialize a binary tree which denote by a root node to a string which
     * can be easily deserialized by your own "deserialize" method later.
     */
    public String serialize(TreeNode root) {
        // write your code here
        ArrayList<String> serialize = new ArrayList<>();
        if (root == null) {
            return serialize.toString();
        }
        String res = "";
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        while (!queue.isEmpty()) {
            int size = queue.size(), count = 0;
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                if (node == null) {
                    //serialize.add("null");
                    res = res + "null" + ",";
                    queue.offer(null);
                    queue.offer(null);
                    count = count + 2;
                } else {
                    //serialize.add(node.val + "");
                    res = res + "" + node.val + ",";
                    queue.offer(node.left);
                    if (node.left == null) {
                        count++;
                    }
                    queue.offer(node.right);
                    if (node.right == null) {
                        count++;                        
                    }
                }
            }
            
            if (count == queue.size()) {
                break;
            }
        }
            
        return res;
    }

    /**
     * This method will be invoked second, the argument data is what exactly
     * you serialized at method "serialize", that means the data is not given by
     * system, it's given by your own serialize method. So the format of data is
     * designed by yourself, and deserialize it here as you serialize it in 
     * "serialize" method.
     */
    public TreeNode deserialize(String data) {
        // write your code here
        String replace = data.replace("[","");
        String replace1 = replace.replace("]","");
        if (replace1.equals("")) {
            return null;
        }
        
        List<String> deserialize = new ArrayList<String>(Arrays.asList(replace1.split(",")));
        List<Integer> arr = new ArrayList<>();
        
        for(String str:deserialize){
            if (str.trim().equals("null")) {
                arr.add(null);
            } else {
                arr.add(Integer.parseInt(str.trim()));   
            }

        }
        
        return helper(arr, 0);
    }
    
    private TreeNode helper(List<Integer> arr, int index) {
        if (index >= arr.size()) {
            return null;
        }
        
        if (arr.get(index) == null) {
            return null;
        }
        
        
        TreeNode root = new TreeNode(arr.get(index));
        root.left = helper(arr, 2*index + 1);
        root.right = helper(arr, 2*index + 2);
             
        return root;
       
    }
}
```

# Time complexity

O(n)

# Note and tips

1. `String.replace(String a, String b)` method replaces all string b with string a in `String`.

2. `Arrays.asList()` takes an array, which can only be generic type, not fundamental type like int[], as the parameter, return a List<T> (not ArrayList). 

   The return List can not `add` or `remove()`.  So we need to create a new List : `List<String> deserialize = new ArrayList<String>(Arrays.asList(replace1.split(",")));`

   Notation : To convert an fundamental type array into List, we can use `Arrays.asList(ArrayUtils.toObject(intArray));`

3. Better to do `trim()` if we want to compare two String. 