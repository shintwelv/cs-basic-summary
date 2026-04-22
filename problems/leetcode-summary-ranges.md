# Summary Ranges

## Description

You are given a **sorted unique** integer array nums.

A range `[a,b]` is the set of all integers from a to b (inclusive).

Return the **smallest sorted list of ranges** that cover all the numbers in the array exactly. That is, each element of `nums` is covered by exactly one of the ranges, and there is no integer `x` such that `x` is in one of the ranges but not in `nums`.

Each range `[a,b]` in the list should be output as:

- `"a->b"` if `a != b`
- `"a"` if `a == b`

## Examples
### Example 1

> Input: nums = [0,1,2,4,5,7]
> 
> Output: ["0->2","4->5","7"]
> 
> Explanation: The ranges are:
> [0,2] --> "0->2"
> [4,5] --> "4->5"
> [7,7] --> "7"

### Example 2

> Input: nums = [0,2,3,4,6,8,9]
> 
> Output: ["0","2->4","6","8->9"]
>
> Explanation: The ranges are:
> [0,0] --> "0"
> [2,4] --> "2->4"
> [6,6] --> "6"
> [8,9] --> "8->9"

## Constraints

- 0 <= nums.length <= 20
- -2^31 <= nums[i] <= 2^31 - 1
- All the values of nums are **unique**.
- nums is sorted in ascending order.
 
## Follow Up
- None

## Solution
## 풀이
<details>
<summary>
확인
</summary>

### 1. 문제 분석 및 접근
- **문제 목적**: 
- **제약 조건**: 
- **접근 방법**: 

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

## 관련 개념
