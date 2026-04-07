# 🗄️ 데이터베이스 (Database)

데이터의 효율적인 저장, 관리 및 설계 원칙(SQL/NoSQL, Index, ACID 등)을 정리한 섹션입니다. 아래 카드를 통해 주요 개념을 학습하실 수 있습니다.

<div class="card-grid">
  <div class="topic-card placeholder">
    <div class="icon">📊</div>
    <div class="card-content">
      <h3>계층 및 데이터 모델</h3>
      <p>관계형 모델의 핵심 구성 요소와 특징이 곧 추가될 예정입니다.</p>
    </div>
  </div>

  <div class="topic-card placeholder">
    <div class="icon">📜</div>
    <div class="card-content">
      <h3>SQL (질의어)</h3>
      <p>SELECT, JOIN 등 주요 SQL 문법과 최적화 방법이 곧 추가될 예정입니다.</p>
    </div>
  </div>

  <div class="topic-card placeholder">
    <div class="icon">🚀</div>
    <div class="card-content">
      <h3>인덱스 (Index)</h3>
      <p>B-Tree 구조와 효율적인 검색을 위한 인덱싱 전략이 곧 추가될 예정입니다.</p>
    </div>
  </div>

  <div class="topic-card placeholder">
    <div class="icon">🔒</div>
    <div class="card-content">
      <h3>트랜잭션과 ACID</h3>
      <p>데이터의 정규성과 일관성을 보장하는 핵심 원칙이 곧 추가될 예정입니다.</p>
    </div>
  </div>

  <div class="topic-card placeholder">
    <div class="icon">📐</div>
    <div class="card-content">
      <h3>표준화 (Normalization)</h3>
      <p>중복을 제거하고 구조를 최적화하는 단계별 과정이 곧 추가될 예정입니다.</p>
    </div>
  </div>

  <div class="topic-card placeholder">
    <div class="icon">🔄</div>
    <div class="card-content">
      <h3>NoSQL vs RDBMS</h3>
      <p>비정형 데이터 처리와 분산 환경을 위한 NoSQL의 특징이 곧 추가될 예정입니다.</p>
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
