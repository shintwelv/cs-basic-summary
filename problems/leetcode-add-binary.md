# Add Binary

## Description

Given two binary strings `a` and `b`, return their sum as a binary string.

## Examples
### Example 1

> Input: a = "11", b = "1"
> 
> Output: "100"

### Example 2

> Input: a = "1010", b = "1011"
> 
> Output: "10101"
 
## Constraints

- 1 <= a.length, b.length <= 10^4
- a and b consist only of `'0'` or `'1'` characters.
- Each string does not contain leading zeros except for the zero itself.

## Follow Up
- None

## Solution
## 풀이
<details>
<summary>
확인
</summary>

### 1. 문제 분석 및 접근
- **문제 목적**: 두 개의 이진수(binary) 문자열을 입력받아 그 합을 이진수 문자열로 반환합니다.
- **제약 조건**: 문자열의 길이는 최대 $10^4$로, 매우 큰 수일 수 있으므로 직접 정수형으로 변환하여 더하는 방식(`Int(a, radix: 2)`)은 오버플로우 위험이 있습니다.
- **접근 방법**: 초등 수학의 세로셈 방식과 유사하게, 각 문자열의 뒤(낮은 자릿수)에서부터 한 글자씩 숫자로 변환하여 더하고, 올림수(Carry)를 앞자리로 전달하는 방식으로 구현합니다.

---

### 2. 핵심 알고리즘
- **자릿수별 합산**: `max(a.length, b.length) + 1` 크기의 배열을 준비하여 자릿수별 합과 올림수를 관리합니다.
- **올림 처리**: 특정 자릿수의 합이 2 이상이 되면 다음 자릿수로 1을 넘겨주고 현재 자릿수는 2로 나눈 나머지값만 남깁니다.
- **결과 생성**: 배열의 첫 번째 요소(최상위 올림수)가 0인 경우 이를 제외하고 문자열로 결합합니다.

---

### 3. 상세 동작 시나리오 (Dry Run)
**입력: `a = "11", b = "1"`**
1. `aDigits = [1, 1]`, `bDigits = [1]`
2. `array = [0, 0, 0]` (결과 저장용, 1칸 여유)
3. **i = 0 (첫 번째 루프, 맨 뒷자리)**:
   - `aDigit = 1`, `bDigit = 1`
   - `sum = 2`
   - `array[2] = 0 + 2 = 2`
   - `array[2] >= 2` 이므로 `array[1] = 1`, `array[2] = 0`
   - 상태: `array = [0, 1, 0]`
4. **i = 1 (두 번째 루프)**:
   - `aDigit = 1`, `bDigit = 0` (b는 자릿수 부족)
   - `sum = 1`
   - `array[1] = 1 + 1 = 2` (이전 루프의 올림수 포함)
   - `array[1] >= 2` 이므로 `array[0] = 1`, `array[1] = 0`
   - 상태: `array = [1, 0, 0]`
5. **결과 변환**:
   - `array[0]`이 0이 아니므로 전체 포함 -> `"100"`

---

### 4. 코드 구현 (Swift)

```swift
// intentionally avoid String(_:radix:) function.

class Solution {
    func addBinary(_ a: String, _ b: String) -> String {
        let aDigits: [Int] = a.split(separator:"").map{Int($0)!}
        let bDigits: [Int] = b.split(separator:"").map{Int($0)!}
        
        var array: [Int] = Array(repeating: 0, count: max(a.count, b.count) + 1)
        
        for i in 0..<(array.count - 1) {
            let index = (array.count - 1) - i
            
            let aDigit: Int = {
                let aIndex = (aDigits.count - 1) - i
                guard aIndex >= 0 else { return 0 }
                return aDigits[aIndex]
            }()
            let bDigit: Int = {
                let bIndex = (bDigits.count - 1) - i
                guard bIndex >= 0 else { return 0 }
                return bDigits[bIndex]
            }()
            
            let sum = aDigit + bDigit
            
            array[index] = array[index] + sum
            
            if array[index] >= 2 {
                array[index - 1] = array[index - 1] + 1
                array[index] = array[index] % 2
            }
        }
        
        var result: String = ""
        
        for i in 0..<array.count {
            if i == 0 && array[i] == 0 {
                continue
            }
            result = "\(result)\(array[i])"
        }
        
        return result
    }
}
```

### 5. 복잡도 분석
- **시간 복잡도**: $O(\max(N, M))$
  - 문자열을 배열로 변환하는 데 $O(N+M)$, 자릿수만큼 루프를 도는 데 $O(\max(N, M))$이 소요됩니다.
- **공간 복잡도**: $O(\max(N, M))$
  - 입력 문자열을 배열로 변환한 `aDigits`, `bDigits`와 결과를 저장할 `array` 공간이 필요합니다.
</details>

---

## 관련 문제
- **[LeetCode - Palindrome Number](./leetcode-palindrome-number.md)**: 숫자를 문자열로 변환하지 않고 수학적 연산을 통해 처리하는 유사한 기초 문제.

---

## 관련 개념
- **[시간 및 공간 복잡도](../algorithm/time-space-complexity.md)**: 알고리즘의 효율성 분석 기법.
