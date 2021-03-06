# Array data structure, Introduction to efficiency of algorithms

## Pre-requisite
Before this lesson, you should have gotten familiar with:
- [Essential mathematics for software engineers](Essential%20Mathematics.md)
- [Computer basics and binary](Binary.md)

## Introduction
A common problem in Computer Science is managing large amounts of data and performing different operations on them. <b>Data Structures</b> provide different well-known ways to organize data. Each data structure follows its own set of rules on how the data should get organized. The study of data structures is to understand these rules. Alongside these governing rules, we are also looking to understand how different common operations like insert, delete and search work on each of these data structures and understand the average and worst case efficiency for the common operations. Knowledge of well-known data structures allows us come up with optimal designs to our real world, practical coding projects. The first data structure we will consider is the <b>Array data structure</b>.

## Properties
<b>Arrays</b> or <b>Array data structures</b> have the following properties:
1. Arrays are <b>homogeneous data structure</b>. This means that all the elements in the array are of the same type. E.g. integer array, character array etc. (Aside: a string is really an array of characters).
1. Elements in an array are allocated in a <b>contiguous block of memory</b>. This means that the array element at index `i + 1` will always be next to (and at a higher memory address than the) array element at index `i`, where `i` is an index into the array such that `i` is greater than or equal to 0 and less than the length of the array.
1. Array is a <b>static data structure</b>. Once created, the size of an array is fixed throughout its lifetime. This means the array length is fixed once the array is created. We cannot add more items to the array than the array length allows.

<b>Aside</b>: Since Ruby is the primary language we will be using at Ada, it is important to note that the <b>Array class in Ruby</b> does not implement the <b>Array data structure</b>. Let's contrast the above properties of the array data structure with the objects of the Ruby Array class:
1. <b>Not homogenous</b>: Objects of the Array class in Ruby are not confined to elements of the same type. Element at one index may be a string, while the next could be an integer. You could even have some intermediate element be `nil`.
1. Array class in Ruby makes no claims about where the objects in the Array will be located in memory. Therefore, the elements in a Ruby Array object are not guaranteed to be in a <b>contiguous block of memory</b> with the elements next to each other.
1. The objects of the Ruby Array class can be resized. We can add more elements than the initial size with which we created an Array object in Ruby. Ruby Arrays behave more like <b>dynamic data structures</b> rather than <b>static data structures</b>.

### Example
Consider the following C code defining two integer variables and an array of integers of size 10:
    
        int x = 1; 
        int y = 2; 
        int z[10];
    

Here's an imagination of how this may look like in memory:
<img src="images/arrays-in-memory.png">

In the example code and imagination of memory above;
- `x` is a variable of type integer. If integers take up 2 bytes on an example system, then `x` takes 2 bytes in memory.
- `y` also takes 2 bytes in memory.
- `z` is an array of ten integers. The array `z` is allocated in a contiguous space in memory. This array will take up 10 times the size of integer number of bytes. In our example system, `z` will take 10 × 2 bytes i.e. 20 bytes.

### Indexing
If there are *n* elements in an integer array `z`, then the first integer value is said to be at index 0, the second element is at index 1 and so on. The last element in the array is at index _n - 1_.

Index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9
------|---|---|---|---|---|---|---|---|---|---
Value | 8 | 3 | 5 | 2 | 6 | 8 | 4 | 1 | 7 | 2

Because elements in an array are <b>homogenous</b>, every element at each index in the array takes up the same amount of space in memory. As we learned earlier, arrays are always <b>allocated in a contiguous block of memory</b> such that the array element at index `i` i.e. `array[i]` is always next to and at a lower address than the array element at index `i + 1`. The index `i` into the array has a range such that <b>0 <= `i` < array's length</b>.

<img src="images/array-indexing.png">

<b>Number of operations</b>: No matter how long the array is, indexing into an array is a really fast operation. The time it takes to index into an array does not depend on the length of the array. This is because the indexing operation leverages the homogenous nature of array elements along with the fact that the array elements are allocated in contiguous blocks of memory.

