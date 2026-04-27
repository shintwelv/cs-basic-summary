# Maximum Depth of Binary Tree

## Description

Given the `root` of a binary tree, return its maximum depth.

A binary tree's **maximum depth** is the number of nodes along the longest path from the root node down to the farthest leaf node.

## Examples
### Example 1

![example 1](https://assets.leetcode.com/uploads/2020/11/26/tmp-tree.jpg)

> Input: root = [3,9,20,null,null,15,7]
> 
> Output: 3

### Example 2

> Input: root = [1,null,2]
> 
> Output: 2 

## Constraints

- The number of nodes in the tree is in the range `[0, 10^4]`.
- `-100 <= Node.val <= 100`
 
## Follow Up
- None

## Solution
## 풀이
<details>
<summary>
확인
</summary>

### 1. 문제 분석 및 접근
- **문제 목적**: 이진 트리의 루트 노드부터 가장 먼 리프 노드까지의 경로에 있는 노드의 개수(최대 깊이)를 계산한다.
- **제약 조건**: 노드 개수는 0개에서 10,000개 사이이며, 빈 트리인 경우 깊이는 0이다.
- **접근 방법**: 재귀(Recursion)를 이용한 DFS 방식을 사용한다. 왼쪽 서브트리와 오른쪽 서브트리의 최대 깊이를 각각 구한 뒤, 그 중 큰 값에 현재 노드의 깊이(1)를 더해 반환한다.
---

### 2. 핵심 알고리즘
- **DFS (Depth First Search)**: 트리의 하단까지 탐색하여 각 서브트리의 높이를 계산한다.
- **재귀 (Recursion)**: 문제를 "현재 노드의 깊이 = 1 + max(왼쪽 자식의 깊이, 오른쪽 자식의 깊이)"라는 작은 문제로 분할하여 해결한다.

---

### 3. 상세 동작 시나리오 (Dry Run)
- **입력**: `root = [3, 9, 20, null, null, 15, 7]`
1. `maxDepth(3)` 호출
   - `maxDepth(9)` 호출 -> 리프 노드이므로 `1` 반환
   - `maxDepth(20)` 호출
     - `maxDepth(15)` 호출 -> 리프 노드이므로 `1` 반환
     - `maxDepth(7)` 호출 -> 리프 노드이므로 `1` 반환
     - `max(1, 1) + 1 = 2` 반환
2. `max(1, 2) + 1 = 3` 반환
- **결과**: `3`

---

### 4. 코드 구현 (Swift)

```swift
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public var val: Int
 *     public var left: TreeNode?
 *     public var right: TreeNode?
 *     public init() { self.val = 0; self.left = nil; self.right = nil; }
 *     public init(_ val: Int) { self.val = val; self.left = nil; self.right = nil; }
 *     public init(_ val: Int, _ left: TreeNode?, _ right: TreeNode?) {
 *         self.val = val
 *         self.left = left
 *         self.right = right
 *     }
 * }
 */
class Solution {
    func maxDepth(_ root: TreeNode?) -> Int {
        // Base case: 빈 노드인 경우 깊이는 0
        guard let root = root else { return 0 }
        
        // 하위 노드가 없는 리프 노드인 경우 깊이는 1 (최적화를 위해 추가 가능)
        if root.left == nil && root.right == nil { return 1 }
        
        // 왼쪽과 오른쪽 서브트리 중 더 깊은 쪽을 선택하고 현재 노드(+1)를 더함
        return max(maxDepth(root.left), maxDepth(root.right)) + 1
    }
}
```

### 5. 복잡도 분석
- **시간 복잡도**: `O(N)`, 트리의 모든 노드를 정확히 한 번씩 방문한다.
- **공간 복잡도**: `O(H)`, 트리의 높이(`H`)만큼 재귀 호출 스택이 쌓인다. 최악의 경우(편향 트리) `O(N)`, 균형 잡힌 트리의 경우 `O(log N)`이다.

</details>

---

## 관련 개념
- [이진 트리 (Binary Tree)](../data-structure/tree.md)
- [깊이 우선 탐색 (DFS)](../algorithm/graph.md)

