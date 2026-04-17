# 🧱 자료구조 (Data Structure)

데이터를 효율적으로 저장하고 관리하는 방법인 스택, 큐, 트리, 그래프 등을 정리한 섹션입니다. 

<div class="card-grid">
  <a href="#/data-structure/array-linkedlist" class="topic-card">
    <div class="icon">🔗</div>
    <div class="card-content">
      <h3>배열 & 연결 리스트</h3>
      <p>연속된 메모리와 노드 구조의 차이점 및 장단점을 정리했습니다.</p>
    </div>
  </a>

  <a href="#/data-structure/stack-queue" class="topic-card">
    <div class="icon">📚</div>
    <div class="card-content">
      <h3>스택 & 큐</h3>
      <p>LIFO와 FIFO 구조의 원리와 활용 사례를 정리했습니다.</p>
    </div>
  </a>

  <div class="topic-card placeholder">
    <div class="icon">🔑</div>
    <div class="card-content">
      <h3>해시 테이블</h3>
      <p>키-값 쌍의 저장 원리와 충돌 해결 전략이 곧 추가될 예정입니다.</p>
    </div>
  </div>

  <div class="topic-card placeholder">
    <div class="icon">🌳</div>
    <div class="card-content">
      <h3>트리</h3>
      <p>이진 탐색 트리, AVL, Red-Black 트리 등 계층 구조가 곧 추가될 예정입니다.</p>
    </div>
  </div>

  <a href="#/data-structure/heap" class="topic-card">
    <div class="icon">🔝</div>
    <div class="card-content">
      <h3>힙 & 우선순위 큐</h3>
      <p>최댓값/최솟값을 빠르게 찾기 위한 완전 이진 트리 기반 자료구조를 정리했습니다.</p>
    </div>
  </a>

  <div class="topic-card placeholder">
    <div class="icon">🕸️</div>
    <div class="card-content">
      <h3>그래프</h3>
      <p>정점과 간선으로 이루어진 관계 표현 및 저장 방식이 곧 추가될 예정입니다.</p>
    </div>
  </div>
</div>

<style>
  .card-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 20px;
    margin-top: 30px;
  }

  .topic-card {
    background: var(--search-bg);
    border: 1px solid var(--sidebar-border);
    border-radius: 16px;
    padding: 24px;
    text-decoration: none !important;
    transition: all 0.3s ease;
    display: flex;
    flex-direction: column;
    box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
    position: relative;
    overflow: hidden;
  }

  .topic-card:not(.placeholder):hover {
    transform: translateY(-5px);
    border-color: var(--theme-color);
    box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
  }

  .topic-card::before {
    content: '';
    position: absolute;
    left: 0;
    top: 0;
    height: 100%;
    width: 4px;
    background: var(--theme-color);
    opacity: 0.8;
  }

  .topic-card .icon {
    font-size: 2rem;
    margin-bottom: 12px;
  }

  .topic-card h3 {
    margin: 0 0 8px 0 !important;
    font-size: 1.25rem !important;
    color: var(--text-color);
  }

  .topic-card p {
    margin: 0 !important;
    font-size: 0.95rem;
    color: var(--sidebar-text);
    line-height: 1.5;
  }

  .placeholder {
    opacity: 0.6;
    cursor: default;
  }
</style>
