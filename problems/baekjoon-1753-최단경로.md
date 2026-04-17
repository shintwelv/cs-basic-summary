# 백준 1753번 - 최단경로

https://www.acmicpc.net/problem/1753

## 제한
시간제한: 1초
메모리제한: 256MB

## 문제
방향그래프가 주어지면 주어진 시작점에서 다른 모든 정점으로의 최단 경로를 구하는 프로그램을 작성하시오. 단, 모든 간선의 가중치는 10 이하의 자연수이다.

## 입력
첫째 줄에 정점의 개수 V와 간선의 개수 E가 주어진다. (1 ≤ V ≤ 20,000, 1 ≤ E ≤ 300,000) 모든 정점에는 1부터 V까지 번호가 매겨져 있다고 가정한다. 둘째 줄에는 시작 정점의 번호 K(1 ≤ K ≤ V)가 주어진다. 셋째 줄부터 E개의 줄에 걸쳐 각 간선을 나타내는 세 개의 정수 (u, v, w)가 순서대로 주어진다. 이는 u에서 v로 가는 가중치 w인 간선이 존재한다는 뜻이다. u와 v는 서로 다르며 w는 10 이하의 자연수이다. 서로 다른 두 정점 사이에 여러 개의 간선이 존재할 수도 있음에 유의한다.

## 출력
첫째 줄부터 V개의 줄에 걸쳐, i번째 줄에 i번 정점으로의 최단 경로의 경로값을 출력한다. 시작점 자신은 0으로 출력하고, 경로가 존재하지 않는 경우에는 INF를 출력하면 된다.

## 예제

|입력|출력|
|---|---|
|5 6<br>1<br>5 1 1<br>1 2 2<br>1 3 3<br>2 3 4<br>2 4 5<br>3 4 6|0<br>2<br>3<br>7<br>INF|

## 풀이
<details>
<summary>
확인
</summary>

### 1. 문제 분석 및 접근
- **유형**: 단일 출발점 최단 경로 (Single-Source Shortest Path)
- **특징**: 간선의 가중치가 10 이하의 '자연수(양수)'이므로 무조건 **[다익스트라(Dijkstra) 알고리즘](../algorithm/graph.md)** 을 사용해야 한다.
- **제한사항 파악**: 정점(V)이 20,000개, 간선(E)이 30만 개이다. 만약 최솟값을 찾기 위해 매번 전체 배열을 순회하거나 간선 목록 전체를 뒤지면 최소 $O(V \times E)$가 되어 시간 초과가 발생한다.
- **해결 접근**: 
  1. 간선을 $E$개 통으로 저장하지 않고, 출발 노드 인덱스에서 바로 이어진 간선만 뽑아 쓸 수 있도록 **인접 리스트(Adjacency List)** 로 설계한다. (**[배열 & 연결 리스트](../data-structure/array-linkedlist.md)** 구조의 차이 이해)
  2. 다음 방문할 '가장 가까운 거리의 노드'를 $O(\log E)$ 만에 찾을 수 있는 **[우선순위 큐(Min-Heap)](../data-structure/heap.md)** 를 도입한다. (Swift는 내장 우선순위 큐가 없어 직접 배열과 완전이진트리 인덱스 조작을 통해 힙을 구현해야 한다.)

---

### 2. 핵심 알고리즘
1. **최소 힙(Min Heap) 직접 구현**
   - 배열을 활용하되, 인덱스 계산의 편의를 위해 `0`번 인덱스에 쓰레기값(더미)을 넣고 루트를 `1`번 인덱스로 고정한다.
   - 부모 위치는 `i / 2`, 왼쪽 자식은 `i * 2`, 오른쪽 자식은 `i * 2 + 1`로 계산한다.
   - **Up-Heap (삽입)**: 맨 끝에 원소를 넣은 뒤, 부모가 나보다 크면 최상단까지 Swap하며 올라간다.
   - **Down-Heap (추출)**: 루트 요소를 반환 및 제거한 뒤, 마지막 요소를 루트로 올리고, 자식들 중 자신보다 '더 작고', '존재하는' 승자를 고차함수(`filter`, `sorted`)를 통해 안전하게 찾아 Swap하며 내려간다.
2. **다익스트라(Dijkstra) 탐색 최적화 (Relaxation 방어)**
   - 큐에서 `pop()`한 거리 정보가 현재 내 테이블(`routeMinCosts`)에 기록된 거리보다 크다면, 이는 과거의 구식 정보(나중에 더 짧은 경로를 찾아 이미 테이블이 갱신된 상태)이므로 불필요한 이웃 간선 탐색을 막고 `continue`를 통해 쳐낸다.

### 3. 상세 동작 시나리오 (Dry Run)
- **예제 입력**: V=5, E=6, 시작점(K)=1
- `routeMinCosts`: `[INF, INF, INF, INF, INF]` (1-based index)
- **초기화**: 1번 노드(시작점)의 거리를 0으로 만들고 우선순위 큐에 `(노드: 1, 거리: 0)`을 삽입한다.

1. **[Pop] (1, 거리 0)**
   - 1번과 연결된 간선: (1->2, 비용 2), (1->3, 비용 3)
   - `routeMinCosts[2] = 2` 갱신 후 큐에 삽입.
   - `routeMinCosts[3] = 3` 갱신 후 큐에 삽입.
