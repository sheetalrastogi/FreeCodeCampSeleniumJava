
#1. Finds the repeating and missing numbers in an array containing numbers from 1 to n
==========================================================================================

public class FindRepeatingAndMissing {
    /**
     * Finds the repeating and missing numbers in an array containing numbers from 1 to n,
     * where one number is missing and one number is repeated.
     * Returns an int array: [repeating, missing]
     */
    public static int[] findRepeatingAndMissing(int[] nums) {
        int n = nums.length;
        int repeating = -1, missing = -1;

        // Use an array to count occurrences
        int[] count = new int[n + 1];
        for (int num : nums) {
            count[num]++;
        }
        for (int i = 1; i <= n; i++) {
            if (count[i] == 0) {
                missing = i;
            } else if (count[i] > 1) {
                repeating = i;
            }
        }
        return new int[]{repeating, missing};
    }

    public static void main(String[] args) {
        int[] nums = {4, 3, 6, 2, 1, 1};
        int[] result = findRepeatingAndMissing(nums);
        System.out.println("Repeating: " + result[0]);
        System.out.println("Missing: " + result[1]);
        // Output: Repeating: 1, Missing: 5
    }
}

#2. Finds reverse pairs in an Array
=====================================

import java.util.*;

public class ReversePairs {
    public static List<List<String>> findReversePairs(String[] arr) {
        Set<String> set = new HashSet<>(Arrays.asList(arr));
        List<List<String>> result = new ArrayList<>();
        Set<String> visited = new HashSet<>();

        for (String s : arr) {
            String reversed = new StringBuilder(s).reverse().toString();
            // Avoid duplicate pairs
            if (set.contains(reversed) && !visited.contains(s) && !visited.contains(reversed) && !s.equals(reversed)) {
                result.add(Arrays.asList(s, reversed));
                visited.add(s);
                visited.add(reversed);
            }
        }
        return result;
    }

    public static void main(String[] args) {
        String[] arr = {"abc", "cba", "xyz", "zyx", "pqr", "lmn"};
        List<List<String>> pairs = findReversePairs(arr);
        for (List<String> pair : pairs) {
            System.out.println(pair.get(0) + " <--> " + pair.get(1));
        }
        // Output:
        // abc <--> cba
        // xyz <--> zyx
    }
}

#3. Merge sort in java arrays:
================================
public class MergeSort {
    // Main method to test merge sort
    public static void main(String[] args) {
        int[] arr = {38, 27, 43, 3, 9, 82, 10};
        mergeSort(arr, 0, arr.length - 1);
        System.out.print("Sorted array: ");
        for (int num : arr) {
            System.out.print(num + " ");
        }
    }

    // Merge Sort function
    public static void mergeSort(int[] arr, int left, int right) {
        if (left < right) {
            int mid = left + (right - left) / 2;
            // Sort first and second halves
            mergeSort(arr, left, mid);
            mergeSort(arr, mid + 1, right);
            // Merge the sorted halves
            merge(arr, left, mid, right);
        }
    }

    // Merge two sorted subarrays arr[left..mid] and arr[mid+1..right]
    public static void merge(int[] arr, int left, int mid, int right) {
        // Sizes of two subarrays to be merged
        int n1 = mid - left + 1;
        int n2 = right - mid;

        // Create temporary arrays
        int[] L = new int[n1];
        int[] R = new int[n2];

        // Copy data to temp arrays
        System.arraycopy(arr, left, L, 0, n1);
        System.arraycopy(arr, mid + 1, R, 0, n2);

        // Initial indexes of first and second subarrays
        int i = 0, j = 0;
        // Initial index of merged subarray
        int k = left;

        while (i < n1 && j < n2) {
            if (L[i] <= R[j]) {
                arr[k++] = L[i++];
            } else {
                arr[k++] = R[j++];
            }
        }

        // Copy remaining elements of L[], if any
        while (i < n1) {
            arr[k++] = L[i++];
        }

        // Copy remaining elements of R[], if any
        while (j < n2) {
            arr[k++] = R[j++];
        }
    }
}


#4. maximum product of a contiguous subarray
==============================================

public class MaximumProductSubarray {
    /**
     * Returns the maximum product of a contiguous subarray.
     */
    public static int maxProduct(int[] nums) {
        if (nums == null || nums.length == 0) return 0;

        int maxSoFar = nums[0];
        int maxEndingHere = nums[0];
        int minEndingHere = nums[0];

        for (int i = 1; i < nums.length; i++) {
            int temp = maxEndingHere;
            maxEndingHere = Math.max(Math.max(nums[i], maxEndingHere * nums[i]), minEndingHere * nums[i]);
            minEndingHere = Math.min(Math.min(nums[i], temp * nums[i]), minEndingHere * nums[i]);
            maxSoFar = Math.max(maxSoFar, maxEndingHere);
        }
        return maxSoFar;
    }