### Search
<b>Exercise</b>: Given an unsorted integer array and its length, devise an algorithm to find if a given value is in the array or not. The algorithm should return `true` if the value is found in the array, and return `false` otherwise. How would you design this algorithm? 
<b>Requirements' gathering</b>: Before we get to considering the actual steps in an algorithm, let us consider our requirements. Here's what we know:
- Inputs to the method being designed:
    - Integer array
    - Length of the array
    - an integer value to find
- Output from the method:
    - `true`, if value is found in the array
    - `false`, if value is not found in the array
<b>Aside note</b>: Requirements' gathering is an important step before we get to algorithm design. This steps helps us confirm that we have captured all of the essentials and there is no ambiguity or misunderstanding in capturing the requirments.

<b>Approach</b>: It's a good practice to <b>always check the input</b> provided to any method. e.g. if the input is an object, always check if the input object value is `nil`. Similarly, if the input is a string, always check if the string is empty. For the problem at hand, to check if a given value exists in the array, it seems useful to check if the array has at least one element. Otherwise, there are no elements in the array and we can safely conclude that the value we are looking for is not in the array and return `false`. Once we have checked the input validity, we could start looking for the value in the array. We can do this by comparing each value in the array one by one with the value we are looking for. If we ever find a match, we can immediately return `true`. If we reach the end of the array and no match was found, then we can return `false`. With that, here's what our solution would look like (in pseudo code):
    
        bool search(array, value_to_find)
        {
            i = 0 
            // i is an index into the first element in the array

            while i < array's length
            {
                // check if value_to_find is the same as value at index i
                if value_to_find == array[i]
                {
                    return true
                }

                // increment i
                i = i + 1
            }

            // value_to_find not in array
            return false
        }
    
<b>Exercise</b>: Try the above algorithm on a sample array and sample value to find. e.g. {4, 8, 0, 3, 9} and value to find is 3. You may try the algoirthm on any other sample inputs.

<b>Number of operations</b>: How many times will the instructions inside the while loop in the code above run?
<details>
    <summary>Counting the number of operations in an algorithm and comparing it with the size and value of input
    </summary>
        In the best case scenario, the input array is empty and we immediately return false. Another relatively quick execution would be if the value to find is at index 0 in the array.In the worst case scenario, the value we are looking for is not found in the array. In this case, the instructions inside the loop will get executed as many times as the number of elements in the array. If there are n elements in the array, then the loop will execute n number of times. In the average cases, the loop will execute somewhere in between the best case and worst case.
</details>

### Minimum and Maximum
<b>Exercise</b>: Given an unsorted integer array and its length, devise an algorithm to find the largest integer value is in the array and return it. Following the approach we applied to the search exercise above, use a paper and pencil to gather the requirements, check the input and author the main algorithm.

We begin again, with <b>gathering the requirements</b>. Here's what we know:
- Inputs to the method being designed:
    - Integer array
    - Length of the array
- Output from the method:
    - largest integer value in the array

Next, we <b>check the input</b>. <b>Question</b>: What should the algorithm return if the array is empty? This is a requirement that is missing in the specification above. Let's say, we want to return `nil` if the array is empty.

Next, let's think about our <b>algorithmic approach</b>. How do we find the largest value in a list of unsorted integer values? One way is to assume that the first value we see if the largest value. Then, we compare this, so far largest known value with the next value in the array. If we find a value that is greater than the largest known value thus far, we update the largest known value. Once we have reached the end of the array, we have found the largest value in the array. Here's what the pseudo code may look like:

        int largest_value(array)
        {
            if array's length == 0
            {
                return nil
            }

            largest_value = array[0]
            i = 1
            while i < array's length
            {
                if array[i] > largest_value
                {
                    largest_value = array[i]
                }
                i = i + 1
            }

            return largest_value
        }
    

