# Palindrome Number

## Description

Given an integer `x`, return `true` if `x` is a palindrome, and `false` otherwise.

## Examples
### Example 1

> Input: x = 121
> 
> Output: true
> 
> Explanation: 121 reads as 121 from left to right and from right to left.

### Example 2

> Input: x = -121
> 
> Output: false
> 
> Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.

### Example 3

> Input: x = 10
> 
> Output: false
> 
> Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
 
## Constraints

- -2^31 <= x <= 2^31 - 1
 
## Follow Up
- Could you solve it without converting the integer to a string?

## Solution
## 풀이
<details>
<summary>
확인
</summary>

### 1. 문제 분석 및 접근
- **문제 목적**: 주어진 정수 `x`가 좌우 대칭(Palindrome)인지 확인합니다.
- **제약 조건**: 
    - 음수는 `-` 부호 때문에 대칭이 될 수 없으므로 항상 `false`입니다.
    - 정수 범위를 고려해야 하며, 문자열 변환 없이 풀이하는 것이 권장됩니다.
- **접근 방법**: 
    - 정수를 10으로 나눈 나머지(`%`)를 통해 각 자릿수를 추출합니다.
    - 추출된 자릿수들을 배열에 저장한 뒤, 양끝에서부터 비교하며 대칭 여부를 확인합니다.

---

### 2. 핵심 알고리즘
- **자릿수 추출**: `while` 루프 내에서 `x % 10`을 사용하여 일의 자리부터 순차적으로 추출합니다.
- **대칭 검사**: 배열의 양쪽 끝 포인터를 좁혀가며(Two Pointers 개념) 값이 같은지 확인합니다.

---

### 3. 상세 동작 시나리오 (Dry Run)
- **입력**: `x = 121`
    1. `121 % 10 = 1`, 배열 `[1]` 저장, `x = 12`
    2. `12 % 10 = 2`, 배열 `[1, 2]` 저장, `x = 1`
    3. `1 % 10 = 1`, 배열 `[1, 2, 1]` 저장, `x = 0` (종료)
    4. 배열 `[1, 2, 1]`의 0번 인덱스(`1`)와 2번 인덱스(`1`) 비교 -> 일치
    5. 비교 종료 -> `true` 반환

---

### 4. 코드 구현 (Swift)

```swift
import Foundation

class Solution {
    func isPalindrome(_ x: Int) -> Bool {
        guard x >= 0 else { return false }
        if x == 0 { return true }

        var copyX: Int = x

        var digits: [Int] = []

        while copyX > 0 {
            let remainder = copyX % 10

            digits.append(remainder)
            copyX -= remainder
            copyX /= 10
        }

        for i in 0..<(digits.count / 2) {
            if digits[i] != digits[digits.count - 1 - i] { return false }
        }

        return true
    }
}
```

### 5. 복잡도 분석
- **시간 복잡도**: $O(\log_{10} n)$ - 정수의 자릿수만큼 연산이 수행됩니다.
- **공간 복잡도**: $O(\log_{10} n)$ - 자릿수를 저장하기 위한 배열 공간이 필요합니다.
    
</details>

---

## 관련 문제
- **[LeetCode - Valid Palindrome](./leetcode-valid-palindrome.md)**: 문자열을 정제하고 두 포인터를 사용하여 팰린드롬을 판별하는 또 다른 대표 문제입니다.

## 관련 개념
- **[배열 (Array)](../data-structure/array-linkedlist.md)**: 추출된 자릿수를 저장하고 관리하기 위한 선형 자료구조
- **[시간 및 공간 복잡도](../algorithm/time-space-complexity.md)**: 알고리즘의 효율성 분석
- **수학 (Math)**: 나머지 연산과 나누기 연산을 통한 자릿수 추출
- **투 포인터 (Two Pointers)**: 배열의 양끝에서 중심 방향으로 비교 수행