    public static void main(String[] args) {
        int[] nums = {2, 3, -2, 4};
        System.out.println("Maximum product subarray: " + maxProduct(nums)); // Output: 6

        int[] nums2 = {-2, 0, -1};
        System.out.println("Maximum product subarray: " + maxProduct(nums2)); // Output: 0
    }
}



#5. Finds the repeating and missing numbers in an array 
==========================================================

public class FindRepeatingAndMissing {
    /**
     * Finds the repeating and missing numbers in an array containing numbers from 1 to n,
     * where one number is missing and one number repeats.
     * Returns an int array: [repeating, missing]
     */
    public static int[] findRepeatingAndMissing(int[] nums) {
        int n = nums.length;
        int repeating = -1, missing = -1;

        int[] count = new int[n + 1]; // 1-based indexing

        // Count occurrences
        for (int num : nums) {
            count[num]++;
        }

        // Find repeating and missing
        for (int i = 1; i <= n; i++) {
            if (count[i] == 0) missing = i;
            if (count[i] > 1) repeating = i;
        }

        return new int[]{repeating, missing};
    }

    public static void main(String[] args) {
        int[] nums = {4, 3, 6, 2, 1, 1};
        int[] result = findRepeatingAndMissing(nums);
        System.out.println("Repeating: " + result[0]);
        System.out.println("Missing: " + result[1]);
        // Output: Repeating: 1, Missing: 5
    }
}


#6. 3-Sum Problem
======================
class GfG {
  
    static boolean hasTripletSum(int[] arr, int target) {
        int n = arr.length;
        
        // Fix the first element as arr[i]
        for (int i = 0; i < n - 2; i++) {
            
            // Fix the second element as arr[j]
            for (int j = i + 1; j < n - 1; j++) {
                
                // Now look for the third number
                for (int k = j + 1; k < n; k++) {
                    if (arr[i] + arr[j] + arr[k] == target)
                        return true; // If a triplet is found
                }
            }
        }

        return false;
    }

    public static void main(String[] args) {
        int[] arr = { 1, 4, 45, 6, 10, 8 };
        int target = 13;
        
        if (hasTripletSum(arr, target))
            System.out.println("true");
        else
            System.out.println("false");
    }
}


#x. 4-Sum Problem
=====================
import java.util.*;

public class tUf {

    public static List<List<Integer>> fourSum(int[] nums, int target) {
        int n = nums.length; // size of the array
        Set<List<Integer>> set = new HashSet<>();

        // checking all possible quadruplets:
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                for (int k = j + 1; k < n; k++) {
                    for (int l = k + 1; l < n; l++) {
                        // taking bigger data type
                        // to avoid integer overflow:
                        long sum = (long)nums[i] + nums[j];
                        sum += nums[k];
                        sum += nums[l];

                        if (sum == target) {
                            List<Integer> temp = Arrays.asList(nums[i], nums[j], nums[k], nums[l]);
                            Collections.sort(temp);
                            set.add(temp);
                        }
                    }
                }
            }
        }
        List<List<Integer>> ans = new ArrayList<>(set);
        return ans;
    }

    public static void main(String[] args) {
        int[] nums = {4, 3, 3, 4, 4, 2, 1, 2, 1, 1};
        int target = 9;
        List<List<Integer>> ans = fourSum(nums, target);
        System.out.println("The quadruplets are: ");
        for (List<Integer> it : ans) {
            System.out.print("[");
            for (int ele : it) {
                System.out.print(ele + " ");
            }
            System.out.print("] ");
        }
        System.out.println();
    }
}



Find the repeating and missing number
======================================
import java.util.ArrayList;

class GfG {

    static ArrayList<Integer> findTwoElement(int[] arr) {
        int n = arr.length;

        // frequency array to count occurrences
        int[] freq = new int[n + 1]; 
        int repeating = -1;
        int missing = -1;

        // count frequency of each element
        for (int i = 0; i < n; i++) {
            freq[arr[i]]++;
        }

        // identify missing and repeating numbers
        for (int i = 1; i <= n; i++) {
            if (freq[i] == 0) missing = i;
            else if (freq[i] == 2) repeating = i;
        }

        ArrayList<Integer> result = new ArrayList<>();
        result.add(repeating);
        result.add(missing);
        return result;
    }

    public static void main(String[] args) {
        int[] arr = {3, 1, 3};
        ArrayList<Integer> ans = findTwoElement(arr);

        System.out.println(ans.get(0) + " " + ans.get(1));
    }
}


Maximum Product Subarray
===========================
class GfG {
  
