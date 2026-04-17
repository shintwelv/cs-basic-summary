# Search Insert Position

## Description

Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You must write an algorithm with $O(log n)$ runtime complexity.

## Examples
### Example 1

> Input: nums = [1,3,5,6], target = 5
>
> Output: 2

### Example 2

> Input: nums = [1,3,5,6], target = 2
> 
> Output: 1

### Example 3

> Input: nums = [1,3,5,6], target = 7
> 
> Output: 4
 

## Constraints

- `1 <= nums.length <= 3 * 10^4`
- `-10^4 <= nums[i] <= 10^4`
- `nums` contains distinct values sorted in ascending order.
- `-10^4 <= target <= 10^4`
 
## Follow Up
- None

## Solution
## 풀이
<details>
<summary>
확인
</summary>

### 1. 문제 분석 및 접근
- **문제 목적**: 정렬된 중복 없는 정수 배열에서 `target`의 인덱스를 찾거나, 존재하지 않는 경우 정렬 순서를 유지하며 삽입될 위치(인덱스)를 반환합니다.
- **제약 조건**: 시간 복잡도는 $O(\log n)$이어야 합니다. 이는 배열을 처음부터 끝까지 탐색하는 선형 탐색($O(n)$)이 아닌, **이진 탐색(Binary Search)**을 사용해야 함을 의미합니다.
- **접근 방법**: 
    - 배열이 이미 오름차순으로 정렬되어 있으므로 이진 탐색의 범위를 좁혀가며 탐색합니다.
    - `target`을 찾으면 해당 인덱스를 즉시 반환합니다.
    - 탐색이 끝날 때까지 찾지 못한 경우, `left` 포인터가 가리키는 위치가 삽입될 적절한 위치가 됩니다.

---

### 2. 핵심 알고리즘
- **이진 탐색 (Binary Search)**:
    - `left`와 `right` 포인터를 사용하여 탐색 범위를 설정합니다.
    - 중간 지점 `mid`를 계산하고 `nums[mid]`와 `target`을 비교합니다.
    - `nums[mid] == target`: 인덱스 반환.
    - `nums[mid] < target`: `left`를 `mid + 1`로 이동하여 오른쪽 탐색.
    - `nums[mid] > target`: `right`를 `mid - 1`로 이동하여 왼쪽 탐색.

---

### 3. 상세 동작 시나리오 (Dry Run)
**예시 2: `nums = [1, 3, 5, 6]`, `target = 2`**

1. **초기 상태**: `left = 0`, `right = 3`
2. **Iteration 1**:
    - `mid = 0 + (3 - 0) / 2 = 1`
    - `nums[1] = 3`
    - `3 > 2` (target보다 큼) → `right = mid - 1 = 0`
3. **Iteration 2**:
    - `mid = 0 + (0 - 0) / 2 = 0`
    - `nums[0] = 1`
    - `1 < 2` (target보다 작음) → `left = mid + 1 = 1`
4. **종료**: `left(1) > right(0)` 가 되어 반복문 탈출.
5. **결과**: `left`인 **1**을 반환. (실제로 2는 1과 3 사이인 인덱스 1에 들어가야 함)

---

### 4. 코드 구현 (Swift)

```swift
class Solution {
    func searchInsert(_ nums: [Int], _ target: Int) -> Int {
        var left: Int = 0
        var right: Int = nums.count - 1
        
        while left <= right {
            let mid = left + (right - left) / 2
            
            if nums[mid] == target {
                return mid
            } else if nums[mid] > target {
                right = mid - 1
            } else {
                left = mid + 1
            }
        }
        
        return left
    }
}
```

### 5. 복잡도 분석
- **시간 복잡도**: $O(\log n)$ - 이진 탐색을 통해 매 단계마다 탐색 범위가 절반으로 줄어듭니다.
- **공간 복잡도**: $O(1)$ - 추가적인 배열이나 자료구조를 사용하지 않고 변수 몇 개만 사용합니다.

</details>

## 관련 개념
- [이진 탐색 (Binary Search)](../algorithm/search.md)