2. **[Pop] (2, 거리 2)**
   - 2번과 연결된 간선: (2->3, 비용 4), (2->4, 비용 5)
   - 3번으로 가는 비용: 기존 누적(2) + 간선(4) = 6. 하지만 현재 수첩(`routeMinCosts[3]`)엔 이미 3이 적혀있어서 **갱신 안 함** (Relaxation 방어).
   - 4번으로 가는 비용: 기존 누적(2) + 간선(5) = 7. `INF > 7`이므로 `routeMinCosts[4] = 7` 갱신 후 큐에 삽입.
3. **[Pop] (3, 거리 3)**
   - 3번과 연결된 간선: (3->4, 비용 6)
   - 4번 가는 비용: 기존 누적(3) + 간선(6) = 9. 수첩 값(7)보다 크므로 **갱신 안 함**.
4. **결과 확정**: 큐가 빌 때까지 반복하여 방문 가능한 모든 지점의 최적 비용 확정. 연결되지 않은 5번 노드는 구식 `INF`로 남게 된다.

### 4. 코드 구현 (Swift)

```swift
// input
struct Edge {
    let start: Int
    let end: Int
    let cost: Int
}

typealias VertexId = Int

let firstLine: [String] = readLine()!.split(separator: " ").map {"\($0)"}

let V: Int = Int(firstLine[0])!
let E: Int = Int(firstLine[1])!

let startNode: Int = Int(readLine()!)!

var edges: [[Edge]] = Array(repeating: [], count: V+1)

Array(repeating: 0, count: E).forEach { _ in
    let line: [Int] = readLine()!.split(separator: " ").map {Int($0)!}
    edges[line[0]].append(Edge(start: line[0], end: line[1], cost: line[2]))
}

// solution
struct Node {
    let vertexId: Int
    let costToVertex: Int
}

struct PriorityQueue {
    private var list: [Node] = [Node(vertexId: -1, costToVertex: -1)]

    mutating func append(_ node: Node) {
        self.list.append(node)

        var appendedNodeIndex = self.list.count - 1

        while (appendedNodeIndex > 1) {
            let parentIndex = appendedNodeIndex / 2

            if self.list[parentIndex].costToVertex > self.list[appendedNodeIndex].costToVertex {
                self.list.swapAt(parentIndex, appendedNodeIndex)
                appendedNodeIndex = parentIndex
            } else {
                break
            }
        }
    }

    mutating func pop() -> Node? {
        guard !self.isEmpty else { return nil }
        if self.list.count == 2 { return self.list.removeLast() }

        let root: Node = self.list[1]
        self.list[1] = self.list.removeLast()

        var index: Int = 1

        while (index < self.list.count - 1) {
            let leftChildIndex = index * 2
            let rightChildIndex = index * 2 + 1

            if let minIndex: Int = [leftChildIndex, rightChildIndex]
                .filter({ $0 < self.list.count })
                .filter({ self.list[$0].costToVertex < self.list[index].costToVertex })
                .sorted(by: { return self.list[$0].costToVertex < self.list[$1].costToVertex })
                .first {
                self.list.swapAt(index, minIndex)
                index = minIndex
                continue
            }

            break
        }

        return root
    }

    var isEmpty: Bool { return self.list.count <= 1 }
}

var routeMinCosts: [Int] = Array(repeating: Int.max, count: V+1)
routeMinCosts[startNode] = 0

var queue = PriorityQueue()
queue.append(Node(vertexId: startNode, costToVertex: 0))

while (!queue.isEmpty) {
    let node: Node = queue.pop()!

    guard node.costToVertex <= routeMinCosts[node.vertexId] else { continue }

    let availableEdges: [Edge] = edges[node.vertexId]

    for edge in availableEdges {
        let costToVertex = node.costToVertex + edge.cost
        guard costToVertex < routeMinCosts[edge.end] else { continue }

        routeMinCosts[edge.end] = costToVertex
        queue.append(Node(vertexId: edge.end, costToVertex: costToVertex))
    }
}

routeMinCosts[1...V].map {
    if $0 == Int.max { return "INF" }
    return "\($0)"
}.forEach {print($0)}
```

### 5. 복잡도 분석
- **시간 복잡도**: $O(E \log V)$
  - 최악의 경우, 존재하는 모든 간선 $E$개를 한 번씩 확인하며 우선순위 큐에 데이터를 넣고 뺀다. 
  - 최소 힙(우선순위 큐)에서의 연산은 데이터 개수가 삽입되더라도 트리의 높이인 $O(\log V)$ 번 연산만 요구한다. 즉, 전체 $O(E \log V)$가 되어 1초 내에 약 30만 개의 제한을 여유롭게 통과한다.
- **공간 복잡도**: $O(V + E)$
  - 2차원 배열 크기 메모리 비용 발생. 그래프 자체를 저장하기 위한 연결 리스트(`edges`)에 최악의 경우 $E$개의 객체가 누적 할당된다.
  - 최단 거리 기록 배열 `routeMinCosts`은 V 크기 필요.
  - 메모리 사용 256MB 제한 조건은 가뿐히 해결할 수 있다.
</details>