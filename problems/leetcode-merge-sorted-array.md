# Merge Sorted Array

## Description

You are given two integer arrays `nums1` and `nums2`, sorted in **non-decreasing order**, and two integers `m` and `n`, representing the number of elements in `nums1` and `nums2` respectively.

Merge `nums1` and `nums2` into a single array sorted in non-decreasing order.

The final sorted array should not be returned by the function, but instead be stored inside the array `nums1`. To accommodate this, `nums1` has a length of `m + n`, where the first `m` elements denote the elements that should be merged, and the last `n` elements are set to `0` and should be ignored. `nums2` has a length of `n`.

## Examples
### Example 1

> Input: nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
>
> Output: [1,2,2,3,5,6]
>
> Explanation: The arrays we are merging are [1,2,3] and [2,5,6].
> The result of the merge is [1,2,2,3,5,6] with the underlined elements coming from nums1.

### Example 2

> Input: nums1 = [1], m = 1, nums2 = [], n = 0
> 
> Output: [1]
> 
> Explanation: The arrays we are merging are [1] and [].
> The result of the merge is [1].

### Example 3

> Input: nums1 = [0], m = 0, nums2 = [1], n = 1
> 
> Output: [1]
> 
> Explanation: The arrays we are merging are [] and [1].
> The result of the merge is [1].
> Note that because m = 0, there are no elements in nums1. The 0 is only there to ensure the merge result can fit in nums1.
 

## Constraints

- `nums1.length == m + n`
- `nums2.length == n`
- `0 <= m, n <= 200`
- `1 <= m + n <= 200`
-  $-10^9$ <= nums1[i], nums2[j] <= $10^9$
 
## Follow Up
Can you come up with an algorithm that runs in $O(m + n)$ time?

## Solution
## 풀이
<details>
<summary>
확인
</summary>

### 1. 문제 분석 및 접근
- **문제 목적**: 이미 정렬된 두 배열 `nums1`과 `nums2`를 합쳐서 하나의 정렬된 배열로 만듭니다. 결과는 `nums1`에 직접 저장해야 합니다.
- **제약 조건**: `nums1`은 `m + n`의 길이를 가지고 있으며, 뒤쪽 `n`개의 공간은 0으로 채워져 비어 있는 상태입니다. 추가 공간 없이 `nums1` 내부에서 해결해야 합니다 ($O(1)$ 공간 복잡도).
- **접근 방법**: 앞에서부터 비교하여 채우기 시작하면 `nums1`의 기존 원소들을 뒤로 밀어야 하는 번거로움이 발생합니다. 하지만 두 배열 모두 오름차순으로 정렬되어 있으므로, **뒤쪽(가장 큰 값)부터 비교하여 채워 넣으면** 기존 원소를 덮어쓰지 않고 효율적으로 정렬할 수 있습니다. 이는 **[배열(Array)](../data-structure/array-linkedlist.md)**의 특성을 활용한 효율적인 데이터 처리 방식입니다.

---

### 2. 핵심 알고리즘
- **역방향 포인터 (Three Pointers from the back)**:
    1. `mIndex`: `nums1`의 실제 데이터 끝 (`m - 1`)을 가리키는 포인터.
    2. `nIndex`: `nums2`의 끝 (`n - 1`)을 가리키는 포인터.
    3. `index`: 합쳐질 결과물인 `nums1`의 전체 끝 (`m + n - 1`)을 가리키는 포인터.
- `mIndex`와 `nIndex` 위치의 값을 비교하여 더 큰 값을 `index` 위치에 넣고 해당 포인터와 `index`를 감소시킵니다.
- 이는 **[정렬(Sort)](../algorithm/sort.md)** 알고리즘 중 병합 정렬(Merge Sort)의 핵심인 '병합(Merge)' 과정을 추가적인 메모리 공간 없이 수행하는 방식입니다.
- `nums2`의 모든 원소가 `nums1`으로 옮겨질 때까지 반복합니다.

---

### 3. 상세 동작 시나리오 (Dry Run)
- **Input**: `nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3`
    - `mIndex = 2 (값: 3)`, `nIndex = 2 (값: 6)`, `index = 5`
    - **Step 1**: `3 < 6` 이므로 `nums1[5] = 6`. `nIndex = 1`, `index = 4`.
    - **Step 2**: `3 < 5` 이므로 `nums1[4] = 5`. `nIndex = 0`, `index = 3`.
    - **Step 3**: `3 > 2` 이므로 `nums1[3] = 3`. `mIndex = 1`, `index = 2`.
    - **Step 4**: `2 == 2` 이므로 `nums1[2] = 2` (mIndex쪽). `mIndex = 0`, `index = 1`.
    - **Step 5**: `1 < 2` 이므로 `nums1[1] = 2`. `nIndex = -1`, `index = 0`.
    - **Step 6**: `nIndex < 0` 이므로 남은 `nums1` 원소는 그대로 둡니다 (또는 루프 종료).
- **Output**: `[1, 2, 2, 3, 5, 6]`

---

### 4. 코드 구현 (Swift)

```swift
class Solution {
    func merge(_ nums1: inout [Int], _ m: Int, _ nums2: [Int], _ n: Int) {
        guard n > 0 else { return }
        
        if m == 0 {
            for i in 0..<n {
                nums1[i] = nums2[i]
            }
            return
        }
        
        var mIndex: Int = m - 1
        var nIndex: Int = n - 1
        var index: Int = m + n - 1
        
        while index >= 0 {
            defer {
                index -= 1
            }
            
            if mIndex < 0 {
                nums1[index] = nums2[nIndex]
                nIndex -= 1
                continue
            }
            
            if nIndex < 0 {
                nums1[index] = nums1[mIndex]
                mIndex -= 1
                continue
            }
            
            let mValue = nums1[mIndex]
            let nValue = nums2[nIndex]
            
            if mValue >= nValue {
                nums1[index] = mValue
                mIndex -= 1
            } else {
                nums1[index] = nValue
                nIndex -= 1
            }
        }
    }
}
```

### 5. 복잡도 분석
- **시간 복잡도**: $O(m + n)$
    - 두 배열의 모든 원소를 한 번씩만 순회하며 비교하므로 원소의 총합에 비례하는 시간이 소요됩니다.
- **공간 복잡도**: $O(1)$
    - `nums1`의 빈 공간을 활용하여 제자리(in-place)에서 수정을 수행하므로 추가적인 배열 공간이 필요하지 않습니다.

</details>

---

## 관련 문제
- **[LeetCode - Summary Ranges](./leetcode-summary-ranges.md)**: 정렬된 배열을 단일 순회하며 연속된 구간을 처리하는 유사한 배열 탐색 문제.
- **[LeetCode - Search Insert Position](./leetcode-search-insert-position.md)**: 정렬된 배열을 활용하는 또 다른 기초 문제.

---

## 관련 개념
- **[정렬 (Sort)](../algorithm/sort.md)**: 이미 정렬된 두 배열을 합치는 과정은 병합 정렬(Merge Sort)의 핵심 원리입니다.
- **[배열 (Array)](../data-structure/array-linkedlist.md)**: In-place 수정을 위해 배열의 특성을 활용합니다.