    static int maxProduct(int arr[]) { 

      	int n = arr.length;
      
        // Initializing result
        int maxProd = arr[0];

        for (int i = 0; i < n; i++) {
            int mul = 1;
          
            // traversing in current subarray
            for (int j = i; j < n; j++) {
                mul *= arr[j];
              
                // updating result every time
                // to keep track of the maximum product
                maxProd = Math.max(maxProd, mul);
            }
        }
        return maxProd;
    }

    public static void main(String[] args) {
        int arr[] = { -2, 6, -3, -10, 0, 2 };
        System.out.println(maxProduct(arr));
    }
}


Merge Sort
===============
// Java program for Merge Sort

class MergeSort {
  
    // Merges two subarrays of a[]
    void merge(int a[], int l, int m, int r)
    {

      	int n1 = m - l + 1;
        int n2 = r - m;

        int L[] = new int[n1];
        int R[] = new int[n2];

        for (int i = 0; i < n1; ++i)
            L[i] = a[l + i];

      	for (int j = 0; j < n2; ++j)
            R[j] = a[m + 1 + j];

        // Merge the temp arrays
        // Initial indexes of first and second subarrays
        int i = 0, j = 0;

        int k = l;
        while (i < n1 && j < n2) {
            if (L[i] <= R[j]) {
                a[k] = L[i];
                i++;
            }
            else {
                a[k] = R[j];
                j++;
            }
            k++;
        }

        while (i < n1) {
            a[k] = L[i];
            i++;
            k++;
        }

        while (j < n2) {
            a[k] = R[j];
            j++;
            k++;
        }
    }

    // Main function that sorts a[l..r] using
    // merge()
    void sort(int a[], int l, int r)
    {
        if (l < r) {
          
            int m = (l + r) / 2;

            // Sort first and second halves
            sort(a, l, m);
            sort(a, m + 1, r);

            // Merge the sorted halves
            merge(a, l, m, r);
        }
    }

    // Driver method
    public static void main(String args[])
    {
        int a[] = { 12, 11, 13, 5, 6, 7 };

        // Calling of Merge Sort
        MergeSort ob = new MergeSort();
        ob.sort(a, 0, a.length - 1);

        int n = a.length;
        for (int i = 0; i < n; ++i)
            System.out.print(a[i] + " ");
    }
}



Count Inversions
====================
// Java program to count inversions 
// in an array
class Test 
{
    static int arr[] =
           new int[] {1, 20, 6, 4, 5};

    static int getInvCount(int n)
    {
        int inv_count = 0;
        for (int i = 0; i < n - 1; i++)
            for (int j = i + 1; j < n; j++)
                if (arr[i] > arr[j])
                    inv_count++;

        return inv_count;
    }

    // Driver code
    public static void main(String[] args)
    {
        System.out.println("Number of inversions are " + 
                            getInvCount(arr.length));
    }
}


Reverse Pairs
===============
class GfG {

    // Function to count reverse pairs
    static int countRevPairs(int[] arr) {
        
        int n = arr.length;
        int count = 0;

        // Iterate through all pairs (i, j)
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                
                // Check if arr[i] > 2 * arr[j]
                if (arr[i] > 2 * arr[j]) {
                    count++;
                }
            }
        }

        return count;
    }

    public static void main(String[] args) {

        int[] arr = {3, 2, 4, 5, 1, 20};

        System.out.println(countRevPairs(arr));
    }
}


Majority Element (>n/2 times)
==============================
class GfG {

    static int majorityElement(int[] arr) {
        int n = arr.length; 

        // Loop to consider each element as 
        // a candidate for majority
        for (int i = 0; i < n; i++) {
            int count = 0;

            // Inner loop to count the frequency of arr[i]
            for (int j = 0; j < n; j++) {
                if (arr[i] == arr[j]) {
                    count++;
                }
            }

            // Check if count of arr[i] is more
            // than half the size of the array
            if (count > n / 2) {
                return arr[i];
            }
        }

        // If no majority element found, return -1
        return -1;
    }

    public static void main(String[] args) {
        int[] arr = {1, 1, 2, 1, 3, 5, 1};

        System.out.println(majorityElement(arr));
    }
}


Next Permutation
===================

import java.util.*;

class GfG {

    // Function to generate all possible permutations
    static void generatePermutations(List<List<Integer>> res,
                                     int[] arr, int idx) {

        // Base case: if idx reaches the end of array
        if (idx == arr.length - 1) {
            List<Integer> temp = new ArrayList<>();
            for (int x : arr) temp.add(x);
            res.add(temp);
            return;
        }

        // Generate all permutations by swapping
        for (int i = idx; i < arr.length; i++) {
            swap(arr, idx, i);

            // Recur for the next index
            generatePermutations(res, arr, idx + 1);

            // Backtrack to restore original array
            swap(arr, idx, i);
        }
    }

