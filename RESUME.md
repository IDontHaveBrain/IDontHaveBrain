# 조남준 &nbsp;|&nbsp; 백엔드 개발자

<style>
/* 드롭다운 컨텐츠를 위한 스타일 */
details {
  border-radius: 8px;
  margin-bottom: 12px;
  transition: all 0.3s ease;
}

details[open] {
  background-color: #f9f9f9;
  padding: 12px;
  border-left: 4px solid #3f51b5;
  box-shadow: 0 2px 5px rgba(0,0,0,0.1);
}

details > summary {
  padding: 8px;
  font-weight: bold;
  cursor: pointer;
  color: #3f51b5;
  list-style: none;
  position: relative;
  padding-left: 24px;
}

details > summary::before {
  content: "▶";
  position: absolute;
  left: 0;
  color: #3f51b5;
  font-size: 14px;
  transition: transform 0.3s ease;
}

details[open] > summary::before {
  content: "▼";
}

details > summary:hover {
  background-color: #f0f0f0;
  border-radius: 4px;
}

details ul {
  margin-top: 10px;
  padding-left: 20px;
}

details p {
  margin-bottom: 8px;
  line-height: 1.5;
}

/* 인쇄용 스타일 */
@media print {
  /* 인쇄 시 모든 details 요소를 강제로 펼침 */
  details {
    display: block;
  }
  
  details > summary {
    display: none; /* 요약 부분 숨김 */
  }
  
  details > * {
    display: block !important; /* 내부 콘텐츠 강제 표시 */
  }
  
  details[open] {
    background-color: #f9f9f9 !important;
    padding: 10px;
    margin-bottom: 15px;
    border-left: 4px solid #3f51b5 !important;
    box-shadow: none; /* 인쇄 시 그림자 제거 */
  }
  
  /* 페이지 설정 */
  @page {
    size: A4;
    margin: 1cm;
  }
  
  /* 불필요한 요소 숨김 */
  summary::before {
    display: none;
  }
  
  /* 프로젝트 섹션 간 페이지 구분 방지 */
  div[style*="border-left"] {
    page-break-inside: avoid;
  }
  
  /* 일부 섹션은 새 페이지에서 시작 */
  h2 {
    page-break-before: auto;
    page-break-after: avoid;
  }
  
  /* 링크 색상 유지 */
  a {
    color: #3f51b5 !important;
    text-decoration: none;
  }
  
  /* 배경색 강제 적용 */
  div[style*="border-left"] {
    -webkit-print-color-adjust: exact !important;
    print-color-adjust: exact !important;
  }
}
</style>

<script>
// 인쇄 시작 전에 모든 details 요소를 자동으로 펼치는 함수
window.addEventListener('beforeprint', function() {
  // 모든 details 요소를 찾아서 open 속성 추가
  const allDetails = document.querySelectorAll('details');
  allDetails.forEach(function(details) {
    // 현재 상태 저장 (나중에 복원하기 위해)
    details.dataset.wasOpen = details.hasAttribute('open');
    // 강제로 펼치기
    details.setAttribute('open', 'true');
  });
});

// 인쇄 완료 후 원래 상태로 복원 (선택적)
window.addEventListener('afterprint', function() {
  // 모든 details 요소를 찾아서 원래 상태로 복원
  const allDetails = document.querySelectorAll('details');
  allDetails.forEach(function(details) {
    // 원래 닫혀 있었으면 다시 닫기
    if (details.dataset.wasOpen === 'false' || !details.dataset.wasOpen) {
      details.removeAttribute('open');
    }
    // 임시 데이터 속성 제거
    delete details.dataset.wasOpen;
  });
});

