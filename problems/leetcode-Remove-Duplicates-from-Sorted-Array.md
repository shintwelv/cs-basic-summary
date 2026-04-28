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
- **유형**: **[배열](../data-structure/array-linkedlist.md)**, **투 포인터 (Two Pointers)**, **[시간 및 공간 복잡도](../algorithm/time-space-complexity.md)**
- **정렬된 배열**: 입력 배열 `nums`가 이미 오름차순으로 정렬되어 있다는 점이 핵심입니다.
- **인접한 중복**: 정렬된 상태에서는 중복된 숫자들이 항상 서로 이웃하게 배치됩니다.
- **In-place 수정**: 추가적인 배열을 생성하지 않고(O(1) Space), 주어진 배열 `nums`를 직접 수정하여 고유한 값들을 앞쪽으로 몰아야 합니다.
- **기존 코드의 문제점**: 
    - `uniques`라는 별도의 배열을 생성하여 메모리를 추가로 사용함 (O(N) 공간 복잡도).
    - `uniques.contains()` 메서드를 호출할 때마다 매번 배열을 검색하므로 성능이 저하됨 (O(N^2) 시간 복잡도).


---

### 2. 핵심 알고리즘
- **투 포인터(Two Pointers)** 기법을 사용합니다.
    - `i` (Slow Pointer): 마지막으로 확인된 고유한 요소의 인덱스를 유지합니다.
    - `j` (Fast Pointer): 배열의 두 번째 요소부터 끝까지 순회하며 새로운 고유 요소를 찾습니다.
- **로직**:
    1. `nums[j]`가 `nums[i]`와 다르면, 이는 새로운 고유 요소를 발견한 것입니다.
    2. `i`를 1 증가시킵니다.
    3. `nums[i]` 위치에 `nums[j]` 값을 덮어씌웁니다.
    4. 최종적으로 고유 요소의 개수는 `i + 1`이 됩니다.

---

### 3. 상세 동작 시나리오 (Dry Run)
- **Input**: `nums = [1, 1, 2]`
    1. `i = 0`, `j = 1` 시작.
    2. `nums[1](1) == nums[0](1)` 이므로 무시.
    3. `j = 2` 이동. `nums[2](2) != nums[0](1)` 이므로 새로운 고유 요소 발견.
    4. `i = 1`로 증가, `nums[1] = nums[2]` 수행 -> `nums = [1, 2, 2]`
    5. 반복 종료. `i + 1 = 2` 반환.
- **Input**: `nums = [0, 0, 1, 1, 2]`
    1. `i = 0`, `j = 1`: `nums[1]==nums[0]` (Pass)
    2. `i = 0`, `j = 2`: `nums[2]!=nums[0]` -> `i=1`, `nums[1]=1` -> `[0, 1, 1, 1, 2]`
    3. `i = 1`, `j = 3`: `nums[3]==nums[1]` (Pass)
    4. `i = 1`, `j = 4`: `nums[4]!=nums[1]` -> `i=2`, `nums[2]=2` -> `[0, 1, 2, 1, 2]`
    5. `i + 1 = 3` 반환.

---

### 4. 코드 구현 (Swift)

```swift
// old
class Solution {
    func removeDuplicates(_ nums: inout [Int]) -> Int {
        var appearedNumbers: Set<Int> = []
        
        for i in 0..<nums.count {
            let number = nums[i]
            
            if appearedNumbers.contains(number) {
                nums[i] = Int.max
                continue
            }
            
            appearedNumbers.insert(number)
        }
        
        nums.sort()
        
        return appearedNumbers.count
    }
}
// new
class Solution {
    func removeDuplicates(_ nums: inout [Int]) -> Int {
        // 빈 배열 예외 처리
        if nums.isEmpty { return 0 }
        
        // i: 고유한 값이 들어갈 위치를 가리키는 포인터
        var i = 0
        
        // j: 배열 전체를 훑는 포인터
        for j in 1..<nums.count {
            // 현재 값(nums[j])이 마지막 고유값(nums[i])과 다르면 새로운 고유값 발견
            if nums[j] != nums[i] {
                i += 1
                nums[i] = nums[j]
            }
        }
        
        // 개수는 인덱스 + 1
        return i + 1
    }
}
```

### 5. 복잡도 분석
- **시간 복잡도**: **O(N)**
    - 배열을 단 한 번만 순회(`j` 포인터)하므로 요소 개수에 비례하는 시간이 소요됩니다.
- **공간 복잡도**: **O(1)**
    - 입력 배열 외에 추가적인 배열이나 자료구조를 사용하지 않고, 오직 인덱스 변수(`i`, `j`)만 사용합니다.

</details>

---

## 관련 문제
- [LeetCode - Remove Element](leetcode-remove-element.md)
- [LeetCode - Merge Sorted Array](leetcode-merge-sorted-array.md)
- [LeetCode - Valid Palindrome](leetcode-valid-palindrome.md): 투 포인터 기법을 활용한 대칭 확인 문제.
- [LeetCode - Palindrome Number](leetcode-palindrome-number.md): 수학적 연산과 투 포인터 개념을 활용한 숫자 대칭 판별 문제.

## 관련 개념
- [배열 & 연결 리스트](../data-structure/array-linkedlist.md)
- [시간 및 공간 복잡도](../algorithm/time-space-complexity.md)

