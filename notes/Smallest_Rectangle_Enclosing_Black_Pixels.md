# Algorism 

Binary Search 

Analysis : 

1. If we want to caculate the area, we must find `left`, `right`, `top` and `bottom` 4 points; 
2. To find the 4 points, the first consideration is Binary Search, which is the best common way to search the target point in an array. 
3. `The difficulty is that '1' is not continuous when converting 2D to 1D array but Binary Search is based on 1D array, we can not judge when applying Binary Search.`
So, to apply Binary Search, we need to think about a way to  `deal with the 2D array into 1D and split it into 2 parts ` !!!!!
4. The solution is : Accordingt to the problem,  '1' is continuous in 2D array, then we can consider the 2D array as a 1D array that the 1D array is the '1''s projection of 2D array. 


# Better solution 

Currently Best

# Solution 

## Performans:
Runtime: 1 ms, faster than 78.47% of Java online submissions for Smallest Rectangle Enclosing Black Pixels.

Memory Usage: 39.6 MB, less than 100.00% of Java online submissions for Smallest Rectangle Enclosing Black Pixels.

## Time spent: 

1 hour 6 min 10 seconds

# Times of wrong answer:

4 -- Bug 1,2,3,4

```java
class Solution {
    public int minArea(char[][] image, int x, int y) {
        if (image == null || image.length == 0) {
            return 0;
        }
        
        if (image[0] == null || image[0].length == 0) {
            return 0;
        }
              
        int m = image.length, n = image[0].length;
        int left = 0, right = 0, top = 0, bottom = 0;
        int startTop = 0, startBot = 0, endTop = m - 1, endBot = m - 1, isBlack = 0;
        while (startTop + 1 < endTop) {
            int mid = startTop + (endTop - startTop) / 2; 
            for (int i = 0; i < n; i++) {
                //Bug 1:Don't write image[mid][i] == 1. The array is a 2D character array, not numbers; 
                if (image[mid][i] == '1') {
                    isBlack = 1;
                    break;
                }
            }
            
            if (isBlack == 1) {
                endTop = mid;
            } else if (x > mid) {
                startTop = mid;
            } else {
                endTop = mid;
            }
            
            isBlack = 0;
        }
        
        for (int i = 0; i < n; i++) {
            if (image[startTop][i] == '1') {
                    isBlack = 1;
                    break;
            }
        }
        
        if (isBlack == 1) {
            top = startTop;
        } else {
            top = endTop;
        }
        
        isBlack = 0;
        
        while (startBot + 1 < endBot) {
            int mid = startBot + (endBot - startBot) / 2;
            for (int i = 0; i < n; i++) {
                if (image[mid][i] == '1') {
                    isBlack = 1;
                    break;
                }
            }
            
            if (isBlack == 1) {
                startBot = mid; 
            } else if (x > mid) {
                startBot = mid;
            } else {
                endBot = mid;
            }
            
            isBlack = 0;
        }
        
        for (int i = 0; i < n; i++) {
                if (image[endBot][i] == '1') {
                       isBlack = 1;
                       break;
                }
        }
        
        if (isBlack == 1) {
            bottom = endBot;
        } else {
            bottom = startBot;
        }
        
        isBlack = 0;
        
        int startLeft = 0, startRight = 0, endLeft = n - 1, endRight = n - 1;
        while (startLeft + 1 < endLeft) {
            int mid = startLeft + (endLeft - startLeft) / 2;
            for (int i = 0; i < m; i++) {
                if (image[i][mid] == '1') {
                    isBlack = 1;
                    break;
                }
            }
            
            if (isBlack == 1) {
                endLeft = mid;
            //Bug2: change x to y when copying code.
            } else if (y > mid) {
                startLeft = mid;
            } else {
                endLeft = mid;
            }
            
            isBlack = 0;
        }
        
        for (int i = 0; i < m; i++) {
            if (image[i][startLeft] == '1') {
                    isBlack = 1;
                    break;
            }
        }
        
        if (isBlack == 1) {
            left = startLeft;
        } else {
            left = endLeft;
        }
        
        isBlack = 0;

        while (startRight + 1 < endRight) {
            int mid = startRight + (endRight - startRight) / 2;
            for (int i = 0; i < m; i++) {
                
                if (image[i][mid] == '1') {
                    isBlack = 1;
                    break;
                }
            }
            
            if (isBlack == 1) {
                startRight = mid;
            } else if (y > mid) {
                startRight = mid;
            } else {
                endRight = mid;
            }
            
            isBlack = 0;
        }
        
        for (int i = 0; i < m; i++) {
            if (image[i][endRight] == '1') {
                   isBlack = 1;
                   break;
            }
        }
        
        if (isBlack == 1) {
            right = endRight;
        } else {
            right = startRight;
        }
        
        //Bug 3: Remember to add 1 when caculating the area!!!!!!
        return (right - left + 1) * (bottom - top + 1);
    }
}
```