    static void swap(int[] arr, int i, int j) {
        int t = arr[i];
        arr[i] = arr[j];
        arr[j] = t;
    }

    // Function to find the next permutation
    static void nextPermutation(int[] arr) {

        List<List<Integer>> res = new ArrayList<>();

        // Generate all permutations
        generatePermutations(res, arr, 0);

        // Sort all permutations lexicographically
        Collections.sort(res, (a, b) -> {
            for (int i = 0; i < a.size(); i++) {
                if (!a.get(i).equals(b.get(i))) {
                    return a.get(i) - b.get(i);
                }
            }
            return 0;
        });

        // Find the current permutation index
        for (int i = 0; i < res.size(); i++) {

            // If current permutation matches input
            boolean match = true;
            for (int j = 0; j < arr.length; j++) {
                if (arr[j] != res.get(i).get(j)) {
                    match = false;
                    break;
                }
            }

            if (match) {

                // If it's not the last permutation
                if (i < res.size() - 1) {
                    for (int j = 0; j < arr.length; j++) {
                        arr[j] = res.get(i + 1).get(j);
                    }
                }

                // If it's the last permutation
                else {
                    for (int j = 0; j < arr.length; j++) {
                        arr[j] = res.get(0).get(j);
                    }
                }

                break;
            }
        }
    }

    public static void main(String[] args) {

        int[] arr = {2, 4, 1, 7, 5, 0};

        nextPermutation(arr);

        for (int x : arr) {
            System.out.print(x + " ");
        }
    }
}


Set Matrix Zeros
==================
class Solution {
    public void setZeroes(int[][] matrix) {
        int m = matrix.length;
        int n = matrix[0].length;
        boolean firstRowZero = false;
        boolean firstColZero = false;

        // Determine if the first row needs to be zeroed
        for (int j = 0; j < n; j++) {
            if (matrix[0][j] == 0) {
                firstRowZero = true;
                break;
            }
        }

        // Determine if the first column needs to be zeroed
        for (int i = 0; i < m; i++) {
            if (matrix[i][0] == 0) {
                firstColZero = true;
                break;
            }
        }

        // Use the first row and column as markers
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                if (matrix[i][j] == 0) {
                    matrix[0][j] = 0;
                    matrix[i][0] = 0;
                }
            }
        }

        // Set elements to zero based on markers in the first row and column
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                if (matrix[i][0] == 0 || matrix[0][j] == 0) {
                    matrix[i][j] = 0;
                }
            }
        }

        // Set the first row to zero if necessary
        if (firstRowZero) {
            for (int j = 0; j < n; j++) {
                matrix[0][j] = 0;
            }
        }

        // Set the first column to zero if necessary
        if (firstColZero) {
            for (int i = 0; i < m; i++) {
                matrix[i][0] = 0;
            }
        }
    }
}


Majority Element (n/3 times)
===============================
import java.util.ArrayList;

class GfG {

    static ArrayList<Integer> findMajority(int[] arr) {
        int n = arr.length;
        ArrayList<Integer> res = new ArrayList<>();

        for (int i = 0; i < n; i++) {
            // Count the frequency of arr[i]
            int cnt = 0;
            for (int j = i; j < n; j++) {
                if (arr[j] == arr[i])
                    cnt += 1;
            }

            // Check if arr[i] is a majority element
            if (cnt > (n / 3)) {
                // Add arr[i] only if it is not already present
                if (res.size() == 0 || arr[i] != res.get(0)) {
                    res.add(arr[i]);
                }
            }

            // If we have found two majority elements, 
            // we can stop our search
            if (res.size() == 2) {
                if (res.get(0) > res.get(1))
                    java.util.Collections.swap(res, 0, 1);
                break;
            }
        }

        return res;
    }

    public static void main(String[] args) {
        int[] arr = {2, 2, 3, 1, 3, 2, 1, 1};
        ArrayList<Integer> res = findMajority(arr);
        for (int ele : res)
            System.out.print(ele + " ");
    }
}


Merge Overlapping Subintervals
================================
import java.util.ArrayList;
import java.util.Arrays;

class GfG {

    static ArrayList<int[]> mergeOverlap(int[][] arr) {
        int n = arr.length;

        Arrays.sort(arr, (a, b) -> Integer.compare(a[0], b[0]));
        ArrayList<int[]> res = new ArrayList<>();

        // Checking for all possible overlaps
        for (int i = 0; i < n; i++) {
            int start = arr[i][0];
            int end = arr[i][1];

            // Skipping already merged intervals
            if (!res.isEmpty() && res.get(res.size() - 1)[1] >= end) {
                continue;
            }

            // Find the end of the merged range
            for (int j = i + 1; j < n; j++) {
                if (arr[j][0] <= end) {
                    end = Math.max(end, arr[j][1]);
                }
            }
            res.add(new int[]{start, end});
        }
        return res;
    }

