# Leetcode

## Sequence 

**General Method :**

​	Two pointers (sliding window):

- Two onward pointers  (sliding window) 
- One onward pointer + One  backward pointer

**General Implementation Steps:**

1. Use two pointers: start and end to represent a window.
2. Move end to find a valid window.
3. When a valid window is found, move start to find a smaller window.

Template :

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



**Key Concepts** : 

Similar to binary search. Try to find a condition that can make pointers keep moving to one direction until they **meet in the middle (onward + backward)** or **meet at the end of the given array (sliding window)** 

**Notation** : Try not to use while loop because it is easy to write bugs. 

**Application** :  

1. Find all results that satisfy some conditions in a given array
2. Do particular permutation to a given array. 

**Extension** : 3 pointers (Keep one pointer and do two pointer to the rest of the given array)

**Common corner cases **: 

1. end = s.length()

- [Medium - 15 3Sum](https://github.com/Wanchunwei/leetcode/blob/master/notes/3Sum.md)
- [Medium - 16 3Sum closest](https://github.com/Wanchunwei/leetcode/blob/master/notes/3Sum%20closest.md)
- [Medium - 75 Sort Colors](https://github.com/Wanchunwei/leetcode/blob/master/notes/Sort%20Colors.md)
- [Hard - 76 Minimum Window Substring](https://github.com/Wanchunwei/leetcode/blob/master/notes/Minimum%20Window%20Substring.md)
- [Easy - 121 Best Time to Buy and Sell Stock](https://github.com/Wanchunwei/leetcode/blob/master/notes/Best%20Time%20to%20Buy%20and%20Sell%20Stock.md
  )
- [Medium - 424 Longest Repeating Character Replacement](https://github.com/Wanchunwei/leetcode/blob/master/notes/Longest%20Repeating%20Character%20Replacement.md)
- [Medium - 763 Partition Labels (Sweep - Line + Two pointers)](https://github.com/Wanchunwei/leetcode/blob/master/notes/Partition%20Labels.md)
- [Medium - 1100 Find K-Length Substrings With No Repeated Characters](https://github.com/Wanchunwei/leetcode/blob/master/notes/Find%20K-Length%20Substrings%20With%20No%20Repeated%20Characters.md)
- [Lintcode Medium - 143 Sort Colors (rainbow sort)](https://github.com/Wanchunwei/leetcode/blob/master/notes/Sort%20Color%20II.md)

## Subsets
- [Easy - 28 Implement_strStr()](https://github.com/Wanchunwei/leetcode/blob/master/notes/Implement_strStr().md)
- [Medium - 78 Subsets](https://github.com/Wanchunwei/leetcode/blob/master/notes/Subsets.md)
- [Medium - 90 Subsets II](https://github.com/Wanchunwei/leetcode/blob/master/notes/Subsets_II.md)

## Sort
- [Easy - lintcode 463. Merge Sort](https://github.com/Wanchunwei/leetcode/blob/master/notes/Merge_Sort.md)
- [Easy - lintcode 463. Quick Sort](https://github.com/Wanchunwei/leetcode/blob/master/notes/Quick_Sort.md)

## Binary Search
- [Medium - 33 Search in Rotated Sorted Array](https://github.com/Wanchunwei/leetcode/blob/master/notes/Search_in_Rotated_Sorted_Array.md)
- [Medium - 34 Find First and Last Position of Element in Sorted Array](https://github.com/Wanchunwei/leetcode/blob/master/notes/Find_First_and_Last_Position_Of_Element.md)
- [Medium - 74 Search a 2D Matrix](https://github.com/Wanchunwei/leetcode/blob/master/notes/Search_a_2D_Matrix.md)
- [Medium - 81 Search in Rotated Sorted Array_II](https://github.com/Wanchunwei/leetcode/blob/master/notes/Search_in_Rotated_Sorted_Array_II.md)
- [Medium - 153 Find Minimum in Rotated Sorted Array](https://github.com/Wanchunwei/leetcode/blob/master/notes/Find_Minimum_in_Rotated_Sorted_Array.md)
- [Easy - 278 First Bad Version](https://github.com/Wanchunwei/leetcode/blob/master/notes/First_Bad_Version.md)
- [Hard - 302 Smallest Rectangle Enclosing Black Pixels](https://github.com/Wanchunwei/leetcode/blob/master/notes/Smallest_Rectangle_Enclosing_Black_Pixels.md)
- [Hard - 410 Split Array Largest Sum](https://github.com/Wanchunwei/leetcode/blob/master/notes/Split_Array_Largest_Sum.md)
- [Hard - 644 Maximum_Average_Subarray_II](https://github.com/Wanchunwei/leetcode/blob/master/notes/Maximum_Average_Subarray_II.md)
- [Medium - 658 Find K Closest Elements](https://github.com/Wanchunwei/leetcode/blob/master/notes/Find_K_Closest_Elements.md)
- [Medium - 702 Search in a big sorted Array](https://github.com/Wanchunwei/leetcode/blob/master/notes/Search_In_a_Big_Sorted_Array.md)
- [Easy - 704 Binary Search](https://github.com/Wanchunwei/leetcode/blob/master/notes/Binary_Search.md)
- [Easy - 852 Peak Index in a Mountain Array](https://github.com/Wanchunwei/leetcode/blob/master/notes/Peak_Index_in_a_Mountain_Array.md)
- [Hard -  Lintcode183 Wood Cut](https://github.com/Wanchunwei/leetcode/blob/master/notes/Wood_Cut.md)
- [Hard - Lintcode 437. Copy Books ](https://github.com/Wanchunwei/leetcode/blob/master/notes/Copy_Books.md)

## BFS 
**Application :**

1. Shortest path problem (especially for the case that each step counts 1, i.e. Matrix)
2. Topological sorting 
3. Go through a graph
4. Matrix problem

**General Implementation Step:**

1. Traverse and collect all the start nodes and push them in a queue. 
2. Construct corresponding graph with given edges.
3. while the queue becomes empty (Add extra Set if needed):
   * Poll one node from the queue each time and find its neighbors.
   * (if Set does not contains neighbors)Push the neighbors (in some conditions) into the queue.
4. Return.  



- [Medium - 102 Binary Tree Level Order Traversal](https://github.com/Wanchunwei/leetcode/blob/master/notes/Binary_Tree_Level_Order_Traversal.md)
- [Medium - 103 Binary Tree Zigzag Level Order Traversal](https://github.com/Wanchunwei/leetcode/blob/master/notes/Binary_Tree_Zigzag_Level_Order_Traversal.md)
- [Medium - 133 Clone Graph](https://github.com/Wanchunwei/leetcode/blob/master/notes/Clone_Graph.md)
- [Medium - 200 Number of Islands](https://github.com/Wanchunwei/leetcode/blob/master/notes/Numbers_Of_Islands.md)
- [Medium - 207 Course Schedule](https://github.com/Wanchunwei/leetcode/blob/master/notes/Course_Schedule.md)
- [Medium - 210 Course Schedule II](https://github.com/Wanchunwei/leetcode/blob/master/notes/Course_Schedule_II.md)
- [Medium - 216 Graph Valid Tree](https://github.com/Wanchunwei/leetcode/blob/master/notes/Graph_Valid_Tree.md)
- [Hard - 297 Serialize and Deserialize Binary Tree](https://github.com/Wanchunwei/leetcode/blob/master/notes/Serialize%20and%20Deserialize%20Binary%20Tree.md)
- [Medium - 323 Number of Connected Components in an Undirected Graph](https://github.com/Wanchunwei/leetcode/blob/master/notes/Number%20of%20Connected%20Components%20in%20an%20Undirected%20Graph.md)
- [Medium - 444 Sequence Reconstruction](https://github.com/Wanchunwei/leetcode/blob/master/notes/Sequence_Reconstruction.md)
- [Medium - 529 Minesweeper](https://github.com/Wanchunwei/leetcode/blob/master/notes/Minesweeper.md)
- [Medium - 909 Snakes and Ladders](https://github.com/Wanchunwei/leetcode/blob/master/notes/Snakes_and_Ladders.md)
- [Medium - 1091 Shortest Path In Binary Matrix](https://github.com/Wanchunwei/leetcode/blob/master/notes/Shortest_Path_In_Binary_Matrix.md)
- [Medium - lintcode 127 Topological Sorting](https://github.com/Wanchunwei/leetcode/blob/master/notes/Topological_Sort.md)

## Binary Tree and Divide Conquer

**General Implementation step:**

1. Set a global value if we need to find the max(min) value in Binary Tree.

2. Set divide conquer rule : 

   - What should we calculate for each node?
   - To achieve this, what value should we get from the return value of `root.left` and `root.right`?
   - How many possible cases `root.left` and `root.right` have  (i.e. : common cases illustrated below)
   - What is the corresponding value for those cases? How to deal with those cases to write clearest code for if..else.. condition.

3. Dealing with return statement like `root == null`

4. Return result in main function


**Common corner case:**

1. 4 cases when merging :  root , root with left, root with right, root with left and right. 

2. root == null (especially, take extra care of the original root is null)

3. leaf node can only be `root.left == null && root.right == null`

- [Medium - 98 Validate Binary Search Tree](https://github.com/Wanchunwei/leetcode/blob/master/notes/Validate%20Binary%20Search%20Tree.md)
- [Easy - 110 Balanced Binary Tree](https://github.com/Wanchunwei/leetcode/blob/master/notes/Balanced%20Binary%20Tree.md)
- [Easy - 111 Minimum Depth of Binary Tree](https://github.com/Wanchunwei/leetcode/blob/master/notes/Minimum%20Depth%20of%20Binary%20Tree.md)
- [Easy - 112 Path Sum](https://github.com/Wanchunwei/leetcode/blob/master/notes/Path%20Sum.md)
- [Medium - 114 Flatten Binary Tree to Linked List](https://github.com/Wanchunwei/leetcode/blob/master/notes/Flatten%20Binary%20Tree%20to%20Linked%20List.md)
- [Hard - 124 Binary Tree Maximum Path Sum](https://github.com/Wanchunwei/leetcode/blob/master/notes/Binary%20Tree%20Maximum%20Path%20Sum.md)
- [Medium - 94 Binary Tree Inorder Traversal(iterative)](https://github.com/Wanchunwei/leetcode/blob/master/notes/Binary%20Tree%20Inorder%20Traversal.md) --- (Template need to remember)
- [Medium - 144 Binary Tree Preorder Traversal(iterative)](https://github.com/Wanchunwei/leetcode/blob/master/notes/Binary%20Tree%20Preorder%20Traversal.md) --- (Template need to remember)
- [Hard - 145 Binary Tree Postorder Traversal(iterative)](https://github.com/Wanchunwei/leetcode/blob/master/notes/Binary%20Tree%20Postorder%20Traversal.md) --- (Template need to remember)
- [Medium - 230 Kth Smallest Element in a BST](https://github.com/Wanchunwei/leetcode/blob/master/notes/Kth%20Smallest%20Element%20in%20a%20BST.md)
- [Medium - 236 Lowest Common Ancestor of a Binary Tree](https://github.com/Wanchunwei/leetcode/blob/master/notes/Lowest%20Common%20Ancestor%20of%20a%20Binary%20Tree.md)
- [Medium - 285 Inorder Successor in BST](https://github.com/Wanchunwei/leetcode/blob/master/notes/Inorder%20Successor%20in%20BST.md)
- [Hard - 297 Serialize and Deserialize Binary Tree](https://github.com/Wanchunwei/leetcode/blob/master/notes/Serialize%20and%20Deserialize%20Binary%20Tree.md)
- [Medium - 298 Binary Tree Longest Consecutive Sequence](https://github.com/Wanchunwei/leetcode/blob/master/notes/Binary%20Tree%20Longest%20Consecutive%20Sequence.md)
- [Medium - 426 Convert Binary Search Tree to Sorted Doubly Linked List](https://github.com/Wanchunwei/leetcode/blob/master/notes/Convert%20Binary%20Search%20Tree%20to%20Sorted%20Doubly%20Linked%20List.md)
- [Easy - 437 Path Sum III](https://github.com/Wanchunwei/leetcode/blob/master/notes/Path%20Sum%20III.md)
- [Medium - 549 BInary Tree Longest Consecutive Sequence II](https://github.com/Wanchunwei/leetcode/blob/master/notes/Binary%20Tree%20Longest%20Consecutive%20Sequence%20II.md)
- [Easy - 559 Maximum Depth of N-ary Tree](https://github.com/Wanchunwei/leetcode/blob/master/notes/Maximum%20Depth%20of%20N-ary%20Tree.md)
- [Medium - 666 Path Sum IV](https://github.com/Wanchunwei/leetcode/blob/master/notes/Path%20Sum%20IV.md)
- [Medium - 1120 Maximum Average Subtree](https://github.com/Wanchunwei/leetcode/blob/master/notes/Maximum%20Average%20Subtree.md)
- [Easy - lintcode 376 Binary Tree Path Sum](https://github.com/Wanchunwei/leetcode/blob/master/notes/Binary%20Tree%20Path%20Sum.md)
- [Easy - lintcode 480 Binary Tree Paths](https://github.com/Wanchunwei/leetcode/blob/master/notes/Binary%20Tree%20Paths.md)
- [Easy - lintcode 596 Minimum Subtree](https://github.com/Wanchunwei/leetcode/blob/master/notes/Minimum%20Subtree.md) 



## DFS

- [Medium - 39 Combination Sum](https://github.com/Wanchunwei/leetcode/blob/master/notes/Combination%20Sum.md)
- [Medium - 40 Combination Sum II](https://github.com/Wanchunwei/leetcode/blob/master/notes/Combination%20Sum%20II.md)
- [Medium - 46 Permutations](https://github.com/Wanchunwei/leetcode/blob/master/notes/Permutations.md)
- [Medium - 47 Permutations II](https://github.com/Wanchunwei/leetcode/blob/master/notes/Permutations%20II.md)
- [Hard - 126 Word Ladder II](https://github.com/Wanchunwei/leetcode/blob/master/notes/Word%20Ladder%20II.md)
- [Medium - 130 Surrounded Regions](https://github.com/Wanchunwei/leetcode/blob/master/notes/Surrounded%20Regions.md)
- [Medium - 131 Palindrome Partitioning](https://github.com/Wanchunwei/leetcode/blob/master/notes/Palindrome%20Partitioning.md)
- [Medium - 216 Combination Sum III](https://github.com/Wanchunwei/leetcode/blob/master/notes/Combination%20Sum%20III.md)
- [Hard - 301 Remove Invalid Parentheses](https://github.com/Wanchunwei/leetcode/blob/master/notes/Remove%20Invalid%20Parentheses.md)
- [Medium - 332 Reconstruct Itinerary](https://github.com/Wanchunwei/leetcode/blob/master/notes/Reconstruct%20Itinerary.md)
- [Hard - 488 Zuma Game](https://github.com/Wanchunwei/leetcode/blob/master/notes/Zuma%20Game.md)
- [Medium - 490 The Maze](https://github.com/Wanchunwei/leetcode/blob/master/notes/The%20Maze.md)



## Dynamic Programming

- [Easy - 53 Maximum Subarray](https://github.com/Wanchunwei/leetcode/blob/master/notes/Maximum%20Subarray.md)
- [Medium - 152 Maximum Product Subarray](https://github.com/Wanchunwei/leetcode/blob/master/notes/Maximum%20Product%20Subarray.md)