# Time complexity
O(mlogn + nlogm)

`Wrost solution:O(mn)`

# Notes and Tips
1. Write help function if the code is very long

i.e: 
```java
class Solution {
    public int minArea(char[][] image, int x, int y) {
        if (image == null || image.length == 0 || image[0].length == 0) {
            return 0;
        }
        int m = image.length;
        int n = image[0].length;
        int left = findLeft(image, 0, y);
        int right = findRight(image, y, n - 1);
        int top = findTop(image, 0, x);
        int bottom = findBottom(image, x, m - 1);
        return (right - left + 1) * (bottom - top + 1);
    }
    
    private int findLeft(char[][] image, int s, int e) {
        while (s + 1 < e) {
            int m = s + (e - s) / 2;
            if (emptyColumn(image, m)) {
                s = m;
            } else {
                e = m;
            }
        }
        if (emptyColumn(image, s)) {
            return e;
        } else {
            return s;
        }
    }
    
    private int findRight(char[][] image, int s, int e) {
        while (s + 1 < e) {
            int m = s + (e - s) / 2;
            if (emptyColumn(image, m)) {
                e = m;
            } else {
                s = m;
            }
        }
        if (emptyColumn(image, e)) {
            return s;
        } else {
            return e;
        }
    }
    
    private int findTop(char[][] image, int s, int e) {
        while (s + 1 < e) {
            int m = s + (e - s) / 2;
            if (emptyRow(image, m)) {
                s = m;
            } else {
                e = m;
            }
        }
        if (emptyRow(image, s)) {
            return e;
        } else {
            return s;
        }
    }
    
    private int findBottom(char[][] image, int s, int e) {
        while (s + 1 < e) {
            int m = s + (e - s) / 2;
            if (emptyRow(image, m)) {
                e = m;
            } else {
                s = m;
            }
        }
        if (emptyRow(image, e)) {
            return s;
        } else {
            return e;
        }
    }
    
    private boolean emptyRow(char[][] image, int r) {
        for (int c = 0; c < image[r].length; ++c) {
            if (image[r][c] == '1') {
                return false;
            }
        }
        return true;
    }
    
    private boolean emptyColumn(char[][] image, int c) {
        for (int r = 0; r < image.length; ++r) {
            if (image[r][c] == '1') {
                return false;
            }
        }
        return true;
    }
}
```
2. Take care of every step when writing copy similar code and morphing;  

# Relavent Question
- [33 Search in Rotated Sorted Array](https://github.com/Wanchunwei/leetcode/blob/master/notes/Search_in_Rotated_Sorted_Array.md)
- [153 Find Minimum in Rotated Sorted Array](https://github.com/Wanchunwei/leetcode/blob/master/notes/Find_Minimum_in_Rotated_Sorted_Array.md)
- [702. Search in a big sorted Array](https://github.com/Wanchunwei/leetcode/blob/master/notes/Search_In_a_Big_Sorted_Array.md)
- [704. Binary Search](https://github.com/Wanchunwei/leetcode/blob/master/notes/Binary_Search.md)

