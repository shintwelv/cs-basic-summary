# 배열 (Array) & 연결 리스트 (Linked List)

|특징|배열(Array)|연결 리스트(Linked List)|
|---|---|---|
|접근속도|매우 빠름 ($O(1)$)|느림 ($O(n)$, 하나씩 찾아야 함)|
|삽입/삭제|느림 ($O(n)$, 밀거나 당겨야 함)|빠름 ($O(1)$, 포인터만 바꾸면 됨)|
|메모리|연속된 공간 필요, 오버헤드 적음|불연속적 공간 사용, 오버헤드 큼|
|확장성|크기 고정, 재할당 시 비용 큼|크기 유연, 동적 할당으로 확장 용이|

---

## 연관 지식
- **[시간 복잡도 (Time Complexity)](../algorithm/time-space-complexity.md)**: 데이터 구조에 따른 연산 효율성 비교의 기초가 됩니다.
- **[이진 탐색 (Binary Search)](../algorithm/search.md)**: **정렬된 배열**에서의 무작위 접근(Random Access) 성능을 극대화한 알고리즘입니다.
- **[해시 테이블 (Hash Table)](../algorithm/README.md)**: 충돌 해결 전략 중 하나인 '체이닝(Chaining)' 기법에서 **연결 리스트**가 핵심적으로 사용됩니다.

## 관련 문제 풀이
- **[백준 10816 - 숫자 카드 2](../problems/baekjoon-10816-숫자카드2.md)**: 정렬된 배열과 이진 탐색을 활용한 원소 개수 세기.
- **[LeetCode - Merge Sorted Array](../problems/leetcode-merge-sorted-array.md)**: 두 개의 정렬된 배열을 제자리(in-place)에서 병합하기.
- **[LeetCode - Palindrome Number](../problems/leetcode-palindrome-number.md)**: 정수를 배열 형태로 추출하여 좌우 대칭 여부를 판별하기.
- **[백준 1753 - 최단경로](../problems/baekjoon-1753-최단경로.md)**: 인접 리스트(Adjacency List) 구조를 활용한 효율적인 그래프 저장.

