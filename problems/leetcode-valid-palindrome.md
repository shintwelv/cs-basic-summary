# Valid Palindrome

## Description

A phrase is a **palindrome** if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string `s`, return `true` if it is a **_palindrome_**, or `false` otherwise.

## Examples
### Example 1

> Input: s = "A man, a plan, a canal: Panama"
>
> Output: true
>
> Explanation: "amanaplanacanalpanama" is a palindrome.

### Example 2

> Input: s = "race a car"
> 
> Output: false
> 
> Explanation: "raceacar" is not a palindrome.

### Example 3

> Input: s = " "
> 
> Output: true
> 
> Explanation: s is an empty string "" after removing non-alphanumeric characters.
> 
> Since an empty string reads the same forward and backward, it is a palindrome.
 

## Constraints

- `1 <= s.length <= 2 * 10^5`
- `s` consists only of printable ASCII characters.
 
## Follow Up
- None

## Solution
## 풀이
<details>
<summary>
확인
</summary>

### 1. 문제 분석 및 접근
- **문제 목적**: 주어진 문자열에서 알파벳(A-Z, a-z)과 숫자(0-9)만 남기고 대소문자를 통일했을 때, 앞에서부터 읽으나 뒤에서부터 읽으나 동일한 '팰린드롬' 문자열인지 확인합니다.
- **제약 조건**: 문자열의 길이는 최대 $2 \times 10^5$ 입니다.
- **접근 방법**: 
    1. **필터링**: 문자열의 각 문자를 확인하여 알파벳이나 숫자인 경우에만 소문자로 변환하여 별도의 리스트에 담습니다.
    2. **대칭 확인**: 필터링된 리스트의 양쪽 끝에서부터 중앙으로 오면서 문자가 일치하는지 비교합니다. (투 포인터 방식의 변형)

---

### 2. 핵심 알고리즘
- **문자 정제**: `isAlphanumeric` 판별 로직을 사용하여 불필요한 문자를 걸러내고 모든 문자를 소문자로 표준화합니다.
- **팰린드롬 검사**: `0`번 인덱스부터 `letters.count - 1`까지 순회하며 `i`번째 문자와 `letters.count - 1 - i`번째 문자를 비교합니다. 하나라도 일치하지 않으면 즉시 `false`를 반환합니다.

---

### 3. 상세 동작 시나리오 (Dry Run)
- **입력**: `s = "race a car"`
- **1단계 (필터링)**: 
    - `r`, `a`, `c`, `e` 추출
    - ` ` (공백) 무시
    - `a` 추출
    - ` ` (공백) 무시
    - `c`, `a`, `r` 추출
    - 정제된 결과: `["r", "a", "c", "e", "a", "c", "a", "r"]`
- **2단계 (대칭 확인)**:
    - `index 0 ('r')` vs `index 7 ('r')` -> 일치
    - `index 1 ('a')` vs `index 6 ('a')` -> 일치
    - `index 2 ('c')` vs `index 5 ('c')` -> 일치
    - `index 3 ('e')` vs `index 4 ('a')` -> **불일치!**
- **결과**: `false` 반환

---

### 4. 코드 구현 (Swift)

```swift
class Solution {
    private static let numerics: [String] = "0123456789".split(separator: "").map {"\($0)"}
    
    private static let alphabets: [String] = "abcdefghijklmnopqrstuvwxyz".split(separator: "").map {"\($0)"}
    
    private static let alphanumerics: [String] = [
        Solution.numerics,
        Solution.alphabets
    ].flatMap {$0}
    
    func isPalindrome(_ s: String) -> Bool {
        let letters: [String] = s.split(separator: "").compactMap { Solution.alphanumerics.contains("\($0)".lowercased()) ? "\($0)".lowercased() : nil }

        for i in 0..<letters.count {
            if letters[i] != letters[letters.count - 1 - i] {
                return false
            }
        }
        
        return true
    }
}
```

### 5. 복잡도 분석
- **시간 복잡도**: $O(N)$
    - 문자열 전체를 한 번 순회하여 Alphanumeric 문자를 가려내는 데 $O(N)$이 걸립니다.
    - 추출된 문자들이 팰린드롬인지 확인하기 위해 최대 $N$번 비교하므로 $O(N)$입니다.
- **공간 복잡도**: $O(N)$
    - 필터링된 문자들을 저장하기 위해 원본 문자열 길이에 비례하는 추가적인 배열(`letters`)을 생성합니다.

</details>

---

## 관련 문제
- **[LeetCode - Palindrome Number](./leetcode-palindrome-number.md)**: 정수를 문자열로 변환하지 않고 수학적 연산을 통해 팰린드롬 여부를 판별하는 문제입니다.
- **[LeetCode - Summary Ranges](./leetcode-summary-ranges.md)**: 정렬된 배열을 한 번의 순회로 처리하는 효율적인 배열 탐색 문제입니다.

## 관련 개념
- **투 포인터 (Two Pointers)**: 배열의 양끝에서 중심 방향으로 비교 수행

