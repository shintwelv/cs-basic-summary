# 🧩 문제 풀이 (Problem Solving)

알고리즘 문제들을 풀이하고 정리한 공간입니다.

<div class="problem-grid">
  <a href="#/algorithm/problems/baekjoon-2750-수정렬하기" class="problem-item">
    <div class="problem-badge">Baekjoon</div>
    <div class="problem-info">
      <h4>2750 수 정렬하기</h4>
      <p>입력된 수들을 Merge Sort를 활용하여 오름차순으로 정렬하는 기능을 구현했습니다.</p>
    </div>
    <div class="problem-footer">
      <span>Swift</span>
      <span>알고리즘</span>
    </div>
  </a>
  <a href="#/algorithm/problems/baekjoon-1920-수 찾기" class="problem-item">
    <div class="problem-badge">Baekjoon</div>
    <div class="problem-info">
      <h4>1920 수 찾기</h4>
      <p>주어진 배열에서 이분 탐색(Binary Search)을 활용하여 특정 정수의 존재 여부를 확인합니다.</p>
    </div>
    <div class="problem-footer">
      <span>Swift</span>
      <span>알고리즘</span>
    </div>
  </a>
  <a href="#/algorithm/problems/baekjoon-10816-숫자카드2" class="problem-item">
    <div class="problem-badge">Baekjoon</div>
    <div class="problem-info">
      <h4>10816 숫자 카드 2</h4>
      <p>중복 원소가 포함된 정렬 배열에서 Lower/Upper Bound를 활용해 특정 숫자의 개수를 효율적으로 계산합니다.</p>
    </div>
    <div class="problem-footer">
      <span>Swift</span>
      <span>이진 탐색</span>
    </div>
  </a>
  <a href="#/algorithm/problems/baekjoon-2839-설탕배달" class="problem-item">
    <div class="problem-badge">Baekjoon</div>
    <div class="problem-info">
      <h4>2839 설탕배달</h4>
      <p>동적 계획법(DP)을 활용하여 주어진 무게를 최소 개수의 3kg, 5kg 봉지로 나누는 방법을 계산합니다.</p>
    </div>
    <div class="problem-footer">
      <span>Swift</span>
      <span>DP</span>
    </div>
  </a>
  <a href="#/algorithm/problems/baekjoon-11399-ATM" class="problem-item">
    <div class="problem-badge">Baekjoon</div>
    <div class="problem-info">
      <h4>11399 ATM</h4>
      <p>그리디 알고리즘을 활용하여 각 사람이 돈을 인출하는 데 필요한 대기 시간의 누적합을 최소화합니다.</p>
    </div>
    <div class="problem-footer">
      <span>Swift</span>
      <span>그리디</span>
      <span>알고리즘</span>
    </div>
  </a>
  <a href="#/algorithm/problems/baekjoon-1931- 회의실 배정" class="problem-item">
    <div class="problem-badge">Baekjoon</div>
    <div class="problem-info">
      <h4>1931 회의실 배정</h4>
      <p>그리디 알고리즘을 활용하여 한 개의 회의실에서 시간이 겹치지 않게 최대한 많은 회의를 배정합니다.</p>
    </div>
    <div class="problem-footer">
      <span>Swift</span>
      <span>그리디</span>
      <span>알고리즘</span>
    </div>
  </a>
</div>

<style>
  .problem-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 20px;
    margin-top: 30px;
  }

  .problem-item {
    background: var(--search-bg);
    border: 1px solid var(--sidebar-border);
    border-radius: 16px;
    padding: 24px;
    text-decoration: none !important;
    transition: all 0.3s ease;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
  }

  .problem-item:hover {
    border-color: var(--theme-color);
    transform: translateY(-5px);
    box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
  }

  .problem-badge {
    display: inline-block;
    padding: 4px 12px;
    background: var(--blockquote-bg);
    color: var(--theme-color);
    font-size: 0.8rem;
    font-weight: 600;
    border-radius: 20px;
    margin-bottom: 16px;
    align-self: flex-start;
  }

  .problem-info h4 {
    margin: 0 0 12px 0 !important;
    font-size: 1.25rem !important;
    color: var(--text-color);
  }

  .problem-info p {
    margin: 0 !important;
    font-size: 0.95rem;
    color: var(--sidebar-text);
    line-height: 1.5;
  }

  .problem-footer {
    margin-top: 20px;
    display: flex;
    gap: 12px;
    border-top: 1px solid var(--sidebar-border);
    padding-top: 16px;
  }

  .problem-footer span {
    font-size: 0.85rem;
    color: var(--sidebar-text);
    background: var(--code-bg);
    padding: 2px 8px;
    border-radius: 4px;
  }
</style>
