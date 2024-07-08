# **Chapter 1 (Introduction to algorithms)**

<font size=6>TIme Complexity</font>
Time Complexity is a number of *iterations* that we need to solve the problem using given algorithm. 

*Worst Case Scenario* is a case where we get the maximum number of iterations for given algorithm.

*Best Case Scenario* is a case where we get the minimum number of iterations for given algorithm.

Usually when we talk about complexity of algorithm we talk about *Worst Case Scenario*.

• <font size=5>O(log n), also known as log time. Example: Binary search.</font>
• <font size=5>O(n), also known as linear time. Example: Simple search.</font>
• <font size=5>O(n * log n). Example: A fast sorting algorithm, like  quicksort.</font>
• <font size=5>O(n2 ), also known as quadratic time. Example: A slow sorting algorithm, like selection sort.</font>
• <font size=5>O(n!), also known as factorial time. Example: A really slow algorithm, like the traveling
salesperson.</font>

==Time complexity grows with problem size, therefore in some cases more simple algorithm may seem as better approach, however the true power of algorithm reveals when problem size starts growing.== 

<font size=6>Simple search</font>
Simple search is easiest way to solve array problems, however it is pretty slow
algorithm as it has time complexity of ==**O(n)**==. 

It is an algorithm when we are iterating through each element in the array starting from first(zero-indexed) value.

If we found our target in array then we return index of this value, otherwise we return -1.

Assume we have a problem where we need to find **target** value in array of ints.

`func simpleSearch(array []int, target int) int {`
    `target := 2`
    `for i := 0; i < len(array); i++{`
        `if array[i] == target{`
			`return i`
        `}` 
    `}`
	 `return -1`
`}`

Here is golang code example of solving this problem using .

<font size=6>Binary search</font>
Binary search is a way to make things faster than simple search in problems where
you need to find target values in array. ==**It only works for sorted arrays problems.**== and it has time complexity of ==**O(log n).

The approach consists of two ==pointers==:  **left** which equals to 0(the first element of array) and **right** which equals `len(array) - 1`(the last element of array). We iterate through array until
left pointer is *not bigger* than right pointer. 

In loop we create **mid** variable to find a mid value in array. 

We check if `array[mid]` is equal to target, if so we return mid. 

If **mid value** is less than target we cut left half of array and iterate again, as all value that are left to current int will also be less than target value as array is sorted.

If **mid value** is bigger than target we cut right side of array, because all values will be bigger than current value.

Finally if we found no matches, function returns -1 as the answer.

`func binarySearch(array []int, target int) int {`
    `left := 0`
    `right := len(array) - 1`

    `for (left <= right){`
        `mid := (left + right)/2`
        `if array[mid] == target{`
            `return mid`
        `} else if array[mid] > target{`
            `left = mid + 1`
        `} else {`
            `right = mid - 1`
        `}`
    `}`

    `return -1`
`}`

Here is golang example for this problem using binary search.

<font size=6>Overall</font>
In conclusion binary search algorithm is much faster than simple search in terms of sorted array problems. In some literature it may be found that binary search is 15x faster than simple search. However this is untrue as time complexity growth with amount of data wea are working with.

# Chapter 2 (Selection sort)
