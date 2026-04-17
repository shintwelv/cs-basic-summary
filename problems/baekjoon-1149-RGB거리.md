# 백준 1149번 - RGB거리

https://www.acmicpc.net/problem/1149

## 제한
시간제한: 0.5초
메모리제한: 128MB

## 문제
RGB거리에는 집이 N개 있다. 거리는 선분으로 나타낼 수 있고, 1번 집부터 N번 집이 순서대로 있다.

집은 빨강, 초록, 파랑 중 하나의 색으로 칠해야 한다. 각각의 집을 빨강, 초록, 파랑으로 칠하는 비용이 주어졌을 때, 아래 규칙을 만족하면서 모든 집을 칠하는 비용의 최솟값을 구해보자.

- 1번 집의 색은 2번 집의 색과 같지 않아야 한다.
- N번 집의 색은 N-1번 집의 색과 같지 않아야 한다.
- i(2 ≤ i ≤ N-1)번 집의 색은 i-1번, i+1번 집의 색과 같지 않아야 한다.

## 입력
첫째 줄에 집의 수 N(2 ≤ N ≤ 1,000)이 주어진다. 둘째 줄부터 N개의 줄에는 각 집을 빨강, 초록, 파랑으로 칠하는 비용이 1번 집부터 한 줄에 하나씩 주어진다. 집을 칠하는 비용은 1,000보다 작거나 같은 자연수이다.

## 출력
첫째 줄에 모든 집을 칠하는 비용의 최솟값을 출력한다.

## 예제

|입력|출력|
|---|---|
|3<br>26 40 83<br>49 60 57<br>13 89 99<br>|96|
|3<br>1 100 100<br>100 1 100<br>100 100 1|3|
|3<br>1 100 100<br>100 100 100<br>1 100 100<br>|102|
|8<br>71 39 44<br>32 83 55<br>51 37 63<br>89 29 100<br>83 58 11<br>65 13 15<br>47 25 29<br>60 66 19|253|

## 풀이
<details>
<summary>
확인
</summary>

### 1. 문제 분석 및 접근
이 문제는 $N$개의 집을 빨강, 초록, 파랑 중 하나의 색으로 칠할 때의 최소 비용을 구하는 문제다. 
핵심 조건은 **"인접한 두 집의 색이 같으면 안 된다"** 는 것이다.
순간순간 가장 적은 비용의 색을 선택하는 그리디(Greedy) 방식은 미래의 선택에 악영향을 미칠 수 있어 적합하지 않다. 반면, $i$번째 집의 색이 결정되었을 때 이전 $i-1$번째 집의 상태에만 영향을 받는 **최적 부분 구조(Optimal Substructure)** 를 가지므로 **[동적 계획법(Dynamic Programming, DP)](../algorithm/dp.md)** 으로 접근하는 것이 가장 효율적이다.

---

### 2. 핵심 알고리즘
- **상태의 정의**: $i$번째 집까지 칠했을 때의 색상별 최소 누적 비용을 배열 `costs[i]` (DP 테이블)에 기록하며 구한다.
- **점화식**: 현재 집을 특정 색으로 칠하기 위해서는 직전 집이 다른 두 가지 색 중 하나로 칠해져 있어야 한다.
  - $i$번째 집을 **빨강**으로 칠할 때 = `min(i-1번째 초록 비용, i-1번째 파랑 비용)` + 현재 집의 빨강 비용
  - $i$번째 집을 **초록**으로 칠할 때 = `min(i-1번째 빨강 비용, i-1번째 파랑 비용)` + 현재 집의 초록 비용
  - $i$번째 집을 **파랑**으로 칠할 때 = `min(i-1번째 빨강 비용, i-1번째 초록 비용)` + 현재 집의 파랑 비용
- **초기 상태**: `costs[0]`은 첫 번째 집 요소 그대로의 비용으로 시작한다.
- **최종 정답**: 마지막 $N-1$번째 구간에서 도출된 빨강, 초록, 파랑 누적 비용 중 최솟값을 구한다.

