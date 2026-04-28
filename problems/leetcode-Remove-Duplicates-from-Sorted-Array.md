# Remove Duplicates from Sorted Array

## Description

Given an integer array `nums` sorted in **non-decreasing order**, remove the duplicates **in-place** such that each unique element appears only **once**. The relative order of the elements should be kept the **same**.

Consider the number of unique elements in `nums` to be `k`. After removing duplicates, return the number of unique elements `k`.

The first `k` elements of `nums` should contain the unique numbers in **sorted order**. The remaining elements beyond index `k - 1` can be ignored.

**Custom Judge:**

The judge will test your solution with the following code:
```
int[] nums = [...]; // Input array
int[] expectedNums = [...]; // The expected answer with correct length

int k = removeDuplicates(nums); // Calls your implementation

assert k == expectedNums.length;
for (int i = 0; i < k; i++) {
    assert nums[i] == expectedNums[i];
}
```
If all assertions pass, then your solution will be accepted.

## Examples
### Example 1

> Input: nums = [1,1,2]
>
> Output: 2, nums = [1,2,_]
>
> Explanation: Your function should return k = 2, with the first two elements of nums being 1 and 2 respectively.
> 
> It does not matter what you leave beyond the returned k (hence they are underscores).

### Example 2

> Input: nums = [0,0,1,1,1,2,2,3,3,4]
> 
> Output: 5, nums = [0,1,2,3,4,_,_,_,_,_]
> 
> Explanation: Your function should return k = 5, with the first five elements of nums being 0, 1, 2, 3, and 4 respectively.
> 
> It does not matter what you leave beyond the returned k (hence they are underscores). 

## Constraints

- `1 <= nums.length <= 3 * 10^4`
- `-100 <= nums[i] <= 100`
- `nums` is sorted in non-decreasing order.
 
## Follow Up
- None

## Solution
## 풀이
<details>
<summary>
확인
</summary>

### 1. 문제 분석 및 접근


---

### 2. 핵심 알고리즘

---

### 3. 상세 동작 시나리오 (Dry Run)

---

### 4. 코드 구현 (Swift)

```swift

```

### 5. 복잡도 분석
- **시간 복잡도**: 
- **공간 복잡도**: 

</details>

---

## 관련 문제

## 관련 개념

