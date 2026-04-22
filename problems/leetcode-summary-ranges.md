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
- **문제 목적**: 정렬된 고유 정수 배열을 가장 적은 수의 범위(range) 리스트로 요약하는 것입니다.
- **제약 조건**: 
    - 배열은 오름차순으로 정렬되어 있습니다.
    - 모든 숫자는 유일합니다.
- **접근 방법**: 
    - 단일 순회(O(n))를 통해 연속된 숫자인지 확인합니다.
    - 현재 숫자와 이전 숫자의 차이가 1보다 크면 연속성이 끊긴 것으로 판단하여 지금까지의 범위를 결과에 추가합니다.

---

### 2. 핵심 알고리즘
- **단일 순회 (One Pass)**: 배열의 요소를 차례대로 검사하며 범위를 생성합니다.
- **포인터 관리**: 범위의 시작점을 기록하는 변수(`start`)를 사용하여 각 범위의 시작과 끝을 추적합니다.

---

### 3. 상세 동작 시나리오 (Dry Run)
- **Input**: `nums = [0,1,2,4,5,7]`
  1. `i = 0`: `start = 0`.
  2. `i = 1`: `nums[1] - nums[0] = 1`. 연속됨.
  3. `i = 2`: `nums[2] - nums[1] = 1`. 연속됨.
  4. `i = 3`: `nums[3] - nums[2] = 2 > 1`. 연속성 끊김.
     - `start(0) != i-1(2)` 이므로 `"0->2"`를 결과에 추가.
     - `start = 3`으로 갱신.
  5. `i = 4`: `nums[4] - nums[3] = 1`. 연속됨.
  6. `i = 5`: `nums[5] - nums[4] = 2 > 1`. 연속성 끊김.
     - `start(3) != i-1(4)` 이므로 `"4->5"`를 결과에 추가.
     - `start = 5`으로 갱신.
  7. **루프 종료 후 마지막 처리**:
     - `start(5) == nums.count-1(5)` 이므로 `"7"`을 결과에 추가.
- **최종 출력**: `["0->2", "4->5", "7"]`

---

### 4. 코드 구현 (Swift)

```swift
class Solution {
    func summaryRanges(_ nums: [Int]) -> [String] {
        guard !nums.isEmpty else { return [] }

        var result: [String] = []

        var start: Int = 0

        for i in 0..<nums.count {
            let diff: Int = {
                if i == 0 { return 0 }
                return nums[i] - nums[i-1]
            }()

            if diff > 1 {
                if start == i-1 {
                    result.append("\(nums[start])")
                } else {
                    result.append("\(nums[start])->\(nums[i-1])")
                }
                start = i
            }
        }

        if start == nums.count-1 {
            result.append("\(nums[start])")
        } else {
            result.append("\(nums[start])->\(nums[nums.count-1])")
        }

        return result
    }
}
```

### 5. 복잡도 분석
- **시간 복잡도**: $O(n)$ - 배열의 모든 요소를 정확히 한 번씩 순회합니다.
- **공간 복잡도**: $O(1)$ - 결과 리스트를 저장하기 위한 공간을 제외하면 추가적인 메모리 사용은 상수가 됩니다.
    
</details>

---

## 관련 문제
- **[LeetCode - Merge Sorted Array](./leetcode-merge-sorted-array.md)**: 배열을 한 번 순회하며 두 정렬된 배열을 합치는 효율적인 포인터 활용 문제.
- **[LeetCode - Valid Palindrome](./leetcode-valid-palindrome.md)**: 문자열의 양 끝에서 중심 방향으로 이동하며 비교하는 포인터 활용 문제.

## 관련 개념
- **[배열 (Array) & 연결 리스트 (Linked List)](../data-structure/array-linkedlist.md)**: 정렬된 배열의 인덱스 접근과 연속성 판단.
- **[시간 및 공간 복잡도 (Time & Space Complexity)](../algorithm/time-space-complexity.md)**: 단일 순회($O(N)$)와 추가 메모리 미사용($O(1)$)의 효율성 분석.