---

### 3. 상세 동작 시나리오 (Dry Run)

**예제 입력 1번 기준:**
```text
3
26 40 83
49 60 57
13 89 99
```

- **i = 0 (1번 집)**
  - `costs[0] = [Red: 26, Green: 40, Blue: 83]`

- **i = 1 (2번 집)**
  - Red(49) 선택 시: 직전 최솟값 `min(Green: 40, Blue: 83)` $\rightarrow 40 + 49 =$ **89**
  - Green(60) 선택 시: 직전 최솟값 `min(Red: 26, Blue: 83)` $\rightarrow 26 + 60 =$ **86**
  - Blue(57) 선택 시: 직전 최솟값 `min(Red: 26, Green: 40)` $\rightarrow 26 + 57 =$ **83**
  - `costs[1] = [Red: 89, Green: 86, Blue: 83]`

- **i = 2 (3번 집)**
  - Red(13) 선택 시: 직전 최솟값 `min(Green: 86, Blue: 83)` $\rightarrow 83 + 13 =$ **96**
  - Green(89) 선택 시: 직전 최솟값 `min(Red: 89, Blue: 83)` $\rightarrow 83 + 89 =$ **172**
  - Blue(99) 선택 시: 직전 최솟값 `min(Red: 89, Green: 86)` $\rightarrow 86 + 99 =$ **185**
  - `costs[2] = [Red: 96, Green: 172, Blue: 185]`

- **결과**
  - 마지막 3번 집까지 칠했을 때의 누적 비용 중 최솟값인 **96**이 도출된다.

---

### 4. 코드 구현 (Swift)

```swift
struct Cost {
    let red: Int
    let green: Int
    let blue: Int

    var min: Int {
        [red, green, blue].min()!
    }
}

struct House {
    let id: Int
    let cost: Cost
}

// input
let N: Int = Int(readLine()!)!

let houses: [House] = Array(repeating: 0, count: N).enumerated().map { index, _ in
    let line: [Int] = readLine()!.split(separator: " ").map { Int($0)! }

    return House(
        id: index,
        cost: Cost (
            red: line[0],
            green: line[1],
            blue: line[2]
        )
    )
}

// solution
enum HouseColor {
    case red
    case green
    case blue
}

var costs: [Cost] = Array(repeating: Cost(red: Int.max, green: Int.max, blue: Int.max), count: N)

costs[0] = houses[0].cost

for i in 1..<N {
    let house = houses[i]
    let accumulatedCost = costs[i-1]

    let redCost: Int = min(
        accumulatedCost.green,
        accumulatedCost.blue
    ) + house.cost.red

    let greenCost: Int = min(
        accumulatedCost.red,
        accumulatedCost.blue
    ) + house.cost.green

    let blueCost: Int = min(
        accumulatedCost.red,
        accumulatedCost.green
    ) + house.cost.blue

    costs[i] = Cost(
        red: redCost,
        green: greenCost,
        blue: blueCost
    )
}

print(costs[N-1].min)
```

### 5. 복잡도 분석
- **시간 복잡도**: $O(N)$
  - 1번 집부터 $N$번 집까지 1번의 루프(Loop)만 수행하며, 루프 내부의 연산은 덧셈과 최솟값 비교이므로 $O(1)$ 이다. 따라서 전체 시간 복잡도는 배열 크기에 비례하는 $O(N)$ 단위이며 0.5초의 시간 제한 안에 넉넉히 들어간다.
- **공간 복잡도**: $O(N)$
  - $N$개의 집에 대한 누적 비용을 저장하기 위한 `costs` 배열이 필요하므로 $O(N)$ 메모리를 사용한다. (배열을 할당하지 않고 직전 DP값 1개만 기억하게 한다면 $O(1)$ 공간 복잡도로도 최적화가 가능하다.)
</details>