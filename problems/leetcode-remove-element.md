# Remove Element

## Description

Given an integer array `nums` and an integer `val`, remove all occurrences of `val` in `nums` **in-place**. The order of the elements may be changed. Then return the number of elements in `nums` which are not equal to `val`. 

Consider the number of elements in `nums` which are not equal to `val` be `k`, to get accepted, you need to do the following things:

Change the array `nums` such that the first `k` elements of `nums` contain the elements which are not equal to `val`. The remaining elements of `nums` are not important as well as the size of `nums`.
Return `k`.

## Examples
### Example 1

> Input: nums = [3,2,2,3], val = 3
> 
> Output: 2, nums = [2,2,_,_]
> 
> Explanation: Your function should return k = 2, with the first two elements of nums being 2.
It does not matter what you leave beyond the returned k (hence they are underscores).

### Example 2

> Input: nums = [0,1,2,2,3,0,4,2], val = 2
> 
> Output: 5, nums = [0,1,4,0,3,_,_,_]
> 
> Explanation: Your function should return k = 5, with the first five elements of nums containing 0, 0, 1, 3, and 4.
> 
> Note that the five elements can be returned in any order.
> 
> It does not matter what you leave beyond the returned k (hence they are underscores).
 
## Constraints

- 0 <= nums.length <= 100
- 0 <= nums[i] <= 50
- 0 <= val <= 100

## Follow Up
- None

## Solution
## 풀이
<details>
<summary>
확인
</summary>

### 1. 문제 분석 및 접근
- **문제 목적**: 주어진 배열 `nums`에서 특정 값 `val`과 일치하는 모든 요소를 **제자리(in-place)**에서 제거하고, 남은 요소의 개수 `k`를 반환합니다.
- **제약 조건**: `nums[i]`의 값은 0 이상 50 이하입니다.
- **접근 방법**: 
    - 배열을 순회하며 `val`과 일치하는 요소를 제약 조건 범위를 벗어나는 값인 `51`로 변경합니다.
    - 이후 정렬을 통해 `51`로 표시된 요소들을 배열의 뒤쪽으로 밀어냅니다.
    - 전체 배열 길이에서 `val`이 발견된 횟수를 뺀 값을 반환합니다.

---

### 2. 핵심 알고리즘
- **값 치환**: `val`과 동일한 데이터를 감지하여 특정 '마커(51)' 값으로 바꿉니다.
- **커스텀 정렬**: Swift의 `sort` 메서드를 사용하여 마커 값(`51`)이 항상 뒤로 가도록 정렬 기준을 정의합니다.

---

### 3. 상세 동작 시나리오 (Dry Run)
- **입력**: `nums = [3, 2, 2, 3], val = 3`
1. **순회 및 치환**:
   - `i = 0`: `nums[0]`은 3이므로 51로 변경. (`valCount = 1`)
   - `i = 1`: `nums[1]`은 2이므로 통과.
   - `i = 2`: `nums[2]`은 2이므로 통과.
   - `i = 3`: `nums[3]`은 3이므로 51로 변경. (`valCount = 2`)
   - 결과: `nums = [51, 2, 2, 51]`
2. **정렬**:
   - `51`이 아닌 값들을 앞으로, `51`인 값들을 뒤로 정렬.
   - 결과: `nums = [2, 2, 51, 51]`
3. **반환**:
   - `nums.count(4) - valCount(2) = 2` 반환.

---

### 4. 코드 구현 (Swift)

```swift
class Solution {
    func removeElement(_ nums: inout [Int], _ val: Int) -> Int {
        var valCount: Int = 0
        for i in 0..<nums.count {
            if nums[i] == val {
                nums[i] = 51 // 제약 조건(0~50)을 벗어나는 값으로 표시
                valCount += 1
            }
        }
        
        // 표시된 값을 뒤로 보내는 정렬
        nums.sort { num1, num2 in
            if num1 == 51 { return false }
            return true
        }
        
        return nums.count - valCount
    }
}
```

### 5. 복잡도 분석
- **시간 복잡도**: $O(N \log N)$ - 배열 순회에 $O(N)$, 정렬 수행에 $O(N \log N)$이 소요됩니다.
- **공간 복잡도**: $O(1)$ - 추가적인 배열 공간을 사용하지 않고 기존 배열 내에서 처리가 이루어집니다. (단, Swift의 `sort` 내부 구현에 따라 일시적인 스택 공간이 사용될 수 있음)
    
</details>

---

## 관련 개념
- [Array](../data-structure/array-linkedlist.md)
- [정렬 (Sort)](../algorithm/sort.md)
- Two Pointers (권장되는 최적화 기법)

## 추천 관련 문제
- [LeetCode - Merge Sorted Array](../problems/leetcode-merge-sorted-array.md): 배열 내에서 제자리(in-place) 수정을 수행하는 유사한 유형의 문제입니다.