// 페이지 로드 시 details 요소를 직접 열어볼 수 있도록 
// 'PDF로 저장하기' 버튼 추가
document.addEventListener('DOMContentLoaded', function() {
  const btnContainer = document.createElement('div');
  btnContainer.style.textAlign = 'center';
  btnContainer.style.margin = '20px 0';
  
  const expandBtn = document.createElement('button');
  expandBtn.textContent = '모든 섹션 펼치기';
  expandBtn.style.padding = '8px 15px';
  expandBtn.style.marginRight = '10px';
  expandBtn.style.backgroundColor = '#3f51b5';
  expandBtn.style.color = 'white';
  expandBtn.style.border = 'none';
  expandBtn.style.borderRadius = '4px';
  expandBtn.style.cursor = 'pointer';
  
  const collapseBtn = document.createElement('button');
  collapseBtn.textContent = '모든 섹션 접기';
  collapseBtn.style.padding = '8px 15px';
  collapseBtn.style.marginRight = '10px';
  collapseBtn.style.backgroundColor = '#9e9e9e';
  collapseBtn.style.color = 'white';
  collapseBtn.style.border = 'none';
  collapseBtn.style.borderRadius = '4px';
  collapseBtn.style.cursor = 'pointer';
  
  const printBtn = document.createElement('button');
  printBtn.textContent = 'PDF로 저장하기';
  printBtn.style.padding = '8px 15px';
  printBtn.style.backgroundColor = '#4CAF50';
  printBtn.style.color = 'white';
  printBtn.style.border = 'none';
  printBtn.style.borderRadius = '4px';
  printBtn.style.cursor = 'pointer';
  
  // 이벤트 리스너 추가
  expandBtn.addEventListener('click', function() {
    document.querySelectorAll('details').forEach(function(detail) {
      detail.setAttribute('open', 'true');
    });
  });
  
  collapseBtn.addEventListener('click', function() {
    document.querySelectorAll('details').forEach(function(detail) {
      detail.removeAttribute('open');
    });
  });
  
  printBtn.addEventListener('click', function() {
    window.print();
  });
  
  btnContainer.appendChild(expandBtn);
  btnContainer.appendChild(collapseBtn);
  btnContainer.appendChild(printBtn);
  
  // 제목 바로 아래에 버튼 추가
  const titleElement = document.querySelector('h1') || document.querySelector('#조남준-백엔드-개발자');
  if (titleElement && titleElement.parentNode) {
    titleElement.parentNode.insertBefore(btnContainer, titleElement.nextSibling);
  } else {
    document.body.insertBefore(btnContainer, document.body.firstChild);
  }
});
</script>