    public static void main(String[] args) {
        int[][] arr = {{7, 8}, {1, 5}, {2, 4}, {4, 6}};
        ArrayList<int[]> res = mergeOverlap(arr);

        for (int[] interval : res) {
            System.out.println(interval[0] + " " + interval[1]);
        }
    }
}


Merge two sorted arrays without extra space
=============================================
class Solution {
    private int nextGap(int gap) {
        return (gap <= 1) ? 0 : (gap / 2) + (gap % 2);
    }
    public void mergeArrays(int[] a, int[] b) {
        int n = a.length, m = b.length;
        int gap = n + m;

        for (gap = nextGap(gap); gap > 0; gap = nextGap(gap)) {
            int i, j;
            for (i = 0; i + gap < n; i++) {
                if (a[i] > a[i + gap]) {
                    int temp = a[i];
                    a[i] = a[i + gap];
                    a[i + gap] = temp;
                }
            }
            for (j = (gap > n ? gap - n : 0); i < n && j < m; i++, j++) {
                if (a[i] > b[j]) {
                    int temp = a[i];
                    a[i] = b[j];
                    b[j] = temp;
                }
            }
            for (j = 0; j + gap < m; j++) {
                if (b[j] > b[j + gap]) {
                    int temp = b[j];
                    b[j] = b[j + gap];
                    b[j + gap] = temp;
                }
            }
        }
    }
}


Longest Consecutive Sequence in an Array
Longest subarray with given sum K(positives)
Longest subarray with sum K (Positives + Negatives)
Count subarrays with given sum
Count number of subarrays with given xor K
Search in a 2 D matrix
Leaders in an Array problem
Print the matrix in spiral manner
Rotate Matrix by 90 degrees
Stock Buy and Sell
Rearrange the array in alternating positive and negative items
Find the duplicate in an array of N+1 integers
Kadane's Algorithm, maximum subarray sum
Print subarray with maximum subarray sum (extended version of above problem)
Grid Unique Paths
Sort an array of 0's, 1's and 2's
Pascal's Triangle
2Sum Problem
Find the Union
Find the number that appears once, and other numbers twice.
Find missing number in an array
Remove duplicates from Sorted array
====================================
import java.util.HashSet;

class GfG {

    static int removeDuplicates(int[] arr) {
        
        // To track seen elements
        HashSet<Integer> s = new HashSet<>();
        
        // To maintain the new size of the array
        int idx = 0;  

        for (int i = 0; i < arr.length; i++) {
            if (!s.contains(arr[i])) { 
                s.add(arr[i]);  
                arr[idx++] = arr[i];  
            }
        }

        // Return the size of the array 
        // with unique elements
        return idx;
    }

    public static void main(String[] args) {
        int[] arr = {1, 2, 2, 3, 4, 4, 4, 5, 5};
        int newSize = removeDuplicates(arr);

        for (int i = 0; i < newSize; i++) {
            System.out.print(arr[i] + " ");
        }
    }
}

Left rotate an array by D places
==================================
// Java Program to left rotate the array by d positions
// by rotating one element at a time

import java.util.Arrays;

class GfG {
    
    // Function to left rotate array by d positions
    static void rotateArr(int[] arr, int d) {
        int n = arr.length;
  
        // Repeat the rotation d times
        for (int i = 0; i < d; i++) {
          
            // Left rotate the array by one position
            int first = arr[0];
            for (int j = 0; j < n - 1; j++) {
                arr[j] = arr[j + 1];
            }
            arr[n - 1] = first;
        }
    }

    public static void main(String[] args) {
        int[] arr = { 1, 2, 3, 4, 5, 6 };
        int d = 2;

        rotateArr(arr, d);

        for (int i = 0; i < arr.length; i++)
            System.out.print(arr[i] + " ");
    }
}


Move Zeros to end
=====================
// Java Program to move all zeros to end using temporary array

import java.util.Arrays;

class GfG {
    
    // function to move all zeros to the end
    static void pushZerosToEnd(int[] arr) {
        int n = arr.length;
        int[] temp = new int[n];

        // to keep track of the index in temp[]
        int j = 0;

        // Copy non-zero elements to temp[]
        for (int i = 0; i < n; i++) {
            if (arr[i] != 0)
                temp[j++] = arr[i];
        }

        // Fill remaining positions in temp[] with zeros
        while (j < n)
            temp[j++] = 0;

        // Copy all the elements from temp[] to arr[]
        for (int i = 0; i < n; i++)
            arr[i] = temp[i];
    }

