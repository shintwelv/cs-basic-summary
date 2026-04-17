# Valid Parentheses

## Description

Given a string s containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
3. Every close bracket has a corresponding open bracket of the same type.

## Examples
### Example 1

> Input: s = "()"
> 
> Output: true

### Example 2

> Input: s = "()[]{}"
> 
> Output: true

### Example 3

> Input: s = "(]"
> 
> Output: false

### Example 4

> Input: s = "([])"
> 
> Output: true

### Example 5

> Input: s = "([)]"
> 
> Output: false
 
## Constraints

- 1 <= s.length <= 104
- s consists of parentheses only '()[]{}'.
 
## Follow Up
- None

## Solution
## 풀이
<details>
<summary>
확인
</summary>

### 1. 문제 분석 및 접근
- **문제 목적**: 주어진 문자열 `s`가 유효한 괄호 구성을 가지고 있는지 확인합니다.
- **제약 조건**: 
    - 열린 괄호는 반드시 같은 종류의 닫힌 괄호로 닫혀야 합니다.
    - 열린 괄호는 반드시 올바른 순서대로 닫혀야 합니다.
    - 문자열 길이는 최대 $10^4$입니다.
- **접근 방법**: 
    - 괄호는 **가장 나중에 열린 것이 가장 먼저 닫히는(LIFO)** 성질을 가집니다. 이를 효과적으로 관리하기 위해 **스택(Stack)** 자료구조를 활용합니다.
    - 여는 괄호가 나오면 스택에 쌓고, 닫는 괄호가 나오면 스택의 가장 위에 있는(가장 최근에 열린) 괄호와 짝이 맞는지 확인합니다.

---

### 2. 핵심 알고리즘
- **스택 활용**:
    1. 문자열을 순회하며 각 문자를 확인합니다.
    2. 여는 괄호(`(`, `{`, `[`)인 경우 스택에 `push`합니다.
    3. 닫는 괄호(`)`, `}`, `]`)인 경우:
        - 스택이 비어있다면 잘못된 구성입니다.
        - 스택에서 `pop`한 문자와 현재 닫는 괄호가 짝이 맞는지 확인합니다.
        - 짝이 맞지 않는다면 잘못된 구성입니다.
    4. 모든 순회가 끝난 후 스택이 완전히 비어 있어야 유효한 문자열(모든 괄호가 짝을 찾음)로 간주합니다.

---

### 3. 상세 동작 시나리오 (Dry Run)
**입력**: `s = "([])"`

1. **'('** 를 만남: 스택이 비어있으므로 스택에 추가. `Stack: ["("]`
2. **'['** 를 만남: 여는 괄호이므로 스택에 추가. `Stack: ["(", "["]`
3. **']'** 를 만남: 
    - 스택의 마지막 요소 `[`를 꺼냄(`pop`). 
    - `]`와 `[`는 짝이 맞으므로 계속 진행. `Stack: ["("]`
4. **')'** 를 만남:
    - 스택의 마지막 요소 `(`를 꺼냄.
    - `)`와 `(`는 짝이 맞으므로 계속 진행. `Stack: []`
5. **결과**: 순회 종료 후 스택이 비어 있으므로 `true` 반환.

---

### 4. 코드 구현 (Swift)

```swift
class Solution {
    func isValid(_ s: String) -> Bool {
        var stack: [String] = []

        for parentheses in s.split(separator: "").map({"\($0)"}) {
            // 스택이 비어있으면 일단 추가 (첫 글자 혹은 짝 맞추기 끝난 후)
            guard !stack.isEmpty else {
                stack.append(parentheses)
                continue
            }

            // 여는 괄호면 스택에 쌓음
            if ["(", "{", "["].contains(parentheses) {
                stack.append(parentheses)
                continue
            }

            // 닫는 괄호인 경우 가장 최근의 여는 괄호를 꺼내서 확인
            let last: String = stack.popLast()!

            // 짝이 맞으면 그대로 pop된 상태 유지 (다음으로 넘어감)
            if parentheses == ")" && last == "(" { continue }
            if parentheses == "}" && last == "{" { continue }
            if parentheses == "]" && last == "[" { continue }

            // 짝이 맞지 않으면 꺼냈던 것과 현재 것을 모두 다시 쌓음 (stack이 비지 않게 됨)
            stack.append(last)
            stack.append(parentheses)
        }

        // 모든 과정을 거친 후 스택이 비어있어야 모든 괄호의 짝이 맞은 것
        return stack.isEmpty
    }
}
```

### 5. 복잡도 분석
- **시간 복잡도**: $O(N)$
    - 문자열의 길이 $N$만큼 한 번 순회하므로 선형 시간이 소요됩니다.
- **공간 복잡도**: $O(N)$
    - 모든 문자가 여는 괄호일 경우 스택의 크기가 $N$까지 커질 수 있습니다.
    
</details>

---

## 관련 개념
- **[스택 & 큐 (Stack & Queue)](../data-structure/stack-queue.md)**: 후입선출(LIFO) 원리를 이용해 괄호의 중첩 구조를 처리하는 데 핵심이 됩니다.
- **[배열 (Array)](../data-structure/array-linkedlist.md)**: Swift에서 배열을 사용하여 동적 스택을 구현했습니다.