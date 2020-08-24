# Questions

1. [Running Sum of 1d Array](https://leetcode.com/problems/running-sum-of-1d-array/)
2. [Number Of Good Pairs](https://leetcode.com/problems/number-of-good-pairs/)
3. [Two-Sum](https://leetcode.com/problems/two-sum/)


# Solutions

## Running Sum of 1d Array

#### Solution 1 : Using an additional array to store values

Space : O(n) since we are allocating new memory to store n values that we will be calculating
Time : O(n) since we will be iterating over each of the elements once

```
result = []
currSum = 0
for index,num in enumerate(nums):
    currSum += num
    result.append(currSum)

return result
```

#### Solution 2 : Modifying memory in place

Space: O(1) since no additional memory needs to be allocated
Time: O(n) since we will be iterating over each element once.

```
currSum = 0
for index,num in enumerate(nums):
    currSum += num
    nums[index] = currSum
    

return nums
```

## Number of good pairs

#### Solution 1 : Brute force 2 for-loops

We observe that we can solve the problem easily using two for-loops. By using these two for-loops, we effectively ensure that we only increment our count by one when our values are equal but the index of one is larger than another.
This is guaranteed by the for loop


Space : O(1)
Time: O(n^2)
```
count = 0
        for index in range(0,len(nums)-1):
            for index2 in range(index+1, len(nums)):
                if nums[index] == nums[index2]:
                    count+=1
        return count
```


#### Solution 2 : Using decreasing sum

We observe that if we have an array

[1,2,3,4,1,1,1] 

and we convert this to a dictionary representation

x = {
1 : [0,4,5,6],
3 : [2],
2: [1]
4: [3]
}

If we look at just 1, 

we know that the first 1 at index 0 has three potential positions which it can form good pairs with
[0,4], [ 0,5] , [0,6]

We know that the second 1 at index 4 has two
[ 0,5] , [0,6]

We know that the third 1 at index 5 has one
[0,6]

We know that the last 1 has none
[]

This means that if we know the number of occurences of a value in our array, we can calculate the number of good pairs by taking

(n-1) + (n-2) + (n-3) + ... + 0

which sums up to

(n-1)(n)/2 using the formula for a decreasing arithmetic sequence.


Time : O(n)
space: O(n)
```
def numIdenticalPairs(self, nums: List[int]) -> int:
    d = defaultdict(lambda:0)
    for index,char in enumerate(nums):
        d[char]+=1
    count = 0
    for key in d:
        count+= int(d[key] * (d[key]-1)/2)

    return count
```


## Two-Sum

Similar to the question above, two-sum can be solved with a brute force solution using two for-loops

### Using two for-loops
```
for index in range(len(nums)):
  for index2 in range(index+1,len(nums)):
    if nums[index]+nums[index2]==target:
      return [index,index2]
                    
```


### Using a hash map
Time: O(n)
Space: O(n)

```
seen = {}
for index,num in enumerate(nums):
    if target-num in seen:
        return [seen[target-num],index]
    else:
        seen[num] = index
```