    public static void main(String[] args) {
        int[] arr = {1, 2, 0, 4, 3, 0, 5, 0};
        pushZerosToEnd(arr);

        // Print the modified array
        for (int num : arr) {
            System.out.print(num + " ");
        }
    }
}



Maximum Consecutive Ones
=============================
import java.util.List;

class GfG {
    
    static int maxConsecBits(int[] arr){

        if (arr.length == 0)
            return 0;

        int maxCount = 0, count = 1;
        
        // Loop through the array starting from the second element
        for (int i = 1; i < arr.length; i++) {
            
            // If the current element is the same as the previous one
            // increment the count
            if (arr[i] == arr[i - 1]) {
                count++;
            }
            
            // If not equal, update maxCount if needed and reset count
            else {
                maxCount = Math.max(maxCount, count);
                count = 1;
            }
        }

        return Math.max(maxCount, count);
    }

    public static void main(String[] args){

        int[] arr = { 0, 1, 0, 1, 1, 1, 1 };

        System.out.println(maxConsecBits(arr));
    }
}



Left Rotate an array by one place
===================================
// Java Program to left rotate the array by d positions
// by rotating one element at a time

import java.util.Arrays;

class GfG {
    
    // Function to left rotate array by d positions
    static void rotateArr(int[] arr, int d) {
        int n = arr.length;
  
        // Repeat the rotation d times
        for (int i = 0; i < d; i++) {
          
            // Left rotate the array by one position
            int first = arr[0];
            for (int j = 0; j < n - 1; j++) {
                arr[j] = arr[j + 1];
            }
            arr[n - 1] = first;
        }
    }

    public static void main(String[] args) {
        int[] arr = { 1, 2, 3, 4, 5, 6 };
        int d = 2;

        rotateArr(arr, d);

        for (int i = 0; i < arr.length; i++)
            System.out.print(arr[i] + " ");
    }
}



Linear Search
Second Largest Element in an Array without sorting
Check if the array is sorted
Largest Element in an Array

#2.  Predicates:
======================

Common Functional Interfaces in Java
=====================================

Interface	Abstract Method	Description
Predicate<T>	test(T t)	Returns boolean; often used for filtering.
Function<T,R>	apply(T t)	Takes T and returns R; used for mapping.
Consumer<T>	accept(T t)	Takes T, returns void; used for actions.
Supplier<T>	get()	Returns T; used for supplying values.
UnaryOperator<T>	apply(T t)	Like Function, but input and output types are same.
BinaryOperator<T>	apply(T t1, T t2)	Like BiFunction, but both inputs and output are same type.
BiPredicate<T,U>	test(T t, U u)	Like Predicate, but takes two arguments.
BiFunction<T,U,R>	apply(T t, U u)	Takes two arguments, returns a result.
BiConsumer<T,U>	accept(T t, U u)	Takes two arguments, returns void.


Predicate<String> isEmpty = s -> s.isEmpty();
Function<Integer, String> intToString = i -> String.valueOf(i);
Consumer<String> printer = s -> System.out.println(s);
Supplier<Double> randomSupplier = () -> Math.random();
UnaryOperator<Integer> square = x -> x * x;
BinaryOperator<Integer> sum = (a, b) -> a + b;


----------------------------------------------------------------------
Predicate<Integer> noGreaterThan5 =  x -> x > 5;
List<Integer> list = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

        List<Integer> collect = list.stream()
                .filter(noGreaterThan5)
                .collect(Collectors.toList());

        System.out.println(collect); // [6, 7, 8, 9, 10]
----------------------------------------------------------------------

        List<Integer> list = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

        // multiple filters
        List<Integer> collect = list.stream().filter(x -> x > 5 && x < 8).collect(Collectors.toList());
----------------------------------------------------------------------

        Predicate<Integer> noGreaterThan5 = x -> x > 5;
        Predicate<Integer> noLessThan8 = x -> x < 8;

        List<Integer> list = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

        List<Integer> collect = list.stream()
                .filter(noGreaterThan5.and(noLessThan8))
                .collect(Collectors.toList());

----------------------------------------------------------------------

        Predicate<String> lengthIs3 = x -> x.length() == 3;
        Predicate<String> startWithA = x -> x.startsWith("A");

        List<String> list = Arrays.asList("A", "AA", "AAA", "B", "BB", "BBB");

        List<String> collect = list.stream()
                .filter(lengthIs3.or(startWithA))
                .collect(Collectors.toList());

----------------------------------------------------------------------

        Predicate<String> startWithA = x -> x.startsWith("A");

        List<String> list = Arrays.asList("A", "AA", "AAA", "B", "BB", "BBB");

        List<String> collect = list.stream()
                .filter(startWithA.negate())
                .collect(Collectors.toList());

