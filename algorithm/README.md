# ⚡ 알고리즘 (Algorithm)

문제 해결을 위한 효율적인 단계적 절차인 정렬, 검색, 동적 계획법 등을 정리한 섹션입니다. 

<div class="card-grid">
  <div class="topic-card placeholder">
    <div class="icon">⏱️</div>
    <div class="card-content">
      <h3>시간 및 공간 복잡도</h3>
      <p>Big-O 표기법과 알고리즘의 효율성 분석 기법이 곧 추가될 예정입니다.</p>
    </div>
  </div>

  <a href="#/algorithm/sort" class="topic-card">
    <div class="icon">📊</div>
    <div class="card-content">
      <h3>정렬 알고리즘</h3>
      <p>Quick, Merge, Heap Sort 등 주요 정렬 방식의 원리와 시간 복잡도를 정리했습니다.</p>
    </div>
  </a>

  <div class="topic-card placeholder">
    <div class="icon">🔎</div>
    <div class="card-content">
      <h3>검색 알고리즘</h3>
      <p>이진 탐색 및 다양한 탐색 기법의 구현 방법이 곧 추가될 예정입니다.</p>
    </div>
  </div>

  <div class="topic-card placeholder">
    <div class="icon">💡</div>
    <div class="card-content">
      <h3>동적 계획법 (DP)</h3>
      <p>최적 부분 구조와 중복되는 부분 문제를 해결하는 방법이 곧 추가될 예정입니다.</p>
    </div>
  </div>

  <div class="topic-card placeholder">
    <div class="icon">🎯</div>
    <div class="card-content">
      <h3>그리디 알고리즘</h3>
      <p>매 순간의 최선의 선택이 전체 최적해로 이어지는 원리가 곧 추가될 예정입니다.</p>
    </div>
  </div>

  <div class="topic-card placeholder">
    <div class="icon">🕸️</div>
    <div class="card-content">
      <h3>그래프 알고리즘</h3>
      <p>DFS, BFS, 다익스트라 등 그래프 탐색 및 최단 경로 알고리즘이 곧 추가될 예정입니다.</p>
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
