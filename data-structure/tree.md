# 트리 (Tree)

트리는 계층적인 구조를 표현하는 비선형 자료구조이다.

---

## 1. 기본 용어 (Vocabulary)

- **Node (노드)**: 데이터를 저장하는 기본 단위
- **Root (루트)**: 노드 간을 잇는 선 (관계 표현)
- **Edge (간선)**: 트리의 최상단 노드 (탐색의 시작점)
- **Leaf (리프)**: 자식이 없는 말단 노드
- **Child / Parent (자식/부모)**: 상하 관계
- **Sibling (형제)**: 부모가 같은 노드들
- **Depth vs. Height (깊이 vs. 높이)**: 
    - Depth: 루트에서 특정 노트까지의 간선 수 (루트의 깊이 = 0)
    - Height: 특정 노드에서 가장 먼 리프까지의 간선 수 (전체 트리의 높이는 루트의 높이)

---

## 2. 이진 트리 (Binary Tree)

### 이진 트리의 종류
- **완전 이진 트리 (Complete Binary Tree)** : 왼쪽부터 빈틈없이 채워진 트리 (배열로 구현시 인덱스 계산이 용이)
- **포화 이진 트리 (Full Binary Tree)** : 모든 노드가 0개 또는 2개의 자식을 가진 트리
- **편향 이진 트리 (Skewed Binary Tree)** : 한쪽으로 노드가 쏠린 트리 (탐색 성능이 $O(n)$으로 저하)

---

## 3. 이진 탐색 트리 (Binary Search Tree, BST)

### 핵심 규칙 (Property)

데이터를 효율적으로 찾기 위해 규칙을 부여한 트리
- `왼쪽 자식 < 부모 < 오른쪽 자식`

### 연산의 시간 복잡도
- **탐색 (Search)**: $O(log n)$
- **삽입 (Insert)**: $O(log n)$
- **삭제 (Delete)**: $O(log n)$
- **최악의 경우(Worst Case)** 
    - 편향된 경우에 $O(n)$
    - 이를 해결하기 위한 자가 균형 트리가 있음
        - AVL 트리
        - Red-Black 트리

---

## 4. 트리 순회 (Tree Traversal)

아래 4가지 순회 방식의 방문 순서와 특징을 정리해 보세요.
- **전위 순회 (Pre-order)**
    - `Root -> Left -> Right`
    - 트리 복사 시 유리
- **중위 순회 (In-order)**
    - `Left -> Root -> Right`
    - BST에서 이 순회 방식이 특별함
    - 오름차순 정렬 결과 제공
- **후위 순회 (Post-order)**
    - `Left -> Right -> Root`
    - 트리 삭제, 용량 계산 시 유리
- **레벨 순회 (Level-order / BFS)**
    - 위층부터 차례대로 방문 (BFS 방식)

---

## 5. 실전 사례 및 연관 지식

- **[힙 (Heap)](./heap.md)**: 힙은 트리의 어떤 특수한 형태인가요?
- **[데이터베이스 (Database)](../database/README.md)**: 인덱스 구현에 가장 많이 쓰이는 트리 기반 자료구조는 무엇인가요? (Hint: B-Tree)
- **[그래프 (Graph)](../algorithm/graph.md)**: 트리는 '사이클이 없는 (  ) 그래프'라고 정의할 수 있습니다. 빈칸은?

---

## 관련 문제
- [LeetCode - Maximum Depth of Binary Tree](../problems/leetcode-maximum-depth-of-binary-tree.md)
- [LeetCode - Search Insert Position](../problems/leetcode-search-insert-position.md) (BST의 원리를 배열에 적용한 사례)
- [LeetCode - Valid Parentheses](../problems/leetcode-valid-parentheses.md) (트리 구조의 유효성을 검사할 때 스택이 쓰이는 이유)
