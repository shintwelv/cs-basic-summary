# 백준 2750번 - 수 정렬하기

https://www.acmicpc.net/problem/2750

## 문제
N개의 수가 주어졌을 때, 이를 오름차순으로 정렬하는 프로그램을 작성하시오.

## 입력
첫째 줄에 수의 개수 N(1 ≤ N ≤ 1,000)이 주어진다. 둘째 줄부터 N개의 줄에는 수가 주어진다. 이 수는 절댓값이 1,000보다 작거나 같은 정수이다. 수는 중복되지 않는다.

## 출력
첫째 줄부터 N개의 줄에 오름차순으로 정렬한 결과를 한 줄에 하나씩 출력한다.

## 예제

|입력|출력|
|---|---|
|5<br>5<br>2<br>3<br>4<br>1|1<br>2<br>3<br>4<br>5|

## 풀이
<details>
<summary>
확인
</summary>

[Quick Sort](../algorithm/sort.md)를 사용했다

```swift
import Foundation

// parse input
let lineSize: Int = Int(readLine()!)!

var inputArray: [Int] = []

for _ in 0..<lineSize {
    inputArray.append(Int(readLine()!)!)
}

// merge sort
func mergeSort(_ arr: [Int]) -> [Int] {
    guard arr.count > 1 else { return arr }
    
    let pivot: Int = arr.randomElement()!
    
    var valuesSmallerThanPivot: [Int] = []
    var valuesLargerThanPivot: [Int] = []
    
    for value in arr {
        guard value != pivot else { continue }
        
        if value > pivot {
            valuesLargerThanPivot.append(value)
        } else {
            valuesSmallerThanPivot.append(value)
        }
    }
    
    return [
        mergeSort(valuesSmallerThanPivot),
        [pivot],
        mergeSort(valuesLargerThanPivot)
    ].flatMap {$0}
}

let mergedSort: [Int] = mergeSort(inputArray)

for value in mergedSort {
    print(value)
}
```

</details>