<b>Number of operations</b>: How many times will the operations inside the loop get executed?
<details>
    <summary> Counting the number of operations in an algorithm and comparing it with the size and value of input
    </summary>
    The comparison inside the loop will happen exactly one less time than the number of elements in the input array. If there are 10 elements in the input array, then the instructions within the loop will run 9 times. If there are 101 elements in the input array, then the instructions within the loop will run 100 times. 
</details>

<b>Exercise</b>: Modify the algorithm above to devise an algorithm that would return the minimum value in the input array. Try this algorithm and the one above on sample input values.

### Sorted arrays
There are several real world scenarios where we want our data to be ordered in ascending or descending way. Example:
- Sort test scores in descending way
- Sort song playtime in descending way
- Sort identification numbers in ascending way
- Sort names from *A* to *Z* (ascending way) like in the contacts' list on the phone.

Having the data sorted, simplifies some of the algorithms.

<b>Question</b>: If the array is sorted in ascending manner, how would you find the min value, or max value?
<details>
    <summary> Minimum and maximum value in a sorted array
    </summary>
        The algorithms for finding the minimum and maximum values get simplified if the array is sorted. The <b>minimum value</b> in an array that is sorted in an ascending manner will always be the first entry in the array i.e. array[0]. The <b>maximum value</b> in an array that is sorted in an ascending manner will always be the last entry in the array i.e. array[*n*-1], where *n* is the length of the array. If you compare the number of steps needed in this approach, with the approach needed for unsorted arrays, you'll find that the algorithm is significantly simpler and faster if the array is sorted.
</details>

You'll learn more about [algorithms to sort an array](Sorting.md) soon. For now, we can already see how having the array sorted makes finding the maximum and minimum value a faster and simplified algorithm. With that, let's consider searching for a value in a sorted array.

### Binary Search
The <b>binary search</b> algorithm leverages the sorted property while searching for a value in the array. Instead of comparing with each value in the array from index 0 to *n*-1, (where *n* is the number of elements in the array), we can be more methodic in eliminating where the value we are searching for will not be. We already apply the binary approach in our everyday life. E.g. Let's say we are looking for a word in dictionary, or while look for a name in the physical phone book. If the word/name starts with 'h', it will likely be in the first half of the book. We open the book to somewhere in the middle, compare the beginnig letter on that page to the word/name we are looking for. After comparing, we can safely eliminate the second half of the book. We keep eliminating half of the remaining pages in each step after repeating the process of opening a page to somewhere in the middle of valid pages and comparing. Unlike [linear search](#search), where after each comparison, one element is eliminated, with binary search, after each comparison, half of the remaining elements are eliminated.

Here's the pseudo code for binary search algorithm. As you read through it, try the algorithm on different set of input arrays and value to find.

        bool binary_seach(array, value_to_find)
        {
            if array length == 0
            {
                return false
            }

            low = 0 
            // initialized to the index of the first element in the array

            high = array length - 1 
            // initialized to the index of the last element in the array

            while low < high
            {
                mid = (low + high) / 2
                // calculate the index value between low and high

                if array[mid] == value_to_find
                { // compare the element at index mid with the value to find
                    return true
                }
                else if array[mid] > value_to_find
                { // value to find is less than the value at mid index
                    // eliminate the second half
                    high = mid - 1
                }
                else // array[mid] < value_to_find
                { // value to find is greater than the value at mid index
                    // eliminate the first half
                    low = mid + 1
                }
            }

            // consider for arrays with only one element
            if array[low] == value_to_find
            {
                return true
            }

            // value not found in the array
            return false
        }
    

After each iteration through the loop, we eliminate half of the remaining elements in the array:
1. In the beginning the value we are looking for could be anywhere amongst the *n* elements in the array.
1. After the first iteration, i.e. after one comparison, we eliminate either the top half or the bottom half of the array and the value could be somewhere in the remaining *n*/2 elements in the array.
1. After the second iteration, i.e. after one more comparison, we eliminate half of the remaining values, thereby reducing the scope of where the value could be to *n*/4 elements.

Eventually, one or no elements will be left and we'll exit the loop. 

