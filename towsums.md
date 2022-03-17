Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

### General Optimization Gaol --> Reduce number of comparisons

nums = [2,7,11,15]

target=9

n=len(nums)=4

total pairs = n! / (n-2)! = 16

| (2)  | (7)  | (11)  | (15)  |
|--------|--------|---------|---------|
| (2,2)  | (7,2)  | (11,2)  | (15,2)  |
| (2,7)  | (7,7)  | (11,7)  | (15,7)  |
| (2,11) | (7,11) | (11,11) | (15,11) |
| (2,15) | (7,15) | (11,15) | (15,15) |

total pairs when skipping equal elements =  n!/2!  =12

total pairs when skipping swapped elements/foward moving= n!/(2! * (n-2)! =6



#### Case Analysis:

Best Case: i,j are first elements

Worst Case:  i,j are last elements

average case:



# Attempts

### Brute Force (Version 1 )

test each pair and skip equal elements

```
def twoSum( nums, target):
    arr_size=len(nums)
    i=0
    j=1
    while i<arr_size:
        while j<arr_size:
            if i!=j and nums[i]+nums[j]==target:
                return [i,j]
            j+=1
        i+=1
        j=1
```


##### Step count analysis
nums of assignments= 6

nums of checks= 4

cost = 6a+4c + c



### Brute Force  (Version 2)

test each pair without need to skip equal elements

#### approach
- reuse value/ decrease assignment
- decrease number of condional checks

```
def twoSum( nums, target):
    arr_size=len(nums)
    i=0
    while i<arr_size:
        j=i+1
        while j<arr_size:
            if nums[i]+nums[j]==target:
                return [i,j]
            j+=1
        i+=1
```

##### Step count analysis


nums of assignments= 5
nums of checks= 3

cost = 6a+4c + c



### Brute Force  (Version 3) 

#### approach
- caching array access



```
def twoSum( nums, target):
    arr_size=len(nums)
    i=0
    while i<arr_size:
        j=i+1
        cached_i=nums[i]
        while j<arr_size:
            if cached_i+nums[j]==target:
                return [i,j]
            j+=1
        i+=1
```


### Brute Force  (Version 4) 

#### approach

- using incremental step/skip technique

![Screenshot](incremental_step_twosums.png)


```
def twoSum( nums, target):
    arr_size=len(nums)
    step=1
   
    while step<arr_size:
        i=0
        while i<arr_size-1:
            j=i+step
            if j<arr_size and nums[i]+nums[j]==target:
                return [i,j]
            i+=1
        step+=1
        
```


### Recursive  (Version 1) 

#### approach 
- tail recursion

### cons
- Stack Overflow, depth limit --> 1000


```
def twoSumR( nums, target):
    arr_size=len(nums)
    def _twoSumInner(nums,target,i):
        j=i+1
        cached_i=nums[i]
        while j<arr_size:
            if cached_i+nums[j]==target:
                return [i,j]
            j+=1
        if i<arr_size:
            return _twoSumInner(nums,target,i+1)
        
    return _twoSumInner(nums,target,0)
```

### Recursive  (Version 2) 

#### approach 
- mutual recursion  
 
### cons
- stack overflow/segmenation fault


```
def twoSumR( nums, target):
    arr_size=len(nums)
    
    def _outerR(nums,target,i):
        if i<arr_size-1:
            return _innerR(nums,target,i,i+1)
            
    def _innerR(nums,target,i,j):
        if nums[i]+nums[j]==target:
            return [i,j]
            
        if j<arr_size-1:
            return _innerR(nums,target,i,j+1)
            
        return _outerR(nums,target,i+1)
        
        
    return _outerR(nums,target,0)
```


