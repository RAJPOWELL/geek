# Second Largest

## Problem

Given an array of **positive** integers **arr[]**, return the **second largest** element from the array. If the second largest element doesn't exist then return **-1.**

Note: The second largest element should not be equal to the largest element.

**Examples:**

```
Input: arr[] = [12, 35, 1, 10, 34, 1]
Output: 34
Explanation: The largest element of the array is 35 and the second largest element is 34.
```

```
Input: arr[] = [10, 5, 10]
Output: 5
Explanation: The largest element of the array is 10 and the second largest element is 5.
```

```
Input: arr[] = [10, 10, 10]
Output: -1
Explanation: The largest element of the array is 10 and the second largest element does not exist.
```

**Constraints:**  
2 ≤ arr.size() ≤ 105  
1 ≤ arr[i]≤ 105

## Solution

# Second Largest Element in an Array

Last Updated : 
10 Feb, 2025

Comments

Improve

Suggest changes

Like Article

Like



Report

[Try it on GfG Practice

![redirect icon](https://media.geeksforgeeks.org/auth-dashboard-uploads/Group-arrow.svg)](https://www.geeksforgeeks.org/problems/second-largest3735/1)

Given an array of ****positive**** integers ****arr[]**** of size ****n****, the task is to find ****second largest distinct element**** in the array.

****Note:**** If the second largest element does not exist, return ****-1****.

****Examples:****

> ****Input:**** arr[] = [12, 35, 1, 10, 34, 1]  
> ****Output:**** 34  
> ****Explanation:**** The largest element of the array is 35 and the second largest element is 34.
>
> ****Input:**** arr[] = [10, 5, 10]  
> ****Output:**** 5  
> ****Explanation:**** The largest element of the array is 10 and the second largest element is 5.
>
> ****Input:**** arr[] = [10, 10, 10]  
> ****Output:**** -1  
> ****Explanation:**** The largest element of the array is 10 there is no second largest element.

Table of Content

* [[Naive Approach] Using Sorting](#naive-approach-using-sorting-onlogn-time-and-o1-space)
* [[Better Approach] Two Pass Search](#better-approach-two-pass-search-on-time-and-o1-space)
* [[Expected Approach] One Pass Search](#expected-approach-one-pass-search-on-time-and-o1-space)

### ****[Naive Approach] Using Sorting****

> The idea is to [sort](https://www.geeksforgeeks.org/dsa/sorting-algorithms/) the array in ****non-decreasing**** order. Now, we know that the largest element will be at index ****n - 1****. So, starting from index ****(n - 2)****, traverse the remaining array in ****reverse order.**** As soon as we encounter an element which is ****not equal**** to the largest element, return it as the ****second largest element**** in the array. If all the elements are equal to the largest element, return ****-1****.

C++

```` ```
// C++ program to find second largest element in an array
// using Sorting

#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

// function to find the second largest element
int getSecondLargest(vector<int> &arr) {
    int n = arr.size();
    
    // Sort the array in non-decreasing order
    sort(arr.begin(), arr.end());
  
    // start from second last element as last element is the largest
    for (int i = n - 2; i >= 0; i--) {
      
        // return the first element which is not equal to the 
        // largest element
        if (arr[i] != arr[n - 1]) {
            return arr[i];
        }
    }
  
    // If no second largest element was found, return -1
    return -1;
}

int main() {
    vector<int> arr = { 12, 35, 1, 10, 34, 1 };
    cout<<getSecondLargest(arr);
    return 0;
}
``` ````
C

```` ```
// C program to find second largest element in an array using Sorting

#include <stdio.h>

// function to compare two integers for qsort
int compare(const void *a, const void *b) {
    return (*(int *)a - *(int *)b);
}

// function to find the second largest element
int getSecondLargest(int arr[], int n) {
    
    // Sort the array in non-decreasing order
    qsort(arr, n, sizeof(int), compare);
  
    // start from second last element as last element is the largest
    for (int i = n - 2; i >= 0; i--) {
        
        // return the first element which is not equal to the 
        // largest element
        if (arr[i] != arr[n - 1]) {
            return arr[i];
        }
    }
  
    // If no second largest element was found, return -1
    return -1;
}

int main() {
    int arr[] = { 12, 35, 1, 10, 34, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    printf("%d\n", getSecondLargest(arr, n));
    return 0;
}
``` ````
Java

```` ```
// Java program to find second largest element in an array
// using Sorting

import java.util.Arrays;

class GfG {
    
    // function to find the second largest element
    static int getSecondLargest(int[] arr) {
        int n = arr.length;
        
        // Sort the array in non-decreasing order
        Arrays.sort(arr);
        
        // start from second last element as last element is the largest
        for (int i = n - 2; i >= 0; i--) {
            
            // return the first element which is not equal to the 
            // largest element
            if (arr[i] != arr[n - 1]) {
                return arr[i];
            }
        }
        
        // If no second largest element was found, return -1
        return -1;
    }

    public static void main(String[] args) {
        int[] arr = { 12, 35, 1, 10, 34, 1 };
        System.out.println(getSecondLargest(arr));
    }
}
``` ````
Python

```` ```
# Python program to find second largest element in an array
# using Sorting

def getSecondLargest(arr):
    n = len(arr)
    
    # Sort the array in non-decreasing order
    arr.sort()
  
    # start from second last element as last element is the largest
    for i in range(n - 2, -1, -1):
      
        # return the first element which is not equal to the 
        # largest element
        if arr[i] != arr[n - 1]:
            return arr[i]
    
    # If no second largest element was found, return -1
    return -1

if __name__ == "__main__":
    arr = [12, 35, 1, 10, 34, 1]
    print(getSecondLargest(arr))
``` ````
C#

```` ```
// C# program to find second largest element in an array
// using Sorting

using System;

class GfG {
    
    // function to find the second largest element
    public static int getSecondLargest(int[] arr) {
        int n = arr.Length;
        
        // Sort the array in non-decreasing order
        Array.Sort(arr);
  
        // start from second last element as last element is the largest
        for (int i = n - 2; i >= 0; i--) {
            
            // return the first element which is not equal to the 
            // largest element
            if (arr[i] != arr[n - 1]) {
                return arr[i];
            }
        }
  
        // If no second largest element was found, return -1
        return -1;
    }

    static void Main() {
        int[] arr = { 12, 35, 1, 10, 34, 1 };
        Console.WriteLine(getSecondLargest(arr));
    }
}
``` ````
JavaScript

```` ```
// JavaScript program to find second largest element in an array
// using Sorting

// function to find the second largest element
function getSecondLargest(arr) {
    let n = arr.length;
    
    // Sort the array in non-decreasing order
    arr.sort((a, b) => a - b);
  
    // start from second last element as last element is the largest
    for (let i = n - 2; i >= 0; i--) {
      
        // return the first element which is not equal to the 
        // largest element
        if (arr[i] !== arr[n - 1]) {
            return arr[i];
        }
    }
  
    // If no second largest element was found, return -1
    return -1;
}

const arr = [12, 35, 1, 10, 34, 1];
console.log(getSecondLargest(arr));
``` ````

**Output**

```
34
```

****Time Complexity:**** O(n\*log(n)), as sorting the array takes ****O(n\*log(n))**** time and traversing the array can take ****O(n)**** time in the worst case, so total time complexity = ****(n\*log(n) + n) = O(n\*log(n))****.  
****Auxiliary space:**** O(1),as no extra space is required.

### [Better Approach] Two Pass Search

> The approach is to traverse the array ****twice****. In the first traversal, find the ****maximum**** element. In the second traversal, find the maximum element ****ignoring the one we found in the first traversal****.

****Working:****

C++

```` ```
// C++ program to find the second largest element in the array
// using two traversals

#include <iostream>
#include <vector>
using namespace std;

// function to find the second largest element in the array
int getSecondLargest(vector<int> &arr) {
    int n = arr.size();

    int largest = -1, secondLargest = -1;

    // finding the largest element
    for (int i = 0; i < n; i++) {
        if (arr[i] > largest)
            largest = arr[i];
    }

    // finding the second largest element
    for (int i = 0; i < n; i++) {

        // Update second largest if the current element is greater
        // than second largest and not equal to the largest
        if (arr[i] > secondLargest && arr[i] != largest) {
            secondLargest = arr[i];
        }
    }
    return secondLargest;
}

int main() {
    vector<int> arr = {12, 35, 1, 10, 34, 1};
    cout << getSecondLargest(arr);

    return 0;
}
``` ````
C

```` ```
// C program to find the second largest element in the array
// using two traversals

#include <stdio.h>

// Function to find the second largest element in the array
int getSecondLargest(int arr[], int n) {
    
    int largest = -1, secondLargest = -1;

    // Finding the largest element
    for (int i = 0; i < n; i++) {
        if (arr[i] > largest)
            largest = arr[i];
    }

    // Finding the second largest element
    for (int i = 0; i < n; i++) {
        
        // Update second largest if the current element is greater
        // than second largest and not equal to the largest
        if (arr[i] > secondLargest && arr[i] != largest) {
            secondLargest = arr[i];
        }
    }
    return secondLargest;
}

int main() {
    int arr[] = {12, 35, 1, 10, 34, 1}; 
	int n = sizeof(arr)/sizeof(arr[0]);
  
    printf("%d\n", getSecondLargest(arr, n)); 
    return 0; 
}
``` ````
Java

```` ```
// Java program to find the second largest element in the array
// using two traversals

import java.util.Arrays;

class GfG {

    // Function to find the second largest element in the array
    static int getSecondLargest(int[] arr) {
        int n = arr.length;

        int largest = -1, secondLargest = -1;

        // Finding the largest element
        for (int i = 0; i < n; i++) {
            if (arr[i] > largest)
                largest = arr[i];
        }

        // Finding the second largest element
        for (int i = 0; i < n; i++) {
            
            // Update second largest if the current element is greater
            // than second largest and not equal to the largest
            if (arr[i] > secondLargest && arr[i] != largest) {
                secondLargest = arr[i];
            }
        }
        return secondLargest;
    }

    public static void main(String[] args) {
        int[] arr = {12, 35, 1, 10, 34, 1};
        System.out.println(getSecondLargest(arr));
    }
}
``` ````
Python

```` ```
# Python program to find the second largest element in the array
# using two traversals

# Function to find the second largest element in the array
def getSecondLargest(arr):
    n = len(arr)

    largest = -1
    secondLargest = -1

    # Finding the largest element
    for i in range(n):
        if arr[i] > largest:
            largest = arr[i]

    # Finding the second largest element
    for i in range(n):
        
        # Update second largest if the current element is greater
        # than second largest and not equal to the largest
        if arr[i] > secondLargest and arr[i] != largest:
            secondLargest = arr[i]
    
    return secondLargest

if __name__ == "__main__":
    arr = [12, 35, 1, 10, 34, 1]
    print(getSecondLargest(arr))
``` ````
C#

```` ```
// C# program to find the second largest element in the array
// using two traversals

using System;

class GfG {
    
    // Function to find the second largest element in the array
    static int getSecondLargest(int[] arr) {
        int n = arr.Length;

        int largest = -1, secondLargest = -1;

        // Finding the largest element
        for (int i = 0; i < n; i++) {
            if (arr[i] > largest)
                largest = arr[i];
        }

        // Finding the second largest element
        for (int i = 0; i < n; i++) {
            
            // Update second largest if the current element is greater
            // than second largest and not equal to the largest
            if (arr[i] > secondLargest && arr[i] != largest) {
                secondLargest = arr[i];
            }
        }
        return secondLargest;
    }

    static void Main() {
        int[] arr = { 12, 35, 1, 10, 34, 1 };
        Console.WriteLine(getSecondLargest(arr));
    }
}
``` ````
JavaScript

```` ```
// JavaScript program to find the second largest element in the array
// using two traversals

function getSecondLargest(arr) {
    let n = arr.length;

    let largest = -1, secondLargest = -1;

    // Finding the largest element
    for (let i = 0; i < n; i++) {
        if (arr[i] > largest)
            largest = arr[i];
    }

    // Finding the second largest element
    for (let i = 0; i < n; i++) {
        
        // Update second largest if the current element is greater
        // than second largest and not equal to the largest
        if (arr[i] > secondLargest && arr[i] !== largest) {
            secondLargest = arr[i];
        }
    }
    return secondLargest;
}

let arr = [12, 35, 1, 10, 34, 1];
console.log(getSecondLargest(arr));
``` ````

**Output**

```
34
```

****Time Complexity:**** O(2\*n) = O(n)****,**** as we are traversing the array two times.  
****Auxiliary space:**** O(1), as no extra space is required.

### ****[Expected Approach] One Pass Search****

> The idea is to keep track of the ****largest**** and ****second largest**** element while traversing the array. Initialize largest and secondLargest with ****-1****. Now, for any index i,
>
> * If ****arr[i]**** ****> largest****, update secondLargest with largest and largest with arr[i].
> * Else If ****arr[i] < largest and arr[i] > secondLargest****, update secondLargest with arr[i].

****Working:****

C++

```` ```
// C++ program to find the second largest element in the array
// using one traversal

#include <iostream>
#include <vector>
using namespace std;

// function to find the second largest element in the array
int getSecondLargest(vector<int> &arr) {
    int n = arr.size();

    int largest = -1, secondLargest = -1;

    // finding the second largest element
    for (int i = 0; i < n; i++) {

        // If arr[i] > largest, update second largest with
        // largest and largest with arr[i]
        if(arr[i] > largest) {
        	secondLargest = largest;
            largest = arr[i];
        }
      
        // If arr[i] < largest and arr[i] > second largest, 
        // update second largest with arr[i]
      	else if(arr[i] < largest && arr[i] > secondLargest) {
        	secondLargest = arr[i];
        }
    }
    return secondLargest;
}

int main() {
    vector<int> arr = {12, 35, 1, 10, 34, 1};
    cout << getSecondLargest(arr);

    return 0;
}
``` ````
C

```` ```
// C program to find the second largest element in the array
// using one traversal

#include <stdio.h>

// function to find the second largest element in the array
int getSecondLargest(int arr[], int n) {
    int largest = -1, secondLargest = -1;

    // finding the second largest element
    for (int i = 0; i < n; i++) {

        // If arr[i] > largest, update second largest with
        // largest and largest with arr[i]
        if(arr[i] > largest) {
            secondLargest = largest;
            largest = arr[i];
        }
      
        // If arr[i] < largest and arr[i] > second largest, 
        // update second largest with arr[i]
        else if(arr[i] < largest && arr[i] > secondLargest) {
            secondLargest = arr[i];
        }
    }
    return secondLargest;
}

int main() {
    int arr[] = {12, 35, 1, 10, 34, 1};
    int n = sizeof(arr) / sizeof(arr[0]);
    printf("%d\n", getSecondLargest(arr, n));

    return 0;
}
``` ````
Java

```` ```
// Java program to find the second largest element in the array
// using one traversal

import java.util.Arrays;

class GfG {
    
    // function to find the second largest element in the array
    static int getSecondLargest(int[] arr) {
        int n = arr.length;

        int largest = -1, secondLargest = -1;

        // finding the second largest element
        for (int i = 0; i < n; i++) {

            // If arr[i] > largest, update second largest with
            // largest and largest with arr[i]
            if(arr[i] > largest) {
                secondLargest = largest;
                largest = arr[i];
            }
          
            // If arr[i] < largest and arr[i] > second largest, 
            // update second largest with arr[i]
            else if(arr[i] < largest && arr[i] > secondLargest) {
                secondLargest = arr[i];
            }
        }
        return secondLargest;
    }

    public static void main(String[] args) {
        int[] arr = {12, 35, 1, 10, 34, 1};
        System.out.println(getSecondLargest(arr));
    }
}
``` ````
Python

```` ```
# Python program to find the second largest element in the array
# using one traversal

# function to find the second largest element in the array
def getSecondLargest(arr):
    n = len(arr)

    largest = -1
    secondLargest = -1

    # finding the second largest element
    for i in range(n):

        # If arr[i] > largest, update second largest with
        # largest and largest with arr[i]
        if arr[i] > largest:
            secondLargest = largest
            largest = arr[i]
      
        # If arr[i] < largest and arr[i] > second largest, 
        # update second largest with arr[i]
        elif arr[i] < largest and arr[i] > secondLargest:
            secondLargest = arr[i]

    return secondLargest

if __name__ == "__main__":
    arr = [12, 35, 1, 10, 34, 1]
    print(getSecondLargest(arr))
``` ````
C#

```` ```
// C# program to find the second largest element in the array
// using one traversal

using System;

class GfG {
    
    // function to find the second largest element in the array
    static int getSecondLargest(int[] arr) {
        int n = arr.Length;

        int largest = -1, secondLargest = -1;

        // finding the second largest element
        for (int i = 0; i < n; i++) {
            
            // If arr[i] > largest, update second largest with
            // largest and largest with arr[i]
            if (arr[i] > largest) {
                secondLargest = largest;
                largest = arr[i];
            }
          
            // If arr[i] < largest and arr[i] > second largest, 
            // update second largest with arr[i]
            else if (arr[i] < largest && arr[i] > secondLargest) {
                secondLargest = arr[i];
            }
        }
        return secondLargest;
    }

    static void Main() {
        int[] arr = { 12, 35, 1, 10, 34, 1 };
        Console.WriteLine(getSecondLargest(arr));
    }
}
``` ````
JavaScript

```` ```
// JavaScript program to find the second largest element in the array
// using one traversal

// function to find the second largest element in the array
function getSecondLargest(arr) {
    const n = arr.length;

    let largest = -1, secondLargest = -1;

    // finding the second largest element
    for (let i = 0; i < n; i++) {

        // If arr[i] > largest, update second largest with
        // largest and largest with arr[i]
        if (arr[i] > largest) {
            secondLargest = largest;
            largest = arr[i];
        }
      
        // If arr[i] < largest and arr[i] > second largest, 
        // update second largest with arr[i]
        else if (arr[i] < largest && arr[i] > secondLargest) {
            secondLargest = arr[i];
        }
    }
    return secondLargest;
}

const arr = [12, 35, 1, 10, 34, 1];
console.log(getSecondLargest(arr));
``` ````

**Output**

```
34
```

****Time Complexity:**** O(n),as we are traversing the array only once.  
****Auxiliary space:**** O(1)

****Related Article****: [Smallest and second smallest element in an array](https://www.geeksforgeeks.org/dsa/to-find-smallest-and-second-smallest-element-in-an-array/)

  

Second Largest Element in an Array

[Visit Course
![explore course icon](https://media.geeksforgeeks.org/auth-dashboard-uploads/Vector11.svg)](https://www.geeksforgeeks.org/courses/gfg-160-series)

Comment

More info

H

Harsh Agarwal

Improve

Article Tags :

* [Misc](https://www.geeksforgeeks.org/category/misc/)
* [DSA](https://www.geeksforgeeks.org/category/dsa/)
* [Arrays](https://www.geeksforgeeks.org/category/dsa/data-structures/c-arrays/)
* [Order-Statistics](https://www.geeksforgeeks.org/tag/order-statistics/)
* [Accolite](https://www.geeksforgeeks.org/tag/accolite/)
* [Zoho](https://www.geeksforgeeks.org/tag/zoho/)
* [Hike](https://www.geeksforgeeks.org/tag/hike/)
* [SAP Labs](https://www.geeksforgeeks.org/tag/sap-labs/)
* [FactSet](https://www.geeksforgeeks.org/tag/factset/)

+5 More
