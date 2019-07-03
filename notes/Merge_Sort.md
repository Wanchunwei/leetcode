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

        int[] temp = new int[A.length];
        mergeSort(A, 0, A.length - 1, temp);
        
    }
    
    private void mergeSort(int[] A, int start, int end, int[] temp) {
        if (start >= end) {
            return;
        }
        
        int mid = start + (end - start) / 2;
        
        mergeSort(A, start, mid, temp);
        //Notation 1: Should be mid + 1, otherwise stackoverflow. 
        mergeSort(A, mid + 1, end, temp);
        merge(A, start, mid, end, temp);
        
    }
    
    private void merge(int[] A, int start, int mid, int end, int[] temp)  {
        int index = start;
        //Notation 2: Add variable type(int) before initiating a variable. 
        int leftStart = start;
        int rightStart = mid + 1;
        while (leftStart <= mid && rightStart <= end) {
            if (A[leftStart] <= A[rightStart]) {
                temp[index++] = A[leftStart++];
            } else {
                temp[index++] = A[rightStart++];
            }
        }
        //Notation 3: User ++, write clearer code. 
        while (leftStart <= mid) {
            temp[index++] = A[leftStart++];
        }
        
        while (rightStart <= end) {
            temp[index++] =  A[rightStart++];
        }
        
        for (int i = start; i <= end; i++) {
            A[i] = temp[i];
        }
    }
}
```

# Time complexity
O(nlogn)

# Note and tips
Notatiion 1, 2, 3 