# 백준 1931번 - 회의실 배정

https://www.acmicpc.net/problem/1931

## 문제
한 개의 회의실이 있는데 이를 사용하고자 하는 N개의 회의에 대하여 회의실 사용표를 만들려고 한다. 각 회의 I에 대해 시작시간과 끝나는 시간이 주어져 있고, 각 회의가 겹치지 않게 하면서 회의실을 사용할 수 있는 회의의 최대 개수를 찾아보자. 단, 회의는 한번 시작하면 중간에 중단될 수 없으며 한 회의가 끝나는 것과 동시에 다음 회의가 시작될 수 있다. 회의의 시작시간과 끝나는 시간이 같을 수도 있다. 이 경우에는 시작하자마자 끝나는 것으로 생각하면 된다.

## 제한사항
|시간제한|메모리제한|
|-----|-------|
|2초|128MB|

## 입력
첫째 줄에 회의의 수 N(1 ≤ N ≤ 100,000)이 주어진다. 둘째 줄부터 N+1 줄까지 각 회의의 정보가 주어지는데 이것은 공백을 사이에 두고 회의의 시작시간과 끝나는 시간이 주어진다. 시작 시간과 끝나는 시간은 231-1보다 작거나 같은 자연수 또는 0이다.

## 출력
첫째 줄에 최대 사용할 수 있는 회의의 최대 개수를 출력한다.

## 예제

|입력|출력|
|---|---|
|11<br>1 4<br>3 5<br>0 6<br>5 7<br>3 8<br>5 9<br>6 10<br>8 11<br>8 12<br>2 13<br>12 14|4|

## 힌트
(1,4), (5,7), (8,11), (12,14) 를 이용할 수 있다.

## 풀이
<details>
<summary>
확인
</summary>

### 1. 문제 분석 및 접근
이 문제는 주어진 회의들 중에서 겹치지 않게 가장 많은 회의를 배정하는 대표적인 **활동 선택 문제(Activity Selection Problem)**다.
모든 경우의 수를 다 확인하면 시간이 오래 걸리기 때문에, **[그리디(Greedy) 알고리즘](../algorithm/greedy.md)**을 사용하여 최적해를 구해야 한다.

회의를 가장 많이 배정하기 위해서는 "회의의 소요 시간"이나 "회의의 시작 시간"이 아니라, **"회의의 종료 시간"**을 기준으로 생각해야 한다. 
가장 일찍 끝나는 회의를 선택해야 남은 빈 시간이 가장 길어지고, 그 빈 시간에 더 많은 회의를 넣을 수 있기 때문이다.

---

### 2. 핵심 알고리즘
이 문제의 핵심은 **정렬과 조건 비교**에 있다.

1. **정렬 기준 적용:**
    - 첫 번째 조건: **종료 시간이 빠른 순(오름차순)**으로 정렬한다. 가장 빨리 끝나는 회의를 먼저 잡아야 더 많은 회의를 진행할 수 있다.
    - 두 번째 조건: 종료 시간이 같다면, **시작 시간이 빠른 순(오름차순)**으로 정렬한다. 시작하자마자 바로 끝나는 회의(예: `(2, 2)`)가 있는 경우를 처리하기 위함이다.
2. **순서대로 회의 선택:**
    - 정렬된 회의 배열을 순회하며, 직전에 선택한 회의의 종료 시간보다 현재 확인 중인 회의의 시작 시간이 크거나 같으면(`>=`) 해당 회의를 선택(배정)하고 기준 종료 시간을 업데이트합니다.

---

### 3. 상세 동작 시나리오 (Dry Run)
예제 입력을 바탕으로 동작을 살펴보자.
`11`개의 회의: `[(1,4), (3,5), (0,6), (5,7), (3,8), (5,9), (6,10), (8,11), (8,12), (2,13), (12,14)]`

**정렬 결과 (종료 시간 오름차순 -> 시작 시간 오름차순):**
1. `(1, 4)`
2. `(3, 5)`
3. `(0, 6)`
4. `(5, 7)`
5. `(3, 8)`
6. `(5, 9)`
7. `(6, 10)`
8. `(8, 11)`
9. `(8, 12)`
10. `(2, 13)`
11. `(12, 14)`

**순회 및 선택 과정:**
- 초기화: `lastEndTime` = 0, 선택된 회의 개수 = 0
- 1번 `(1, 4)`: `start`(1) >= `lastEndTime`(0) ➔ **[선택]** (lastEndTime = 4, 개수 = 1)
- 2번 `(3, 5)`: `start`(3) < `lastEndTime`(4) ➔ [패스]
- 3번 `(0, 6)`: `start`(0) < `lastEndTime`(4) ➔ [패스]
- 4번 `(5, 7)`: `start`(5) >= `lastEndTime`(4) ➔ **[선택]** (lastEndTime = 7, 개수 = 2)
- 5번 `(3, 8)`: `start`(3) < `lastEndTime`(7) ➔ [패스]
- 6번 `(5, 9)`: `start`(5) < `lastEndTime`(7) ➔ [패스]
- 7번 `(6, 10)`: `start`(6) < `lastEndTime`(7) ➔ [패스]
- 8번 `(8, 11)`: `start`(8) >= `lastEndTime`(7) ➔ **[선택]** (lastEndTime = 11, 개수 = 3)
- 9번 `(8, 12)`: `start`(8) < `lastEndTime`(11) ➔ [패스]
- 10번 `(2, 13)`: `start`(2) < `lastEndTime`(11) ➔ [패스]
- 11번 `(12, 14)`: `start`(12) >= `lastEndTime`(11) ➔ **[선택]** (lastEndTime = 14, 개수 = 4)

최종적으로 총 4개의 회의를 배정하게 된다.

---

### 4. 코드 구현 (Swift)

```swift
struct Meeting {
    let start: Int
    let end: Int
}

// input
let N: Int = Int(readLine()!)!

let meetings:[Meeting] = Array(repeating: 0, count: N).map { _ in
    let line = readLine()!
    let split = line.split(separator: " ")

    return Meeting(start: Int(split[0])!, end: Int(split[1])!)
}

// solution
var availableMeetings: [Meeting] = []

let sortedMeetings: [Meeting] = meetings.sorted { meetingA, meetingB in
    if meetingA.end == meetingB.end {
        return meetingA.start < meetingB.start
    }
    return meetingA.end < meetingB.end
}

for meeting in sortedMeetings {
    guard let lastMeeting = availableMeetings.last else {
        availableMeetings.append(meeting)
        continue
    }

    if meeting.start >= lastMeeting.end {
        availableMeetings.append(meeting)
    }
}

print(availableMeetings.count)
```

### 5. 복잡도 분석
- **시간 복잡도 (Time Complexity):** 전체 배열을 정렬하는 데 `O(N log N)`의 시간이 소요된다. 이후 배열을 한 번 순회하는 데 `O(N)`의 시간이 걸린다. 제한 시간 2초 내에 N=100,000을 처리하기에 `O(N log N)`은 효율적이고 충분한 시간 복잡도이다. 따라서 총 시간 복잡도는 `O(N log N)`이다.
- **공간 복잡도 (Space Complexity):** 회의 정보를 담는 1차원 구조체 배열을 생성하므로 공간 복잡도는 `O(N)`이 된다. (정렬을 위한 추가 공간 제외) 128MB 메모리 제한 내에 10만 개의 데이터는 문제없이 들어간다.
</details>