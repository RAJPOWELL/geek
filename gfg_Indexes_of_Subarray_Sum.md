# Indexes of Subarray Sum

## Problem

Given an array **arr[]** containing only non-negative integers, your task is to find a continuous subarray (a contiguous sequence of elements) whose sum equals a specified value **`target`**. You need to return the **1-based indices** of the leftmost and rightmost elements of this subarray. You need to find the first subarray whose sum is equal to the target.

Note: If no such array is possible then, return [-1].

**Examples:**

```
Input: arr[] = [1, 2, 3, 7, 5], target = 12
Output: [2, 4]
Explanation: The sum of elements from 2nd to 4th position is 12.
```

```
Input: arr[] = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10], target = 15
Output: [1, 5]
Explanation: The sum of elements from 1st to 5th position is 15.
```

```
Input: arr[] = [5, 3, 4], target = 2
Output: [-1]
Explanation: There is no subarray with sum 2.
```

**Constraints:**1 <= arr.size()<= 1060 <= arr[i] <= 103  
0 <= target <= 109

## Solution

# Subarray with Given Sum

Last Updated : 
23 Jul, 2025

Comments

Improve

Suggest changes

Like Article

Like



Report

[Try it on GfG Practice

![redirect icon](https://media.geeksforgeeks.org/auth-dashboard-uploads/Group-arrow.svg)](https://www.geeksforgeeks.org/problems/subarray-with-given-sum-1587115621/1)

Given a 1-based indexing array ****arr[]**** of ****non-negative**** integers and an integer ****sum****. You mainly need to return the left and right indexes(****1-based indexing****) of that subarray. In case of multiple subarrays, return the subarray indexes which come first on moving from left to right. If no such subarray exists return an array consisting of element ****-1****.

****Examples:**** 

> ****Input****: arr[] = [15, 2, 4, 8, 9, 5, 10, 23], target = 23  
> ****Output****: [2, 5]  
> *****Explanation:***** Sum of subarray arr[2...5] is 2 + 4 + 8 + 9 = 23.
>
> ****Input****: arr[] = [1, 10, 4, 0, 3, 5], target = 7  
> ****Output****: [3, 5]  
> *****Explanation:***** Sum of subarray arr[3...5] is 4 + 0 + 3 = 7.
>
> ****Input****: arr[] = [1, 4], target = 0  
> ****Output****: [-1]  
> *****Explanation:***** There is no subarray with 0 sum.

Table of Content

* [[Naive Approach] Using Nested loop - O(n2) Time and O(1) Space](#naive-using-nested-loop-on2-time-and-o1-auxiliary-space)
* [[Expected Approach] Sliding Window - O(n) Time and O(1) Space](#expected-approach-using-sliding-window-ontime-and-o1-auxiliary-space)
* [[Alternate Approach] Hashing + Prefix Sum - O(n) Time and O(n) Space](#-hashing-prefix-sum-ontime-and-on-space)

### [Naive Approach] Using ****Nested loop**** - O(n^2) Time and O(1) S****pace****

The very basic idea is to use a nested loop where the outer loop picks a starting element, and the inner loop calculates the cumulative sum of elements starting from this element.

> For each starting element, the inner loop iterates through subsequent elements and adding each element to the cumulative sum until the given sum is found or the end of the array is reached. If at any point the cumulative sum equals the given ****sum****, then return starting and ending indices (1-based). If no such sub-array is found after all iterations, then return -1.

C++

```` ```
#include <iostream>
#include <vector>
using namespace std;

// Function to find a continuous sub-array which adds up to
// a given number.
vector<int> subarraySum(vector<int> arr, int target) {
    vector<int> res;
    int n = arr.size();

    // Pick a starting point for a subarray
    for (int s = 0; s < n; s++) {
        int curr = 0;
      	
        // Consider all ending points
        // for the picked starting point 
        for (int e = s; e < n; e++) {
            curr += arr[e];
            if (curr == target) {
                res.push_back(s + 1);
                res.push_back(e + 1);
                return res;
            }
        }
    }
  	// If no subarray is found
    return {-1}; 
}

int main() {
    vector<int> arr = {15, 2, 4, 8, 9, 5, 10, 23};
    int target = 23;
    vector<int> res = subarraySum(arr, target);
  
    for (int ele : res)
        cout << ele << " ";
    return 0;
}
``` ````
Java

```` ```
import java.util.ArrayList;
import java.util.List;

class GfG {
    // Function to find a continuous sub-array which adds up to
    // a given number.
    static ArrayList<Integer> subarraySum(int[] arr, int target) {
        ArrayList<Integer> res = new ArrayList<>();
        int n = arr.length;

        // Pick a starting point for a subarray
        for (int s = 0; s < n; s++) {
            int curr = 0;

            // Consider all ending points
            // for the picked starting point
            for (int e = s; e < n; e++) {
                curr += arr[e];
                if (curr == target) {
                    res.add(s + 1);
                    res.add(e + 1);
                    return res;
                }
            }
        }
        // If no subarray is found
        res.add(-1);
        return res;
    }

    public static void main(String[] args) {
        int[] arr = {15, 2, 4, 8, 9, 5, 10, 23};
        int target = 23;
        ArrayList<Integer> res = subarraySum(arr, target);

        for (int ele : res)
            System.out.print(ele + " ");
    }
}
``` ````
Python

```` ```
# Function to find a continuous sub-array which adds up to
# a given number.
def subarraySum(arr, target):
    res = []
    n = len(arr)

    # Pick a starting point for a subarray
    for s in range(n):
        curr = 0

        # Consider all ending points
        # for the picked starting point
        for e in range(s, n):
            curr += arr[e]
            if curr == target:
                res.append(s + 1)
                res.append(e + 1)
                return res

    # If no subarray is found
    return [-1]
  	
if __name__ == "__main__":
    arr = [15, 2, 4, 8, 9, 5, 10, 23]
    target = 23
    res = subarraySum(arr, target)

    for ele in res:
        print(ele, end=" ")
``` ````
C#

```` ```
using System;
using System.Collections.Generic;

class GfG {
    // Function to find a continuous sub-array which adds up to
    // a given number.
    static List<int> subarraySum(int[] arr, int target) {
        List<int> res = new List<int>();
        int n = arr.Length;

        // Pick a starting point for a subarray
        for (int s = 0; s < n; s++) {
            int curr = 0;

            // Consider all ending points
            // for the picked starting point
            for (int e = s; e < n; e++) {
                curr += arr[e];
                if (curr == target) {
                    res.Add(s + 1);
                    res.Add(e + 1);
                    return res;
                }
            }
        }
        // If no subarray is found
        res.Add(-1);
        return res;
    }

    static void Main() {
        int[] arr = {15, 2, 4, 8, 9, 5, 10, 23};
        int target = 23;
        List<int> res = subarraySum(arr, target);

        foreach (var ele in res)
            Console.Write(ele + " ");
    }
}
``` ````
JavaScript

```` ```
// Function to find a continuous sub-array which adds up to
// a given number.
function subarraySum(arr, target) {
    let res = [];
    let n = arr.length;

    // Pick a starting point for a subarray
    for (let s = 0; s < n; s++) {
        let curr = 0;

        // Consider all ending points
        // for the picked starting point
        for (let e = s; e < n; e++) {
            curr += arr[e];
            if (curr === target) {
                res.push(s + 1);
                res.push(e + 1);
                return res;
            }
        }
    }
    // If no subarray is found
    return [-1];
}

// Driver Code
let arr = [15, 2, 4, 8, 9, 5, 10, 23];
let target = 23;
let res = subarraySum(arr, target);

console.log(res.join(' '));
``` ````

**Output**

```
2 5
```

### [****Expected Approach****] ****Sliding Window**** - O(n) Time ****and**** O(1) S****pace****

> The idea is simple, as we know that all the elements in subarray are positive so, If a subarray has sum greater than the ****given sum**** then there is no possibility that adding elements to the current subarray will be equal to the given sum. So the Idea is to use a similar approach to a [****sliding window****](https://www.geeksforgeeks.org/dsa/window-sliding-technique/). 
>
> * Start with an empty window
> * add elements to the window while the current sum is less than ****sum****
> * If the sum is greater than *****sum*****, remove elements from the ****start**** of the current window.
> * If current sum becomes same as ****sum,**** return the result

C++

```` ```
#include <iostream>
#include <vector>
using namespace std;

// Function to find a continuous sub-array which adds up to
// a given number.
vector<int> subarraySum(vector<int>& arr, int target) {
  	// Initialize window
    int s = 0, e = 0;  
    vector<int> res;

    int curr = 0;
    for (int i = 0; i < arr.size(); i++) {
        curr += arr[i];

        // If current sum becomes more or equal,
        // set end and try adjusting start
        if (curr >= target) {
            e = i;

            // While current sum is greater, 
          	// remove starting elements of current window
            while (curr > target && s < e) {
                curr -= arr[s];
                ++s;
            }

            // If we found a subraay
            if (curr == target) {
                res.push_back(s + 1);
                res.push_back(e + 1);
                return res;
            }
        }
    }
	// If no subarray is found
    return {-1};
}

int main() {
    vector<int> arr = {15, 2, 4, 8, 9, 5, 10, 23};
    int target = 23;
    vector<int> res = subarraySum(arr, target);
    for (int ele : res)
        cout << ele << " ";
    return 0;
}
``` ````
Java

```` ```
import java.util.ArrayList;
import java.util.List;

class GfG {
    // Function to find a continuous sub-array which adds up to
    // a given number.
    static ArrayList<Integer> subarraySum(int[] arr, int target) {
        // Initialize window
        int s = 0, e = 0;  
        ArrayList<Integer> res = new ArrayList<>();

        int curr = 0;
        for (int i = 0; i < arr.length; i++) {
            curr += arr[i];

            // If current sum becomes more or equal,
            // set end and try adjusting start
            if (curr >= target) {
                e = i;

                // While current sum is greater, 
                // remove starting elements of current window
                while (curr > target && s < e) {
                    curr -= arr[s];
                    ++s;
                }

                // If we found a subarray
                if (curr == target) {
                    res.add(s + 1);
                    res.add(e + 1);
                    return res;
                }
            }
        }
        // If no subarray is found
        res.add(-1);
        return res;
    }

    public static void main(String[] args) {
        int[] arr = {15, 2, 4, 8, 9, 5, 10, 23};
        int target = 23;
        ArrayList<Integer> res = subarraySum(arr, target);

        for (int ele : res)
            System.out.print(ele + " ");
    }
}
``` ````
Python

```` ```
# Function to find a continuous sub-array which adds up to
# a given number.
def subarraySum(arr, target):
    # Initialize window
    s, e = 0, 0
    res = []

    curr = 0
    for i in range(len(arr)):
        curr += arr[i]

        # If current sum becomes more or equal,
        # set end and try adjusting start
        if curr >= target:
            e = i

            # While current sum is greater, 
            # remove starting elements of current window
            while curr > target and s < e:
                curr -= arr[s]
                s += 1

            # If we found a subarray
            if curr == target:
                res.append(s + 1)
                res.append(e + 1)
                return res

    # If no subarray is found
    return [-1]
  	
if __name__ == "__main__":
    arr = [15, 2, 4, 8, 9, 5, 10, 23]
    target = 23
    res = subarraySum(arr, target)

    print(" ".join(map(str, res)))
``` ````
C#

```` ```
using System;
using System.Collections.Generic;

class GfG {
    // Function to find a continuous sub-array which adds up to
    // a given number.
    static List<int> subarraySum(int[] arr, int target) {
        // Initialize window
        int s = 0, e = 0;
        List<int> res = new List<int>();

        int curr = 0;
        for (int i = 0; i < arr.Length; i++) {
            curr += arr[i];

            // If current sum becomes more or equal,
            // set end and try adjusting start
            if (curr >= target) {
                e = i;

                // While current sum is greater, 
                // remove starting elements of current window
                while (curr > target && s < e) {
                    curr -= arr[s];
                    ++s;
                }

                // If we found a subarray
                if (curr == target) {
                    res.Add(s + 1);
                    res.Add(e + 1);
                    return res;
                }
            }
        }
        // If no subarray is found
        res.Add(-1);
        return res;
    }

    static void Main() {
        int[] arr = {15, 2, 4, 8, 9, 5, 10, 23};
        int target = 23;
        List<int> res = subarraySum(arr, target);

        foreach (var ele in res)
            Console.Write(ele + " ");
    }
}
``` ````
JavaScript

```` ```
// Function to find a continuous sub-array which adds up to
// a given number.
function subarraySum(arr, target) {
    
    // Initialize window
    let s = 0, e = 0;
    let res = [];

    let curr = 0;
    for (let i = 0; i < arr.length; i++) {
        curr += arr[i];

        // If current sum becomes more or equal,
        // set end and try adjusting start
        if (curr >= target) {
            e = i;

            // While current sum is greater, 
            // remove starting elements of current window
            while (curr > target && s < e) {
                curr -= arr[s];
                s++;
            }

            // If we found a subarray
            if (curr === target) {
                res.push(s + 1);
                res.push(e + 1);
                return res;
            }
        }
    }
    // If no subarray is found
    return [-1];
}

// Driver Code
let arr = [15, 2, 4, 8, 9, 5, 10, 23];
let target = 23;
let res = subarraySum(arr, target);

console.log(res.join(' '));
``` ````

**Output**

```
2 5
```

### [****Alternate Approach****] ****Hashing + Prefix Sum**** - O(n) Time ****and**** O(n) S****pace****

****The above solution does not work for arrays with negative numbers.**** To handle all cases, we use hashing and prefix sum. The idea is to store the sum of elements of every prefix of the array in a hashmap, i.e, every index stores the sum of elements up to that index hashmap. So to check if there is a subarray with a sum equal to *****target*****, check for every index ****i****, and sum up to that index as *****currSum*****. If there is a prefix with a sum equal to ****(*********currSum – target)*****, then the subarray with the given sum is found.

****To know more about the implementation, please refer**** [****Subarray with Given Sum – Handles Negative Numbers****](https://www.geeksforgeeks.org/dsa/find-subarray-with-given-sum-in-array-of-integers/)****.****

  

Subarray with Given Sum | DSA

[Visit Course
![explore course icon](https://media.geeksforgeeks.org/auth-dashboard-uploads/Vector11.svg)](https://www.geeksforgeeks.org/courses/gfg-160-series)

Comment

More info

[K](https://www.geeksforgeeks.org/user/kartik/)

[kartik](https://www.geeksforgeeks.org/user/kartik/)

Follow

Improve

Article Tags :

* [DSA](https://www.geeksforgeeks.org/category/dsa/)
* [Arrays](https://www.geeksforgeeks.org/category/dsa/data-structures/c-arrays/)
* [Amazon](https://www.geeksforgeeks.org/tag/amazon/)
* [Google](https://www.geeksforgeeks.org/tag/google/)
* [Morgan Stanley](https://www.geeksforgeeks.org/tag/morgan-stanley/)
* [Facebook](https://www.geeksforgeeks.org/tag/facebook/)
* [Zoho](https://www.geeksforgeeks.org/tag/zoho/)
* [Visa](https://www.geeksforgeeks.org/tag/visa/)
* [FactSet](https://www.geeksforgeeks.org/tag/factset/)
* [subarray](https://www.geeksforgeeks.org/tag/subarray/)
* [sliding-window](https://www.geeksforgeeks.org/tag/sliding-window/)
* [subarray-sum](https://www.geeksforgeeks.org/tag/subarray-sum/)

+8 More