[![Email](https://img.shields.io/badge/Email-jonamjun.dev%40gmail.com-blue?style=for-the-badge&logo=gmail)](mailto:jonamjun.dev@gmail.com)
[![Phone](https://img.shields.io/badge/Phone-%2B821051264634-green?style=for-the-badge&logo=whatsapp)](tel:+821051264634)
[![GitHub](https://img.shields.io/badge/GitHub-IDontHaveBrain-181717?style=for-the-badge&logo=github)](https://github.com/IDontHaveBrain)

<p><i>💡 복잡한 기술적 문제 해결과 시스템 설계에 열정을 가진 백엔드 개발자 💡</i></p>

---

## 💼 소개

**분산 시스템 설계와 레거시 현대화에 깊은 관심을 가진 백엔드 개발자**입니다. 기술적 도전을 즐기며 가독성, 확장성, 유지보수성을 고려한 코드 작성을 추구합니다.

**Java, Spring, JPA 기반 백엔드 개발**에 전문성을 쌓아가고 있으며, 주니어 개발자로서 레거시 시스템 현대화 프로젝트를 적극적으로 주도하고 아키텍처 설계에 참여한 경험을 통해 빠르게 성장하고 있습니다.

<table>
  <tr>
    <td width="25%" align="center"><b>🔧 Java/Spring 백엔드 설계</b><br><small>백엔드 아키텍처 설계 주도 경험</small></td>
    <td width="25%" align="center"><b>🔄 시스템 현대화</b><br><small>레거시 시스템 재설계 및 구현</small></td>
    <td width="25%" align="center"><b>🔍 문제 해결</b><br><small>복잡한 기술적 문제 식별 및 해결</small></td>
    <td width="25%" align="center"><b>📚 빠른 적응력</b><br><small>새로운 기술 스택 빠른 습득 및 적용</small></td>
  </tr>
</table>

---

## 🛠️ 기술 스택

<table>
  <tr>
    <td><b>핵심 전문 분야</b></td>
    <td>
      <img src="https://img.shields.io/badge/Java-ED8B00?style=flat-square&logo=openjdk&logoColor=white" alt="Java" />
      <img src="https://img.shields.io/badge/Spring-6DB33F?style=flat-square&logo=spring&logoColor=white" alt="Spring" />
      <img src="https://img.shields.io/badge/Spring_Boot-6DB33F?style=flat-square&logo=spring-boot&logoColor=white" alt="Spring Boot" />
      <img src="https://img.shields.io/badge/JPA-007396?style=flat-square&logo=hibernate&logoColor=white" alt="JPA" />
    </td>
  </tr>
  <tr>
    <td><b>프로그래밍 언어</b></td>
    <td>
      <img src="https://img.shields.io/badge/Java-ED8B00?style=flat-square&logo=openjdk&logoColor=white" alt="Java" />
      <img src="https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black" alt="JavaScript" />
      <img src="https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white" alt="TypeScript" />
      <img src="https://img.shields.io/badge/Kotlin-7F52FF?style=flat-square&logo=kotlin&logoColor=white" alt="Kotlin" />
    </td>
  </tr>
  <tr>
    <td><b>프레임워크</b></td>
    <td>
      <img src="https://img.shields.io/badge/Spring_Boot-6DB33F?style=flat-square&logo=spring-boot&logoColor=white" alt="Spring Boot" />
      <img src="https://img.shields.io/badge/React-61DAFB?style=flat-square&logo=react&logoColor=black" alt="React" />
      <img src="https://img.shields.io/badge/Vue.js-4FC08D?style=flat-square&logo=vue.js&logoColor=white" alt="Vue.js" />
      <img src="https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=node.js&logoColor=white" alt="Node.js" />
      <img src="https://img.shields.io/badge/Express-000000?style=flat-square&logo=express&logoColor=white" alt="Express" />
    </td>
  </tr>
  <tr>
    <td><b>데이터베이스 & ORM</b></td>
    <td>
      <img src="https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white" alt="MySQL" />
      <img src="https://img.shields.io/badge/PostgreSQL-336791?style=flat-square&logo=postgresql&logoColor=white" alt="PostgreSQL" />
      <img src="https://img.shields.io/badge/DynamoDB-4053D6?style=flat-square&logo=amazon-dynamodb&logoColor=white" alt="DynamoDB" />
      <img src="https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white" alt="Redis" />
      <img src="https://img.shields.io/badge/JPA-007396?style=flat-square&logo=hibernate&logoColor=white" alt="JPA" />
      <img src="https://img.shields.io/badge/QueryDsl-0769AD?style=flat-square&logoColor=white" alt="QueryDsl" />
      <img src="https://img.shields.io/badge/Mybatis-000000?style=flat-square&logoColor=white" alt="Mybatis" />
    </td>
  </tr>
  <tr>
    <td><b>인프라/DevOps</b></td>
    <td>
      <img src="https://img.shields.io/badge/AWS-232F3E?style=flat-square&logo=amazon-aws&logoColor=white" alt="AWS" />
      <img src="https://img.shields.io/badge/NCloud-03C75A?style=flat-square&logoColor=white" alt="NCloud" />
      <img src="https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white" alt="Docker" />
      <img src="https://img.shields.io/badge/Jenkins-D24939?style=flat-square&logo=jenkins&logoColor=white" alt="Jenkins" />
      <img src="https://img.shields.io/badge/GitHub_Actions-2088FF?style=flat-square&logo=github-actions&logoColor=white" alt="GitHub Actions" />
      <img src="https://img.shields.io/badge/Kubernetes-326CE5?style=flat-square&logo=kubernetes&logoColor=white" alt="Kubernetes" />
    </td>
  </tr>
  <tr>
    <td><b>통신/메시징</b></td>
    <td>
      <img src="https://img.shields.io/badge/RabbitMQ-FF6600?style=flat-square&logo=rabbitmq&logoColor=white" alt="RabbitMQ" />
      <img src="https://img.shields.io/badge/REST_API-009688?style=flat-square&logo=fastapi&logoColor=white" alt="REST API" />
      <img src="https://img.shields.io/badge/SSE-CC6699?style=flat-square&logoColor=white" alt="SSE" />
    </td>
  </tr>
</table>

---

## 👨‍💻 경력

### 🏢 주식회사 현대벤디스
**기술개발팀 백엔드파트** | *2024.09 - 현재 재직중*  
**팀 구성:** 백엔드 6명, DevOps 2명, 프론트엔드 3명, 앱 4명

<div style="border-left: 4px solid #4CAF50; padding-left: 15px; margin-bottom: 20px;">
<h4>🚀 서버 메모리 개선 (2024.11)</h4>

<table style="margin-bottom: 15px;">
  <tr>
    <td align="center"><h3>📊 30%</h3><small>누적 메모리 사용량 감소</small></td>
    <td align="center"><h3>📊 20%</h3><small>피크타임 메모리 사용량 감소</small></td>
    <td align="center"><h3>📊 40%</h3><small>API 응답시간 개선</small></td>
  </tr>
</table>

<details>
<summary><b>주요 역할 및 해결 과제</b></summary>
<b>성능 병목 분석:</b> Datadog을 활용하여 응답 시간이 5초 이상 지연되는 API 패턴 분석 및 메모리 사용량 상관관계 발견

<b>문제 식별 및 해결:</b> 특정 Annotation을 조건으로 빈번하게 수행되는 AOP 로직에서 InputStream 사용 후 close 처리 누락을 확인

<b>리팩토링 주도:</b> try-with-resources 구문으로 close 처리 자동화 리팩토링 구현 및 적용

<b>사용자 경험 개선:</b> 응답 시간 개선으로 앱 사용성 향상 및 사용자 만족도 증가에 기여
</details>
</div>

---

### 🏢 에스큐아이소프트(주)
*2022.10 - 2024.09*

<div style="border-left: 4px solid #2196F3; padding-left: 15px; margin-bottom: 20px;">
<h4>🚀 Eliga Order(B2B 카페, 식당 키오스크 솔루션) 차세대 (2024.03 - 2024.09)</h4>
<p><code>Java</code> <code>Spring Boot</code> <code>PostgreSQL</code> <code>Docker</code> <code>K8S</code> <code>Redis</code><br>
<b>팀 구성:</b> 백엔드 4명, 데이터 마이그레이션 1명, 프론트 3명, 앱 3명</p>

<b>핵심 성과:</b>
<ul>
<li>🏗️ 서버리스/NoSQL 기반 레거시에서 현대적 아키텍처로 재설계</li>
<li>🔄 멀티테넌시 아키텍처 도입으로 고객별 독립 배포 환경 구축</li>
<li>⚙️ Github Action, Jenkins, Docker, K8S 기반 CI/CD 파이프라인 구축</li>
</ul>

<details>
<summary><b>주요 역할 및 도전 과제</b></summary>

<p><b>아키텍처 설계 주도:</b> 주니어지만 시스템 아키텍처 설계를 적극적으로 주도하고 기술 스택 의사결정 과정을 이끔</p>

<p><b>레거시 시스템 문제점 식별:</b></p>
<ul>
<li>Node.js, Express, AWS Lambda, DynamoDB 기반 시스템의 유지보수 어려움 분석</li>
<li>로깅 시스템 미흡으로 인한 문제 추적 한계 발견</li>
<li>설계 없이 급하게 개발된 데이터 구조의 복잡성 파악</li>
</ul>

<p><b>기술 스택 선택 및 이유:</b></p>
<ul>
<li><b>Java & Spring Boot:</b> 풍부한 생태계와 개발자 수급 용이성, 견고한 엔터프라이즈 기능 지원을 위해 선택</li>
<li><b>PostgreSQL:</b> NoSQL에서 RDB로 전환하여 데이터 무결성 강화 및 개발자 친화적 환경 제공</li>
<li><b>Docker:</b> 환경 일관성 보장 및 12시간 이내 On-premise 배포 요구사항 충족 가능성</li>
<li><b>Kubernetes:</b> 서비스 이중화, 무중단 배포, 멀티테넌시 지원, 중앙집중식 로깅 환경 구축을 위해 도입</li>
<li><b>Redis:</b> 세션 관리 및 캐싱으로 NoSQL→RDB 전환 과정에서의 성능 최적화를 위해 활용</li>
<li><b>NCloud:</b> AWS 대비 비용 효율성과 국내 서비스 특성상 지원 용이성 고려</li>
</ul>

<p><b>설계 및 구현:</b></p>
<ul>
<li>ERD 설계부터 전체 시스템 아키텍처 구성까지 전 과정 주도적 참여</li>
<li>멀티테넌시 아키텍처 설계로 고객사별 독립 환경 제공하는 시스템 구축</li>
<li>Docker 컨테이너화 및 K8S 배포 파이프라인 설계 및 구현</li>
<li>중앙화된 로깅 시스템 구축으로 문제 추적 용이성 확보</li>
</ul>

<p><b>기술적 도전 및 성장:</b></p>
<ul>
<li>서버리스에서 컨테이너 기반 아키텍처로 전환 경험</li>
<li>분산 시스템 설계 원칙과 멀티테넌시 아키텍처 구현 역량 습득</li>
<li>주니어 개발자로서 전체 아키텍처 설계 경험을 통한 기술적 시야 확장</li>
</ul>
</details>
</div>

<div style="border-left: 4px solid #2196F3; padding-left: 15px; margin-bottom: 20px;">
<h4>📌 CSIOS (카시아 속초 호텔 통합관리 시스템) 구축 (2023.09 - 2024.05)</h4>
<p><code>React</code> <code>TypeScript</code> <code>Spring</code> <code>JPA</code> <code>RabbitMQ</code> <code>Redis</code> <code>Docker</code><br>
<b>팀 구성:</b> 백엔드 2명, 풀스택 2명, 프론트 2명, APP 1명, 기획자 1명</p>

<b>핵심 성과:</b>
<ul>
<li>📦 분산된 코어 로직을 멀티모듈, Git 서브레파지토리로 통합하여 재사용성 극대화</li>
<li>🔐 JPA @Convert 기능을 활용한 DB 개인정보 암복호화 구현</li>
<li>🚀 Spring Boot 2.4.x에서 2.7.x로 마이그레이션 성공</li>
</ul>

<details>
<summary><b>주요 역할 및 해결 과제</b></summary>

<p><b>풀스택 개발:</b> 8인 팀 중 풀스택 개발 및 CI/CD, 인프라 담당</p>

<p><b>코드 통합 및 관리:</b></p>
<ul>
<li>여러 서버에 분산된 코어 로직을 식별하고 중복 코드 문제점 발견</li>
<li>멀티모듈 아키텍처와 Git 서브레파지토리로 재구성하여 코드 재사용성 및 유지보수성 개선</li>
</ul>

<p><b>통신 아키텍처 설계:</b></p>
<ul>
<li>HTTP 기반 동기 통신의 문제점(장애 전파, 높은 결합도)을 인식하고 개선 방향 제시</li>
<li>OAuth 서버 중심의 JWT 토큰 인증 체계로 보안 강화</li>
<li>RabbitMQ 기반 이벤트 주도 아키텍처를 도입하여 시스템 안정성 향상</li>
</ul>

<p><b>아키텍처 설계 및 구현:</b><br>
MSA 기반 6개 서버 구성 환경 설계 및 구현</p>
<ul>
<li>Account Management Server: 사용자 계정 및 권한 관리</li>
<li>Authorization Server: 인증 및 토큰 관리 전담</li>
<li>Batch Server: 예약 업무 및 주기적 작업 처리</li>
<li>Contents Management Server: 호텔 콘텐츠 및 상품 관리</li>
<li>Member Management Server: 호텔 회원 정보 관리</li>
<li>Interface Server: 외부 시스템 연동 전담</li>
</ul>

<p><b>기술적 도전 및 학습:</b></p>
<ul>
<li>멀티모듈 아키텍처 설계와 모듈 간 의존성 관리 방법 습득</li>
<li>Spring Boot 버전 마이그레이션 과정에서 변경된 API와 의존성 충돌 해결</li>
<li>메시지 기반 비동기 아키텍처의 장단점과 구현 패턴 학습</li>
</ul>
</details>
</div>

<div style="border-left: 4px solid #2196F3; padding-left: 15px; margin-bottom: 20px;">
<h4>📌 Eliga Order (B2B 카페, 식당 키오스크) 고도화 (2023.05 - 2023.08)</h4>
<p><code>React</code> <code>TypeScript</code> <code>Electron</code> <code>DynamoDB</code> <code>AWS Lambda</code> <code>NeDB</code><br>
<b>팀 구성:</b> 키오스크 1명, 앱 1명, 백오피스 1명</p>

<b>핵심 성과:</b>
<ul>
<li>💯 월 3~4회 발생하던 중복결제 이슈 <b>100% 해결</b></li>
<li>🔄 오프라인 환경에서도 RFID 기반 결제 지원 및 서버 재연결 시 동기화 구현</li>
</ul>

<details>
<summary><b>주요 역할 및 해결 과제</b></summary>

<p><b>결제 모듈 문제 분석 및 해결:</b></p>
<ul>
<li>중복결제 발생 원인을 결제 프로세스의 동시성 제어 부재로 식별</li>
<li>결제 프로세스에 로직적 Lock 체크를 구현하여 중복 트랜잭션 방지</li>
</ul>

<p><b>트러블슈팅 주도:</b></p>
<ul>
<li>C++ 작성 Van 연동 모듈에 상세 로그 추가하여 문제 식별</li>
<li>로그 분석을 통해 네트워크 지연 시 결제 상태 추적 불가 문제 발견</li>
</ul>

<p><b>오프라인 결제 시스템 설계:</b></p>
<ul>
<li>NeDB를 활용한 키오스크 로컬 주문기록 저장소 설계 및 개발</li>
<li>네트워크 재연결 시 서버와 자동 동기화 메커니즘 구현</li>
</ul>

<p><b>기술적 도전 및 학습:</b></p>
<ul>
<li>결제 시스템의 동시성 제어 및 장애 대응 패턴 습득</li>
<li>온/오프라인 데이터 동기화 전략 및 개발</li>
<li>Electron 애플리케이션 아키텍처 개선 및 성능 최적화 경험</li>
</ul>
</details>
</div>

<div style="border-left: 4px solid #2196F3; padding-left: 15px; margin-bottom: 20px;">
<h4>📌 KT All In Safety 고도화 (2023.04 - 2023.05)</h4>
<p><code>Vue</code> <code>Spring</code> <code>Mybatis</code><br>
<b>팀 구성:</b> 프론트 2명, 백엔드 3명</p>

<b>핵심 성과:</b>
<ul>
<li>🔐 프론트-백엔드 통신간 민감정보(로그인시 비밀번호 등) RSA 암호화 구현</li>
<li>🔑 KT LDAP 연동 로그인 구현으로 기업 내부 인증 시스템과의 원활한 통합</li>
</ul>

<details>
<summary><b>주요 역할 및 해결 과제</b></summary>

<p><b>보안 취약점 식별 및 개선:</b> 민감정보 평문 전송의 위험성을 인식하고 RSA 암호화 도입</p>
<p><b>인증 시스템 설계:</b> 기업 LDAP 기반 인증 체계와 애플리케이션 연동 아키텍처 설계</p>
<p><b>기술적 도전 및 학습:</b> 비대칭 암호화 알고리즘의 실무 적용 및 엔터프라이즈 인증 시스템 통합 경험</p>
</details>
</div>

<div style="border-left: 4px solid #2196F3; padding-left: 15px; margin-bottom: 20px;">
<h4>📌 KT ITMS 고도화 (2022.10 - 2023.03)</h4>
<p><code>Spring</code> <code>Mybatis</code> <code>Oracle</code> <code>JSP</code><br>
<b>팀 구성:</b> 풀스택 개발자 4명</p>

<b>핵심 성과:</b>
<ul>
<li>📊 10초 이상 소요되던 대형 쿼리 실행 시간을 <b>1초 이내로 단축</b> (90% 이상 개선)</li>
<li>🔄 서블릿 기반 레거시 시스템을 Spring 프레임워크로 성공적 마이그레이션</li>
<li>🔗 KT사내 업무 통합문서함과 API 연동 개발로 업무 효율성 증대</li>
</ul>

<details>
<summary><b>주요 역할 및 해결 과제</b></summary>

<p><b>성능 병목 분석 및 해결:</b></p>
<ul>
<li>1000줄 이상 대형 쿼리의 실행 지연(10초+) 문제 분석</li>
<li>단순 쿼리 최적화(Union → Join 변환)로 초기 개선 시도</li>
<li>업무 도메인 심층 분석을 통해 승인 프로세스의 직급별 처리 로직을 이해</li>
<li>비즈니스 로직과 데이터 액세스 계층 분리 설계로 쿼리 분해 및 Java 코드와 결합</li>
</ul>

<p><b>기술적 도전 및 학습:</b></p>
<ul>
<li>복잡한 레거시 쿼리 분석 및 최적화 방법론 습득</li>
<li>비즈니스 로직과 데이터 액세스 계층 분리를 통한 성능 개선 설계 패턴</li>
<li>레거시 시스템 점진적 현대화 프로세스 경험</li>
</ul>
</details>
</div>

---

## 🔍 개인 프로젝트 및 오픈소스 기여

<div style="border-left: 4px solid #9C27B0; padding-left: 15px; margin-bottom: 20px;">
<h3><a href="https://github.com/IDontHaveBrain/AutoClassification">AutoClassification</a></h3>
<p><code>Python</code> <code>Flask</code> <code>Kotlin</code> <code>Spring Boot</code> <code>React</code> <code>TypeScript</code> <code>PostgreSQL</code> <code>Redis</code> <code>Docker</code></p>

<p><b>OpenAI API와 YOLOv8을 활용한 자동 이미지 분류 및 모델 훈련 시스템</b></p>

<table>
  <tr>
    <td><b>🏗️ 멀티모듈 아키텍처</b><br><small>AiServer, UserServer, Frontend</small></td>
    <td><b>⚡ 비동기 처리</b><br><small>이벤트 기반 작업 처리</small></td>
    <td><b>🔒 보안 설계</b><br><small>OAuth2 및 JWT 인증</small></td>
  </tr>
</table>

<details>
<summary><b>기술 스택 선택 이유 및 구현 세부사항</b></summary>

<p><b>AiServer (Python, Flask):</b></p>
<ul>
<li>머신러닝/딥러닝 생태계에 최적화된 Python 선택</li>
<li>경량 웹 프레임워크로 Flask 활용하여 API 엔드포인트 구현</li>
<li>OpenAI API를 활용한 이미지 자동 라벨링</li>
<li>YOLOv8 모델 훈련 파이프라인 구축</li>
</ul>

<p><b>UserServer (Kotlin, Spring Boot):</b></p>
<ul>
<li>JVM 생태계의 안정성과 Kotlin의 현대적 문법 조합 선택</li>
<li>사용자 관리 및 OAuth2 인증 시스템 설계로 보안 강화</li>
<li>PostgreSQL의 관계형 데이터 모델을 활용한 사용자 데이터 관리</li>
<li>Redis를 활용한 분산 세션 관리 및 캐싱으로 성능 최적화</li>
</ul>

<p><b>Frontend (React, TypeScript):</b></p>
<ul>
<li>컴포넌트 기반 구조와 상태 관리의 용이성을 위해 React 선택</li>
<li>TypeScript를 도입하여 코드 안정성 및 개발 생산성 향상</li>
<li>Redux를 활용한 체계적인 상태 관리로 실시간 모델 훈련 상태 추적 기능 구현</li>
</ul>

<p><b>기술적 도전 및 해결:</b></p>
<ul>
<li>다양한 언어로 작성된 서비스 간 통신 아키텍처 설계 및 최적화</li>
<li>대용량 이미지 처리를 위한 비동기 워크플로우 최적화</li>
<li>Docker를 활용한 개발 및 테스트 환경 표준화로 일관된 결과 보장</li>
</ul>
</details>
</div>

<div style="border-left: 4px solid #9C27B0; padding-left: 15px; margin-bottom: 20px;">
<h3>오픈소스 기여</h3>

<p><b>🔧 tree-sitter-language-pack:</b></p>
<ul>
<li>Windows 환경에서의 설치 및 작동 문제 해결을 위한 PR 기여</li>
<li>경로 처리 정규식 패턴 개선 및 MSVC 컴파일러 옵션 추가</li>
<li>Windows 테스트를 GitHub Actions 워크플로우에 추가하여 크로스 플랫폼 호환성 보장</li>
</ul>

<p><b>🔧 multilspy:</b></p>
<ul>
<li>Windows 환경에서 TypeScriptLanguageServer 사용 시 발생하는 'No module named pwd' 오류 해결 PR 기여</li>
<li>Unix 시스템에서만 사용 가능한 pwd 모듈을 Windows에서는 조건부로 임포트하도록 개선</li>
</ul>

<p>오픈소스 프로젝트 기여를 통해 다양한 개발 환경에 대한 이해와 협업 경험을 쌓고 있습니다.</p>
</div>

---

## 💡 개발 철학 및 미래 목표

<table>
  <tr>
    <td width="20%"><b>🔍 문제 해결 접근법</b></td>
    <td>단순 기술적 해결책을 넘어 업무 도메인을 깊이 이해하고 근본적인 문제 원인을 찾아 해결하는 방식 추구</td>
  </tr>
  <tr>
    <td width="20%"><b>📚 지속적 학습</b></td>
    <td>각 프로젝트마다 요구되는 새로운 기술 스택을 빠르게 습득하고 실무에 적용하는 적응력 보유</td>
  </tr>
  <tr>
    <td width="20%"><b>🚀 기술적 도전 추구</b></td>
    <td>난이도 높은 기술적 문제에 적극적으로 도전하고 주니어 개발자로서의 한계를 뛰어넘으려는 열정</td>
  </tr>
  <tr>
    <td width="20%"><b>🔮 미래 목표</b></td>
    <td>시스템 아키텍처 설계와 개발을 균형있게 수행하는 백엔드 전문가로 성장하여 복잡한 기술적 문제를 해결하는 아키텍트 되기</td>
  </tr>
  <tr>
    <td width="20%"><b>🔭 현재 관심 분야</b></td>
    <td>대규모 트래픽 환경에서의 시스템 설계, 마이크로서비스 아키텍처, 분산 시스템 최적화</td>
  </tr>
</table>