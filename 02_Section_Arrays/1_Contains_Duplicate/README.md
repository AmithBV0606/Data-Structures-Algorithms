# Contains Duplicate

### Problem Statement : 

Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.

**Example 1** :
```
Input: nums = [1,2,3,1]

Output: true

Explanation:

The element 1 occurs at the indices 0 and 3.
```

**Example 2** :
```
Input: nums = [1,2,3,4]

Output: false

Explanation:

All elements are distinct.
```

**Example 3** :
```
Input: nums = [1,1,1,3,3,4,3,2,4,2]

Output: true
```

Link : [Click here](https://leetcode.com/problems/contains-duplicate/description/)

### Solution : 

1. **Brute force approach :** Time complexity: O(n^2)

```c++
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        for(int i = 0; i < nums.size(); i++){
            for (int j = i + 1; j < nums.size(); j++){
                if(nums[i] == nums[j]){
                    return true;
                }
            }
        }

        return false;
    }
};
```

2. **Optimized approach 1 :** Time complexity: O(nlogn)

```C++
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        sort(nums.begin(), nums.end());

        for(int i = 1; i < nums.size(); i++){
            if(nums[i] == nums[i - 1]){
                return true;
            }
        }

        return false;
    }
};
```

3. **Optimized approach 2(Set) :** Time complexity: O(n)

```C++
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        unordered_set<int> numSet;

        for (int n : nums) {
            if (numSet.find(n) != numSet.end()) {
                return true;
            }
            numSet.insert(n);
        }
        
        return false;        
    }
};
```

NOTE : Understanding `unordered_set.find(n)` :

The function `numSet.find(n)` is used to check if the element `n` exists in the `unordered_set (numSet)`.

**How does find(n) work?**

- If `n` does NOT exist in `numSet`, `find(n)` returns `numSet.end()`, which is a special iterator pointing past the last element of the set.

- If `n` exists in `numSet`, `find(n)` returns an iterator (a pointer-like object) pointing to the element inside the set.


4. **Optimized approach 3(set and vector) :** Time complexity: O(n)

```C++
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        unordered_set<int> numSet(nums.begin(), nums.end()); 
        return numSet.size() < nums.size();        
    }
};
```

**NOTE :** Creates an unordered_set named numSet and initializes it with all elements of nums:

- `nums.begin()` and `nums.end()` define the range of elements copied from nums into `numSet`.

- `unordered_set` only stores unique elements, meaning duplicates are automatically removed.