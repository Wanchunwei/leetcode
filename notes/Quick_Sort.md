# Algorism 

Merge Sort

# Better solution 

Currently Best

# Solution 


```java
public class Solution {
    /**
     * @param A: an integer array
     * @return: nothing
     */
    public void sortIntegers(int[] A) {
        // write your code here
        if (A == null || A.length == 0) {
            return;
        }

        quickSort(A, 0, A.length - 1);
    }
    
    private void quickSort(int[] A, int start, int end) {
        //Notation 1: if start >] end directly retrun
        if (start >= end) {
            return ;
        }
        
        int pivot = A[start + (end - start) / 2];
        int left = start;
        int right = end;
        
        //Notation 2: Use left <= right, rather than left < right to avoid (left == right) and get into stack over flow error in recursion;
        while (left <= right) {
            while (eft <= right && A[left] < pivot) {
                left++;
            } 
            
            while (eft <= right && A[right] > pivot) {
                right--;
            }
            //Notaation 3: Must have a "left <= right" condition, otherwise it's possible to swap when right < left
            if (left <= right && A[left] >= pivot && A[right] <= pivot ) {
                //Notation 4: Done write function swap(int a, int b). int is a fundermental type in java, always pass value but not address to parameter. 
                int temp = A[left];
                A[left] = A[right];
                A[right] = temp;

                left++;
                right--;
            }
            
            
        }
        
        quickSort(A, start, right);
        quickSort(A, left, end);
    }
    
}
```

# Time complexity
O(nlogn)

# Note and tips
Notatiion 1, 2, 3 