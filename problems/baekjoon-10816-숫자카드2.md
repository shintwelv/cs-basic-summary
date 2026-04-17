# 백준 10816번 - 숫자카드2

https://www.acmicpc.net/problem/10816

## 문제
숫자 카드는 정수 하나가 적혀져 있는 카드이다. 상근이는 숫자 카드 N개를 가지고 있다. 정수 M개가 주어졌을 때, 이 수가 적혀있는 숫자 카드를 상근이가 몇 개 가지고 있는지 구하는 프로그램을 작성하시오.

## 입력
첫째 줄에 상근이가 가지고 있는 숫자 카드의 개수 N(1 ≤ N ≤ 500,000)이 주어진다. 둘째 줄에는 숫자 카드에 적혀있는 정수가 주어진다. 숫자 카드에 적혀있는 수는 -10,000,000보다 크거나 같고, 10,000,000보다 작거나 같다.

셋째 줄에는 M(1 ≤ M ≤ 500,000)이 주어진다. 넷째 줄에는 상근이가 몇 개 가지고 있는 숫자 카드인지 구해야 할 M개의 정수가 주어지며, 이 수는 공백으로 구분되어져 있다. 이 수도 -10,000,000보다 크거나 같고, 10,000,000보다 작거나 같다.

## 출력
첫째 줄에 입력으로 주어진 M개의 수에 대해서, 각 수가 적힌 숫자 카드를 상근이가 몇 개 가지고 있는지를 공백으로 구분해 출력한다.

## 예제

|입력|출력|
|---|---|
|10<br>6 3 2 10 10 10 -10 -10 7 3<br>8<br>10 9 -5 2 3 4 5 -10|3 0 0 1 2 0 0 2|

## 풀이
<details>
<summary>
확인
</summary>

### 1. 문제 분석 및 접근
이 문제는 주어진 정수 **[배열(Array)](../data-structure/array-linkedlist.md)** 에서 특정 숫자가 **몇 개** 포함되어 있는지를 빠르게 찾아야 합니다.
- **단순 탐색 ($O(N \times M)$)**: 매번 처음부터 끝까지 세면 $500,000 \times 500,000$으로 시간 초과가 발생합니다.
- **이진 탐색 ($O(M \log N)$)**: 배열을 정렬한 뒤 이진 탐색을 사용하면 매우 빠르지만, 일반적인 이진 탐색은 "값이 있는지"만 알려줄 뿐 "몇 개"인지는 알려주지 않습니다.
- **해결책**: 중복된 값의 **시작점(Lower Bound)**과 **끝점(Upper Bound)**을 [이진 탐색](../algorithm/search.md)으로 찾아 그 차이를 구합니다.

---

### 2. 핵심 알고리즘: Lower Bound & Upper Bound

중복 원소가 있는 정렬된 배열에서 핵심은 `if` 조건문의 등호(`=`) 처리입니다.

#### ① Lower Bound (하한)
> 찾고자 하는 값 **이상**이 처음 나타나는 위치를 찾습니다.
- `array[mid] >= value`: 중간값이 찾으려는 값보다 **크거나 같다면**, 더 앞쪽(왼쪽)에 똑같은 값이 더 있을 수 있으므로 `end = mid`로 범위를 좁힙니다.
- 최종적으로 `start`는 타겟 값이 나타나는 **가장 첫 번째 인덱스**를 가리킵니다.

#### ② Upper Bound (상한)
> 찾고자 하는 값을 **초과**하는 값이 처음 나타나는 위치를 찾습니다.
- `array[mid] > value`: 중간값이 찾으려는 값보다 **클 때만** 범위를 왼쪽으로 좁힙니다. 
- 만약 값이 같다면(`array[mid] == value`), 더 오른쪽에 값이 더 있을 수 있으므로 `start = mid + 1`로 범위를 오른쪽으로 밀어냅니다.
- 최종적으로 `start`는 타겟 값의 **마지막 인덱스 바로 다음 칸**을 가리킵니다.

---

### 3. 상세 동작 시나리오 (Dry Run)
배열: `[1, 2, 2, 2, 3]`, 찾는 값: `2`

1. **Lower Bound 탐색**:
   - `1`이상의 첫 위치 -> 인덱스 `1` 반환
2. **Upper Bound 탐색**:
   - `2`를 초과하는(`3`이상) 첫 위치 -> 인덱스 `4` 반환
3. **개수 계산**:
   - `4 - 1 = 3` (정확히 2가 3개 있음을 확인)

> [!NOTE]
> **특이 케이스 처리**
> - **값이 없는 경우**: Lower와 Upper Bound가 동일한 위치를 가리켜 차이가 `0`이 됩니다.
> - **값이 1개인 경우**: 상한이 하한보다 딱 한 칸 뒤를 가리켜 차이가 `1`이 됩니다.

---

### 4. 코드 구현 (Swift)

```swift
import Foundation

// input
let N: Int = Int(readLine()!)!
let NArray: [Int] = readLine()!.split(separator: " ").map {Int($0)!}
let M: Int = Int(readLine()!)!
let MArray: [Int] = readLine()!.split(separator: " ").map {Int($0)!}

// solution
func lowerBound(array: [Int], value: Int) -> Int {
    var start = 0
    var end = array.count
    
    while start < end {
        let mid = (start + end) / 2
        let midValue = array[mid]
        
        if midValue >= value {
            end = mid
        } else {
            start = mid + 1
        }
    }
    return start
}

func upperBound(array: [Int], value: Int) -> Int {
    var start = 0
    var end = array.count
    
    while start < end {
        let mid = (start + end) / 2
        let midValue = array[mid]
        
        if midValue > value {
            end = mid
        } else {
            start = mid + 1
        }
    }
    return start
}

// 1. 이진 탐색을 위해 원본 배열 정렬 (O(N log N))
let sortedNArray = NArray.sorted()

// 2. 각 쿼리에 대해 이진 탐색 수행 (M * O(log N))
let results = MArray.map { target in
    let lower = lowerBound(array: sortedNArray, value: target)
    let upper = upperBound(array: sortedNArray, value: target)
    return "\(upper - lower)"
}

// 3. 결과 출력 (한 번에 합쳐서 출력하여 효율성 증대)
print(results.joined(separator: " "))
```

### 5. 복잡도 분석
- **시간 복잡도**: $O((N + M) \log N)$
  - 배열 정렬: $O(N \log N)$
  - $M$번의 이진 탐색: $O(M \log N)$
- **공간 복잡도**: $O(N)$ (정렬된 배열 저장)

</details>