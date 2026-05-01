# 🌐 네트워크 (Network)

네트워크 프로토콜, 계층 구조, TCP/UDP 및 보안 등 통신 전반에 관한 내용을 정리한 섹션입니다. 

<div class="card-grid">
  <a href="#/network/layer" class="topic-card">
    <div class="icon">🧱</div>
    <div class="card-content">
      <h3>계층 구조 (OSI 7 & TCP/IP)</h3>
      <p>네트워크 통신의 핵심인 OSI 7계층별 역할과 캡슐화/역캡슐화의 원리를 정리합니다.</p>
    </div>
  </a>

  <a href="#/network/tcp-vs-udp" class="topic-card">
    <div class="icon">🔌</div>
    <div class="card-content">
      <h3>TCP vs UDP</h3>
      <p>신뢰성 있는 연결과 빠른 전송의 차이점 및 활용 분야를 정리합니다.</p>
    </div>
  </a>

  <div class="topic-card placeholder">
    <div class="icon">🌐</div>
    <div class="card-content">
      <h3>HTTP / HTTPS</h3>
      <p>웹 브라우징의 기본 프로토콜과 보안 통신 원리가 곧 추가될 예정입니다.</p>
    </div>
  </div>

  <div class="topic-card placeholder">
    <div class="icon">🏷️</div>
    <div class="card-content">
      <h3>DNS (도메인 네임 시스템)</h3>
      <p>도메인 주소를 IP 주소로 변환하는 계층적 구조가 곧 추가될 예정입니다.</p>
    </div>
  </div>

  <div class="topic-card placeholder">
    <div class="icon">⚖️</div>
    <div class="card-content">
      <h3>로드 밸런싱</h3>
      <p>트래픽을 효율적으로 분산시키는 기법과 장치들이 곧 추가될 예정입니다.</p>
    </div>
  </div>

  <div class="topic-card placeholder">
    <div class="icon">🍪</div>
    <div class="card-content">
      <h3>쿠키 vs 세션</h3>
      <p>상태 비저장 프로토콜인 HTTP에서 상태를 유지하는 방법이 곧 추가될 예정입니다.</p>
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