Such a change is known as logarithmic change. As we saw in [essential mathematics](Essential%20Mathematics.md#exponents-and-logarithms), logarithmic change is related to exponential. _Log<sub>2</sub> n_ means at each step the value reduces by half of the remaining.

The main loop in binary seach runs <b>_log<sub>2</sub> n_</b> number of times where *n* is the number of elements in the input array.

### Reverse
<b>Exercise</b>: Devise an algorithm to reverse the elements in the input array _in-place_. e.g. If the input array is:

Index | 0 | 1 | 2 | 3 | 4 
------|---|---|---|---|---
Value | 8 | 3 | 5 | 2 | 6 

then, after the algorithm is complete, the same array should look like:

Index | 0 | 1 | 2 | 3 | 4 
------|---|---|---|---|---
Value | 6 | 2 | 5 | 3 | 8 

<b>Note</b>: _in-place_ means the updates should happen in the same location in memory i.e. in the same location as the original array.

#### Reverse solution 1 - using an auxiliary array
One approach to solve this problem would be create a new array of the same size as the input array. We copy over the element at index 0 in the original array over to index *n*-1 in the new array, where *n* is length of the input array. Then we copy over the element at index 1 in the original array over to index *n*-2 in the new array. We keep repeating the process until all values are copied over. Then, we copy the elements from the new array sequentially from index 0 to *n*-1 to the same index in the original array.

Here's what the pseudo code for this approach look like:

        // array is the input integer array to the algorithm
        
        if array.length <= 1
        {
            return // nothing to reverse
        }

        i = 0
        j = array.length - 1

        // create a new array of the same size as input array
        temp_array = new array of size array.length

        while i < array.length
        {
            // copy over the values in input array 
            // into the temp array in reverse order
            temp_array[i] = array[j]
            increment i
            decrement j
        }

        i = 0
        while i < array.length
        {
            // copy over values from the temp array 
            // into the input array
            array[i] = temp_array[i]
        }

        // array is reversed
    
    
You'll notice that the solution above has two `while` loops in addition to a set of single line code instructions. The two while loops are one after the other.
- The first while loop copies over each of the elements in the input array into a new array in reverse order of their position. The means, if there are 100 elements in the input array, then the loop will execute 100 times. If there are 700,000 elements in the input array, then the loop will execute 700,000 times and so on. Therefore, we can conclude that in the instructions in the first loop run as many times as the number of elements in the input array.
- The second loop copies for each element of the temporary array back into the input array. So, the second loop will also run as many times as the number of elements in the input array.

#### Reverse solution 2 - using swap
Is there any algorithmic approach where we can avoid creating an additional array of the same size as the input array? In order to reverse the elements in the array, we could consider swapping the element at index 0 with the element at index *n*-1, where *n* is the number of elements in the input array. Then, we could swap the element at index *n*-2 with the element at index 1, and so on.
Here's what the pseudo code for this approach would look like:

        // array is the input integer array to the algorithm

        if array.length <= 1
        {
            return // nothing to reverse
        }

        i = 0
        j = array.length - 1

        while i < j
        {
            // swap values at i and j
            temp = array[i]
            array[i] = array[j]
            array[j] = temp

            increment i
            decrement j
        }
    

You'll notice that the loop in this approach will run roughly half the number of times as the number of elements in the input array.

## Exercises
Continue learning about [efficieny of algorithms](Efficiency%20of%20algorithms.md). Then, complete the assignments listed in the section [Arrays and efficiency and algorithms](../homeworks.md#arrays-and-efficiency-of-algorithms)

## Slide Deck
+ Slide Deck used in class</br>
<span xmlns:dct="http://purl.org/dc/terms/" property="dct:title"><a href="https://drive.google.com/file/d/0B__DV26QHsH4eHJqTWttLUdNZk0/view?usp=sharing">Array data structure and Introduction to Efficiency of Algorithms</a></span> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/">Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International License</a>.</br>
<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/88x31.png" /></a><br />
