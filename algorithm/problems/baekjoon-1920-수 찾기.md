# 백준 1920번 - 수 찾기

https://www.acmicpc.net/problem/1920

## 문제
N개의 정수 A[1], A[2], …, A[N]이 주어져 있을 때, 이 안에 X라는 정수가 존재하는지 알아내는 프로그램을 작성하시오.

## 제한사항
|시간제한|메모리제한|
|-----|-------|
|1초|128MB|

## 입력
첫째 줄에 자연수 N(1 ≤ N ≤ 100,000)이 주어진다. 다음 줄에는 N개의 정수 A[1], A[2], …, A[N]이 주어진다. 다음 줄에는 M(1 ≤ M ≤ 100,000)이 주어진다. 다음 줄에는 M개의 수들이 주어지는데, 이 수들이 A안에 존재하는지 알아내면 된다. 모든 정수의 범위는 $-2^{31}$ 보다 크거나 같고 $2^{31}$ 보다 작다.

## 출력
M개의 줄에 답을 출력한다. 존재하면 1을, 존재하지 않으면 0을 출력한다.

## 예제

|입력|출력|
|---|---|
|5<br>4 1 5 2 3<br>5<br>1 3 7 9 5|1<br>1<br>0<br>0<br>1|

## 풀이
<details>
<summary>
확인
</summary>

[정렬](../sort.md) 후 [이진탐색](../search.md)을 사용했다.

직접 구현한 Quick Sort보다 .sorted()가 더 빨랐다.

```swift
//quick sort
func quickSort(_ arr: [Int]) -> [Int] {
    guard arr.count > 1 else { return arr }
    let pivot: Int = arr.randomElement()!

    var lessThanPivot: [Int] = []
    var largerThanPivot: [Int] = []
    var equalToPivot: [Int] = []

    for value in arr {
        if value == pivot {
            equalToPivot.append(value)
            continue
        }

        if value > pivot {
            largerThanPivot.append(value)
        } else {
            lessThanPivot.append(value)
        }
    }

    return quickSort(lessThanPivot) + equalToPivot + quickSort(largerThanPivot)
}
```

```swift
// input
let n: Int = Int(readLine()!)!

let nArray: [Int] = readLine()!.split(separator: " ").map { Int($0)! }

let m: Int = Int(readLine()!)!

let mArray: [Int] = readLine()!.split(separator: " ").map { Int($0)! }

// solution
func isInArrayWithbinarySearch(sortedArray: [Int], toFind value: Int) -> Bool {
    guard sortedArray.count > 0 else { return false }

    if sortedArray.first! == value { return true }
    if sortedArray.last! == value { return true }

    var startIndex = 0
    var endIndex = sortedArray.count - 1

    while startIndex <= endIndex {
        let midIndex  = (startIndex + endIndex) / 2

        let midValue = sortedArray[midIndex]

        if value == midValue { return true }

        if value > midValue {
            startIndex = midIndex + 1
        } else {
            endIndex = midIndex - 1
        }
    }

    return false
}

let sortedNArray:[Int] = nArray.sorted()

for mValue in mArray {
    let isInNArray: Bool = isInArrayWithbinarySearch(sortedArray: sortedNArray, toFind: mValue)
    print(isInNArray ? "1" : "0")
}
```

</details>