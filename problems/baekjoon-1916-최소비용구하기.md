# 백준 1916번 - 최소비용 구하기

https://www.acmicpc.net/problem/1916

## 제한
시간제한: 0.5초
메모리제한: 128MB

## 문제
N개의 도시가 있다. 그리고 한 도시에서 출발하여 다른 도시에 도착하는 M개의 버스가 있다. 우리는 A번째 도시에서 B번째 도시까지 가는데 드는 버스 비용을 최소화 시키려고 한다. A번째 도시에서 B번째 도시까지 가는데 드는 최소비용을 출력하여라. 도시의 번호는 1부터 N까지이다.

## 입력
첫째 줄에 도시의 개수 N(1 ≤ N ≤ 1,000)이 주어지고 둘째 줄에는 버스의 개수 M(1 ≤ M ≤ 100,000)이 주어진다. 그리고 셋째 줄부터 M+2줄까지 다음과 같은 버스의 정보가 주어진다. 먼저 처음에는 그 버스의 출발 도시의 번호가 주어진다. 그리고 그 다음에는 도착지의 도시 번호가 주어지고 또 그 버스 비용이 주어진다. 버스 비용은 0보다 크거나 같고, 100,000보다 작은 정수이다.

그리고 M+3째 줄에는 우리가 구하고자 하는 구간 출발점의 도시번호와 도착점의 도시번호가 주어진다. 출발점에서 도착점을 갈 수 있는 경우만 입력으로 주어진다.

## 출력
첫째 줄에 출발 도시에서 도착 도시까지 가는데 드는 최소 비용을 출력한다.

## 예제

|입력|출력|
|---|---|
|5<br>8<br>1 2 2<br>1 3 3<br>1 4 1<br>1 5 10<br>2 4 2<br>3 4 1<br>3 5 1<br>4 5 3<br>1 5|4|

## 풀이
FileIO 써야한다
<details>
<summary>
확인
</summary>

### 1. 문제 분석 및 접근
- **유형**: 최단 경로 (Dijkstra)
- **이유**: 가중치가 양수인 그래프에서 특정 시작점에서 도착점까지의 최소 비용을 구하는 문제.
- **조건**: 도시 수 $N \le 1,000$, 버스 수 $M \le 100,000$. 시간 제한이 0.5초로 매우 촉박하여 효율적인 **[우선순위 큐(Heap)](../data-structure/heap.md)** 구현과 빠른 입출력이 필수.
---
### 2. 핵심 알고리즘
- **[다익스트라(Dijkstra)](../algorithm/graph.md)**: 
  - 출발지로부터 각 도시까지의 최단 거리를 무한대(`Int.max`)로 초기화.
  - 우선순위 큐에 (비용 0, 출발 도시)를 삽입.
  - 큐에서 가장 비용이 적은 노드를 꺼내 인접한 도시들의 경로를 갱신하고, 갱신된 노드들만 다시 큐에 삽입.
---
### 3. 상세 동작 시나리오 (Dry Run)
1. 시작 도시 1번을 큐에 삽입 (비용 0).
2. 1번과 연결된 2, 3, 4, 5번 도시의 비용을 확인하고 `costs` 배열 업데이트 후 큐 삽입.
3. 큐에서 가장 저렴한 도시(예: 4번)를 꺼내 해당 도시로부터 갈 수 있는 경로 재확인.
4. 도착 도시 5번에 도달할 때까지 반복.

---

### 4. 코드 구현 (Swift)

```swift
import Foundation
final class FileIO {
    private var buffer = [UInt8]()
    private var index = 0
    init() {
        buffer = Array(try! FileHandle.standardInput.readToEnd()!) + [UInt8(0)]
    }
    @inline(__always) private func read() -> UInt8 {
        defer { index += 1 }
        return buffer[index]
    }
    @inline(__always) func readInt() -> Int {
        var sum = 0
        var now = read()
        while now == 10 || now == 32 { now = read() }
        let negative = now == 45
        if negative { now = read() }
        while now >= 48 && now <= 57 {
            sum = sum * 10 + Int(now - 48)
            now = read()
        }
        return negative ? -sum : sum
    }
}
struct Node {
    let id: Int
    let cost: Int
}
struct PriorityQueue {
    private var list: [Node] = [Node(id: -1, cost: -1)]
    var isEmpty: Bool { list.count < 2 }
    
    mutating func append(_ node: Node) {
        list.append(node)
        var index = list.count - 1
        while index > 1 {
            let parentIndex = index / 2
            if list[parentIndex].cost <= list[index].cost { break }
            list.swapAt(parentIndex, index)
            index = parentIndex
        }
    }
    
    mutating func pop() -> Node? {
        if isEmpty { return nil }
        if list.count == 2 { return list.removeLast() }
        
        let root = list[1]
        list[1] = list.removeLast()
        
        var index = 1
        while index * 2 < list.count {
            let left = index * 2
            let right = index * 2 + 1
            var child = left
            
            if right < list.count && list[right].cost < list[left].cost {
                child = right
            }
            
            if list[index].cost <= list[child].cost { break }
            list.swapAt(index, child)
            index = child
        }
        return root
    }
}
let file = FileIO()
let numberOfCity = file.readInt()
let numberOfRoutes = file.readInt()
var adj = Array(repeating: [(Int, Int)](), count: numberOfCity + 1)
for _ in 0..<numberOfRoutes {
    let u = file.readInt()
    let v = file.readInt()
    let w = file.readInt()
    adj[u].append((v, w))
}
let targetStart = file.readInt()
let targetEnd = file.readInt()
var costs = Array(repeating: Int.max, count: numberOfCity + 1)
costs[targetStart] = 0
var pq = PriorityQueue()
pq.append(Node(id: targetStart, cost: 0))
while !pq.isEmpty {
    guard let node = pq.pop() else { break }
    if node.cost > costs[node.id] { continue }
    
    for (nextId, nextCost) in adj[node.id] {
        let newCost = node.cost + nextCost
        if newCost < costs[nextId] {
            costs[nextId] = newCost
            pq.append(Node(id: nextId, cost: newCost))
        }
    }
}
print(costs[targetEnd])
```

### 5. 복잡도 분석
- **시간 복잡도**: $O(M \log N)$
  - 큐에 삽입 및 삭제 연산은 $O(\log N)$이며, 이를 최대 간선 수 $M$만큼 반복함.
- **공간 복잡도**: $O(N + M)$
  - 인접 리스트와 거리 배열 저장 공간.
</details>