----------------------------------------------------------------------
        List<String> lines = Arrays.asList("spring", "node", "mkyong");

        List<String> result = lines.stream()                // convert list to stream
                .filter(line -> !"mkyong".equals(line))     // we dont like mkyong
                .collect(Collectors.toList());              // collect the output and convert streams to a List

        result.forEach(System.out::println);                //output : spring, node

----------------------------------------------------------------------

public class Person {

    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    //gettersm setters, toString
}



        List<Person> persons = Arrays.asList(
                new Person("mkyong", 30),
                new Person("jack", 20),
                new Person("lawrence", 40)
        );

        Person result1 = persons.stream()                        // Convert to steam
                .filter(x -> "jack".equals(x.getName()))        // we want "jack" only
                .findAny()                                      // If 'findAny' then return found
                .orElse(null);                                  // If not found, return null

        System.out.println(result1);

----------------------------------------------------------------------

Combining Predicates:

        List<Person> persons = Arrays.asList(
                new Person("mkyong", 30),
                new Person("jack", 20),
                new Person("lawrence", 40)
        );

        Person result1 = persons.stream()
                .filter((p) -> "jack".equals(p.getName()) && 20 == p.getAge())
                .findAny()
                .orElse(null);

        System.out.println("result 1 :" + result1);

----------------------------------------------------------------------

map in Predicates:

        List<Person> persons = Arrays.asList(
                new Person("mkyong", 30),
                new Person("jack", 20),
                new Person("lawrence", 40)
        );

        String name = persons.stream()
                .filter(x -> "jack".equals(x.getName()))
                .map(Person::getName)                        //convert stream to String
                .findAny()
                .orElse("");

        System.out.println("name : " + name);

----------------------------------------------------------------------

List<Integer> transactionsIds = 
    transactions.stream()
                .filter(t -> t.getType() == Transaction.GROCERY)
                .sorted(comparing(Transaction::getValue).reversed())
                .map(Transaction::getId)
                .collect(toList());

----------------------------------------------------------------------

List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8);
List<Integer> twoEvenSquares = 
    numbers.stream()
           .filter(n -> {
                    System.out.println("filtering " + n); 
                    return n % 2 == 0;
                  })
           .map(n -> {
                    System.out.println("mapping " + n);
                    return n * n;
                  })
           .limit(2)
           .collect(toList());


----------------------------------------------------------------------
List<String> words = Arrays.asList("Oracle", "Java", "Magazine");
 List<Integer> wordLengths = 
    words.stream()
         .map(String::length)
         .collect(toList());

----------------------------------------------------------------------

enum Gender {
    FEMALE,
    MALE
}

static class User {
    Gender gender;
    int age;

    public User(Gender gender, int age){
        this.gender = gender;
        this.age = age;
    }

    public Gender getGender() {
        return gender;
    }

    public void setGender(Gender gender) {
        this.gender = gender;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}

static long test1(List<User> users){
    long time1 = System.currentTimeMillis();
    users.stream()
            .filter((u) -> u.getGender() == Gender.FEMALE && u.getAge() % 2 == 0)
            .allMatch(u -> true);                   // least overhead terminal function I can think of
    long time2 = System.currentTimeMillis();
    return time2 - time1;
}

static long test2(List<User> users){
    long time1 = System.currentTimeMillis();
    users.stream()
            .filter(u -> u.getGender() == Gender.FEMALE)
            .filter(u -> u.getAge() % 2 == 0)
            .allMatch(u -> true);                   // least overhead terminal function I can think of
    long time2 = System.currentTimeMillis();
    return time2 - time1;
}

static long test3(List<User> users){
    long time1 = System.currentTimeMillis();
    users.stream()
            .filter(((Predicate<User>) u -> u.getGender() == Gender.FEMALE).and(u -> u.getAge() % 2 == 0))
            .allMatch(u -> true);                   // least overhead terminal function I can think of
    long time2 = System.currentTimeMillis();
    return time2 - time1;
}

public static void main(String... args) {
    int size = 10000000;
    List<User> users =
    IntStream.range(0,size)
            .mapToObj(i -> i % 2 == 0 ? new User(Gender.MALE, i % 100) : new User(Gender.FEMALE, i % 100))
            .collect(Collectors.toCollection(()->new ArrayList<>(size)));
    repeat("one filter with predicate of form u -> exp1 && exp2", users, Temp::test1, 100);
    repeat("two filters with predicates of form u -> exp1", users, Temp::test2, 100);
    repeat("one filter with predicate of form predOne.and(pred2)", users, Temp::test3, 100);
}

private static void repeat(String name, List<User> users, ToLongFunction<List<User>> test, int iterations) {
    System.out.println(name + ", list size " + users.size() + ", averaged over " + iterations + " runs: " + IntStream.range(0, iterations)
            .mapToLong(i -> test.applyAsLong(users))
            .summaryStatistics());
}
----------------------------------------------------------------------
String auth = cookies.stream()
            .filter(c -> c.getName().equals("auth"))
            .map(Cookie::getValue)
            .findAny().orElse("");

----------------------------------------------------------------------
The map operations allows us to apply a function, that takes in a parameter of one type, and returns something else. 

eg. 
Stream students = persons.stream()
      .filter(p -> p.getAge() > 18)
      .map(new Function<Person, Student>() {
                  @Override
                  public Student apply(Person person) {
                     return new Student(person);
                  }
              });

----------------------------------------------------------------------
List<Students> students = persons.stream()
        .filter(p -> p.getAge() > 18)
        .map(Student::new)
        .collect(Collectors.toList());

OR

List<Students> students = persons.stream()
        .filter(p -> p.getAge() > 18)
        .map(Student::new)
        .collect(Collectors.toCollection(ArrayList::new));

----------------------------------------------------------------------

import java.util.List;
  import java.util.function.Predicate;

