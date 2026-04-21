# Ransom Note

## Description

Given two strings `ransomNote` and `magazine`, return true if `ransomNote` can be constructed by using the letters from `magazine` and `false` otherwise.

Each letter in `magazine` can only be used once in `ransomNote`.

## Examples
### Example 1

> Input: ransomNote = "a", magazine = "b"
> 
> Output: false

### Example 2

> Input: ransomNote = "aa", magazine = "ab"
> 
> Output: false

### Example 3

> Input: ransomNote = "aa", magazine = "aab"
> 
> Output: true
 
## Constraints

- 1 <= ransomNote.length, magazine.length <= 105
- ransomNote and magazine consist of lowercase English letters.

## Follow Up
- None

## Solution
## 풀이
<details>
<summary>
확인
</summary>

### 1. 문제 분석 및 접근

주어진 `ransomNote`를 `magazine`에 있는 문자들로 구성할 수 있는지 확인하는 문제입니다. 핵심은 각 문자의 **출현 빈도(Frequency)**를 비교하는 것입니다.

- `magazine`의 각 문자는 한 번만 사용할 수 있습니다.
- 따라서 `ransomNote`에 포함된 각 문자의 개수가 `magazine`에 포함된 해당 문자의 개수보다 작거나 같아야 합니다.
- 영문 소문자로만 구성되어 있으므로, 해시 테이블(Dictionary)이나 크기 26의 배열을 사용하여 각 문자의 개수를 저장하고 비교하는 방식으로 접근할 수 있습니다.

---

### 2. 핵심 알고리즘

- **해시 테이블(Hash Table/Dictionary)**: 각 문자열의 문자별 빈도수를 저장하기 위해 `[String: Int]` 형태의 딕셔너리를 사용합니다.
- **빈도 비교**: `ransomNote`의 모든 문자에 대해, `magazine`에서의 출현 빈도가 충분한지 확인합니다. 만약 특정 문자가 `magazine`에 없거나 개수가 부족하면 `false`를 반환합니다.

---

### 3. 상세 동작 시나리오 (Dry Run)

**예제 3: `ransomNote = "aa", magazine = "aab"`**

1.  **`ransomNote` 빈도 계산**:
    - 'a'가 2번 나타납니다. `ransomNoteCharacterTable = ["a": 2]`
2.  **`magazine` 빈도 계산**:
    - 'a'가 2번, 'b'가 1번 나타납니다. `magazineCharacterTable = ["a": 2, "b": 1]`
3.  **빈도 비교**:
    - `ransomNote`의 'a' (2개) vs `magazine`의 'a' (2개) -> `2 >= 2` (충분함)
4.  모든 조건을 만족하므로 `true`를 반환합니다.

---

### 4. 코드 구현 (Swift)

```swift
class Solution {
    func canConstruct(_ ransomNote: String, _ magazine: String) -> Bool {
        var ransomNoteCharacterTable: [String: Int] = [:]
        var magazineCharacterTable: [String: Int] = [:]
        
        for s in ransomNote {
            guard let value = ransomNoteCharacterTable["\(s)"] else {
                ransomNoteCharacterTable["\(s)"] = 1
                continue
            }
            
            ransomNoteCharacterTable["\(s)"] = value + 1
        }
        
        for s in magazine {
            guard let value = magazineCharacterTable["\(s)"] else {
                magazineCharacterTable["\(s)"] = 1
                continue
            }
            
            magazineCharacterTable["\(s)"] = value + 1
        }
        
        for key in ransomNoteCharacterTable.keys {
            guard let occurenceInMagazine = magazineCharacterTable[key] else {
                return false
            }
            
            guard occurenceInMagazine >= ransomNoteCharacterTable[key]! else {
                return false
            }
        }
        
        return true
    }
}
```

### 5. 복잡도 분석
- **시간 복잡도**: $O(N + M)$
    - $N$은 `ransomNote`의 길이, $M$은 `magazine`의 길이입니다. 두 문자열을 각각 한 번씩 순회하며 빈도수를 계산하고, 딕셔너리의 키(최대 26개)를 순회하므로 선형 시간 복잡도를 가집니다.
- **공간 복잡도**: $O(1)$ (또는 $O(K)$)
    - 알파벳 소문자만 사용하므로 딕셔너리의 최대 크기는 26으로 제한됩니다. 입력 크기에 관계없이 일정한 공간을 사용하므로 상수 공간 복잡도로 볼 수 있습니다.
    
</details>

---

## 관련 개념
- [Hash Table](../data-structure/hash-table.md)
- [시간 및 공간 복잡도](../algorithm/time-space-complexity.md)

## 추천 관련 문제
- [Baekjoon 10816 - 숫자카드2](./baekjoon-10816-숫자카드2.md)
- [Baekjoon 1920 - 수 찾기](./baekjoon-1920-수%20찾기.md)
