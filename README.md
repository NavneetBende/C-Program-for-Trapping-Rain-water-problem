Trapping Rain water problem in C
 

Here, in this page we will discuss the program for trapping rain water problem in C programing language. We will discuss different methods in this page.

Trapping Rain Water in C
While loop in C
Method Discussed :
Method 1 : Naive Approach
Method 2 : Efficient Approach
Let’s discuss the above two methods in brief.

Method 1 :
Iterate the entire array,
For every ith element, traverse the array from 0 to i and find the maximum height (a) and after that traverse the array from the i index to n, and find the maximum height (b).
The amount of water that will be stored in this column is min(a, b) – arr[i], add this value to the total amount of water stored.
After complete iteration print the amount of water.
Time and Space complexity :
Time-Complexity : O(n^2)
Space-Complexity : O(1)
Method 1 : Code in C
Run
#include <stdio.h>

int min(int a, int b){
    if(a<b) return a; return b; } int max(int a, int b){ if(a>b)
        return a;
        
    return b;
}

int maxWater(int arr[], int n)
{
    int res = 0;

    for (int i = 1; i < n-1; i++) {

      // Find the maximum element on its left
      int left = arr[i];
      for (int j=0; j<i; j++)
        left = max(left, arr[j]);

      // Find the maximum element on its right 
      int right = arr[i];
      for (int j=i+1; j<n; j++)
        right = max(right, arr[j]);

      // Update the maximum water 
     res = res + (min(left, right) - arr[i]); 
   }

  return res;
}

// Driver code
int main()
{
  
   int arr[] = {3, 0, 2, 0, 4};
   int n = sizeof(arr)/sizeof(arr[0]);
   
   printf("%d ", maxWater(arr, n));

   return 0;
}
Output
7
Related Pages
Given an array which consists of only 0, 1 and 2

Find the “Kth” max and min element of an array

Find the Union and Intersection of the two sorted arrays

Find Largest sum contiguous Subarray

Minimize the maximum difference between heights 

Method 2 :
Create two array say left[] and right[] of size n.
Create a variable say max_ and set its value to INT_MIN.
Run one loop from 0 to n and  in each iteration update max_ as max_ = max(max_, arr[i]) and also assign left[i] = max_.
Again, update max_ = INT_MIN.
Run another loop from n-1 to 0 and in each iteration update max_ as max_ = max(max_, arr[i]) and also assign right[i] = max_.
Now, traverse the array from 0 to n,
The amount of water that will be stored in this column is min(a,b) – array[i],(where a = left[i] and b = right[i]) add this value to total amount of water stored
After complete iteration print the amount of water.
Time and Space complexity :
Time-Complexity : O(n)
Space-Complexity : O(n)
Run
#include <stdio.h>

int min(int a, int b){
    if(a>b)
        return b;
        
    return a;
}

int max(int a, int b){
    if(a>b)
        return a;
        
    return b;
}

int maxWater(int arr[], int n)
{

    int left[n];

    int right[n];

    int water = 0;
    
    left[0] = arr[0];
    for (int i = 1; i < n; i++) 
      left[i] = max(left[i - 1], arr[i]); 
    
    right[n - 1] = arr[n - 1]; 
      
    for (int i = n - 2; i >= 0; i--)
        right[i] = max(right[i + 1], arr[i]);

    for (int i = 0; i < n; i++)
        water += min(left[i], right[i]) - arr[i];

    return water;
}

// Driver code
int main()
{
   int arr[] = {3, 0, 2, 0, 4};
   int n = sizeof(arr)/sizeof(arr[0]);
   
   printf("%d ", maxWater(arr, n));

   return 0;
    
}
Output
7