  public class PredicateExample {
      public static void main(String[] args) {
          List<Integer> ages = List.of(17, 18, 19, 28, 18, 28, 46, 7, 8, 9, 21, 12);
          NotLessThan18<Integer> isAdult = new NotLessThan18<>();
          ages.stream().filter(isAdult).forEach(System.out::println);
      }
  }



class NotLessThan18<E> implements Predicate<Integer> {

      @Override
      public boolean test(Integer v) {
          Integer ADULT = 18;
          return v >= ADULT;
      }
  }

----------------------------------------------------------------------

       int[] ages = { 18, 28, 18, 46, 90, 45, 2, 3, 1, 5, 7, 21, 12 };

       IntPredicate p = n -> n >= 18;

       Arrays.stream(ages).filter(p).forEach(System.out::println);

----------------------------------------------------------------------

    Predicate<String> predicate1 =  str -> str.startsWith("J");
    Predicate<String> predicate2 =  str -> str.length() < 4;
    
    List<String> result = names.stream()
      .filter(predicate1.or(predicate2.negate()))
      .collect(Collectors.toList());
    
    assertEquals(3, result.size());
    assertThat(result, contains("Adam","Alexander","John"));

----------------------------------------------------------------------

Combine Predicates Inline

We don’t need to explicitly define our Predicates to use and(),  or(), and negate().

We can also use them inline by casting the Predicate:

@Test
public void whenFilterListWithCombinedPredicatesInline_thenSuccess(){
    List<String> result = names.stream()
      .filter(((Predicate<String>)name -> name.startsWith("A"))
      .and(name -> name.length()<5))
      .collect(Collectors.toList());

    assertEquals(1, result.size());
    assertThat(result, contains("Adam"));
}

----------------------------------------------------------------------

@Test
public void whenFilterListWithCollectionOfPredicatesUsingAnd_thenSuccess(){
    List<Predicate<String>> allPredicates = new ArrayList<Predicate<String>>();
    allPredicates.add(str -> str.startsWith("A"));
    allPredicates.add(str -> str.contains("d"));        
    allPredicates.add(str -> str.length() > 4);
    
    List<String> result = names.stream()
      .filter(allPredicates.stream().reduce(x->true, Predicate::and))
      .collect(Collectors.toList());
    
    assertEquals(1, result.size());
    assertThat(result, contains("Alexander"));
}

OR

@Test
public void whenFilterListWithCollectionOfPredicatesUsingOr_thenSuccess(){
    List<String> result = names.stream()
      .filter(allPredicates.stream().reduce(x->false, Predicate::or))
      .collect(Collectors.toList());
    
    assertEquals(2, result.size());
    assertThat(result, contains("Adam","Alexander"));
}
----------------------------------------------------------------------

import java.util.function.Predicate;

class User {
    String name;
    User(String name) { this.name = name; }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof User)) return false;
        User user = (User) o;
        return name.equals(user.name);
    }
}

public class IsEqualCustomObjectExample {
    public static void main(String[] args) {
        User targetUser = new User("Alice");
        Predicate<User> isAlice = Predicate.isEqual(targetUser);

        System.out.println(isAlice.test(new User("Alice"))); // true
        System.out.println(isAlice.test(new User("Bob")));   // false
    }
}


----------------------------------------------------------------------

JVM Arguments:

#1. How to determine the amount of memory your application requires? The easiest method is to activate the GC logging in JVM parameters by running

	-verbose:gc -XX:+PrintGCDetails

This way, before the application exits, the total and used memory values will be printed in the console.



----------------------------------------------------------------------
