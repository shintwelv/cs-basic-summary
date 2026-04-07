# 🏛️ 운영체제 (Operating System)

운영체제의 핵심 원리인 프로세스 관리, 메모리 전략, 자원 할당 등을 정리한 섹션입니다. 아래 카드들을 클릭하여 세부 내용을 학습해 보세요.

<div class="card-grid">
  <a href="#/operating-system/thread-vs-process" class="topic-card">
    <div class="icon">🧵</div>
    <div class="card-content">
      <h3>프로세스 vs 스레드</h3>
      <p>실행 단위의 차이점, 자원 공유 방식 및 멀티태스킹의 핵심 원리인 시분할 기법을 다룬다.</p>
    </div>
  </a>

  <a href="#/operating-system/memory-management" class="topic-card">
    <div class="icon">🧠</div>
    <div class="card-content">
      <h3>메모리 관리</h3>
      <p>가상 메모리, 페이징 기법, 단편화 해결 전략 및 LRU 알고리즘 등 주 메모리 관리 기법을 요약합니다.</p>
    </div>
  </a>

  <div class="topic-card placeholder">
    <div class="icon">⏱️</div>
    <div class="card-content">
      <h3>CPU 스케줄링</h3>
      <p>다양한 스케줄링 알고리즘(FCFS, SJF, RR 등)에 대한 내용이 곧 추가될 예정입니다.</p>
    </div>
  </div>

  <div class="topic-card placeholder">
    <div class="icon">💀</div>
    <div class="card-content">
      <h3>데드락 (Deadlock)</h3>
      <p>교착 상태의 발생 조건과 이를 해결하기 위한 예방/회피 전략이 곧 추가될 예정입니다.</p>
    </div>
  </div>

  <div class="topic-card placeholder">
    <div class="icon">🔄</div>
    <div class="card-content">
      <h3>동기화와 세마포어</h3>
      <p>경쟁 상태를 방지하기 위한 뮤텍스, 세마포어 등의 동기화 기법이 곧 추가될 예정입니다.</p>
    </div>
  </div>

  <div class="topic-card placeholder">
    <div class="icon">📂</div>
    <div class="card-content">
      <h3>파일 시스템</h3>
      <p>파일의 저장 구조, 할당 방식 및 파일 관리 시스템의 원리가 곧 추가될 예정입니다.</p>
    </div>
  </div>

  <div class="topic-card placeholder">
    <div class="icon">⚡</div>
    <div class="card-content">
      <h3>인터럽트와 시스템 콜</h3>
      <p>커널 모드 전환과 하드웨어 이벤트 처리 메커니즘이 곧 추가될 예정입니다.</p>
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
