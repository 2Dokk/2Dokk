<div align="center">

<!-- 소개 문구는 나중에 추가 -->

| 이름 | 학교 | 전공 | 복수전공 |
|:---:|:---:|:---:|:---:|
| 이도경 | 서강대학교 | 아트&테크놀로지 | 컴퓨터공학과 |

[![Email](https://img.shields.io/badge/Email-2dokyoung%40gmail.com-EA4335?style=flat-square&logo=gmail&logoColor=white)](mailto:2dokyoung@gmail.com)

</div>

---

## 🛠 Tech Stack

**Backend** &nbsp;
![Java](https://img.shields.io/badge/Java_21-007396?style=flat-square&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot_3-6DB33F?style=flat-square&logo=springboot&logoColor=white)
![Spring Security](https://img.shields.io/badge/Spring_Security-6DB33F?style=flat-square&logo=springsecurity&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![WebSocket](https://img.shields.io/badge/STOMP_WebSocket-010101?style=flat-square&logo=socketdotio&logoColor=white)

**Frontend** &nbsp;
![React](https://img.shields.io/badge/React-61DAFB?style=flat-square&logo=react&logoColor=black)
![Next.js](https://img.shields.io/badge/Next.js-000000?style=flat-square&logo=nextdotjs&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![Tailwind](https://img.shields.io/badge/Tailwind_CSS-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white)

**AI / Data** &nbsp;
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![Chroma](https://img.shields.io/badge/Chroma_VectorDB-FF6446?style=flat-square)
![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=flat-square&logo=langchain&logoColor=white)
![LLM](https://img.shields.io/badge/RAG_·_LLM-191919?style=flat-square)

**Test / Infra** &nbsp;
![JUnit5](https://img.shields.io/badge/JUnit5-25A162?style=flat-square&logo=junit5&logoColor=white)
![Testcontainers](https://img.shields.io/badge/Testcontainers-2496ED?style=flat-square)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white)

---

## 📌 Projects

### 🛰 [위성 지상국 관제 콘솔 (TT&C Console)](https://github.com/2Dokk/ttc-console)

`2026.09` &nbsp; `개인 프로젝트`

`Spring Boot` `Orekit` `STOMP WebSocket` `PostgreSQL` `Flyway` `React` `TypeScript` `Testcontainers`

> 위성이 지상국 상공을 지나는 **몇 분 동안만 통신할 수 있다**는 제약을 그대로 구현한 소형 관제 시스템

<a href="https://github.com/2Dokk/ttc-console"><img src="https://raw.githubusercontent.com/2Dokk/ttc-console/main/docs/console.png" width="100%" alt="지상국 관제 콘솔 화면"></a>

- 공개 궤도 데이터(Celestrak TLE) + **Orekit SGP4** 로 위성 위치와 **AOS/LOS** 계산
- 가시권 밖 명령은 **PENDING** 으로 대기 → AOS 시 **슬라이딩 윈도우 + Go-Back-N**(COP-1 단순화)으로 순서대로 정확히 한 번 전달
- 교신 불가 구간 텔레메트리는 온보드 레코더에 저장했다가 다음 패스에 **재생(playback)**
- 명령의 **전달 확인(ACK)** 과 **실행 확인(EXECUTED/REJECTED)** 을 분리 검증

---

### 💸 [DVP 증권결제 시뮬레이터](https://github.com/2Dokk/dvp-settlement-simulator)

`2026.09` &nbsp; `개인 프로젝트`

`Java 21` `Spring Boot 3` `PostgreSQL 16` `Testcontainers` `GitHub Actions`

> 증권 이전과 대금 지급이 **반드시 함께 성공하거나 함께 실패**하는 DVP 결제를 넷팅·동시성 제어까지 포함해 구현

<a href="https://github.com/2Dokk/dvp-settlement-simulator"><img src="https://raw.githubusercontent.com/2Dokk/dvp-settlement-simulator/main/docs/images/netting.png" width="100%" alt="넷팅 전후 비교: 결제 이동 18건 → 4건"></a>

- DVP 원자성 = 하나의 `@Transactional` 안에서 **잠금 → 양쪽 검증 → 일괄 반영**
- CCP 상대 **배치 넷팅**으로 결제 이동 **18건 → 4건 (78% 감소, 테스트 데이터 기준)**
- 부족 참가자를 한 명씩 제외하며 정산 가능한 거래 집합을 먼저 확정 → 처음 설계의 **CCP 잔여 불균형 버그**를 구조적으로 제거
- **고정 순서 비관적 잠금**으로 교착상태 방지: 20건 동시 결제 요청에서 정확히 16건만 성공, 초과 인출 0

<details>
<summary>🔍 동시성·장애 시나리오 검증 결과 보기</summary>
<br>
<img src="https://raw.githubusercontent.com/2Dokk/dvp-settlement-simulator/main/docs/images/results.png" width="100%" alt="동시성·장애 시나리오 검증 결과">
</details>

---

### 📈 [Smart Order Router (KRX · NXT)](https://github.com/2Dokk/smart-order-router)

`2026.09` &nbsp; `개인 프로젝트`

`Java 21` `Gradle 멀티모듈` `JUnit5` `GitHub Actions`

> 한국거래소와 넥스트레이드 복수시장 환경에서 주문을 가장 유리한 시장으로 나눠 보내는 **SOR 엔진 + 모의 거래소**

<a href="https://github.com/2Dokk/smart-order-router"><img src="https://raw.githubusercontent.com/2Dokk/smart-order-router/main/docs/images/backtest-results.png" width="100%" alt="백테스트 결과: 가상 시장 2,000건에서 세 방식 비교"></a>

- **가격·시간 우선** 매칭엔진 직접 구현 (지정가/시장가, DAY·IOC·FOK, KRX 호가단위 검증)
- 통합 호가창과 라우팅 전략 분리 — 전략은 계획만 세우고, 주문은 **안전 검사를 통과해야** 나가도록 설계
- 호가 깊이까지 나눠 보내는 **분할(Sweep) 전략**: 가상 시장 2,000건에서 체결률 **66.2% → 73.9%**, KRX 단독 대비 **+2.11bp**, 불리한 주문 **0건** (모의 시뮬레이션, seed 42)
- 같은 입력이면 같은 결과가 나오는 **결정적 설계**, 자식 주문마다 **최선집행 근거 로그** 기록

<details>
<summary>🔍 아키텍처 · 라우팅 비교 예시 보기</summary>
<br>
<img src="https://raw.githubusercontent.com/2Dokk/smart-order-router/main/docs/images/architecture.png" width="100%" alt="아키텍처: 주문 하나가 두 거래소로 나뉘어 체결되기까지">
<br><br>
<img src="https://raw.githubusercontent.com/2Dokk/smart-order-router/main/docs/images/routing-example.png" width="100%" alt="라우팅 비교: 같은 274주 매수 주문을 세 방식으로 처리한 결과">
</details>

---

### 🌿 [한의원 진료 기록 자동 정리 도우미 (RAG)](https://github.com/2Dokk/Rag-Project)

`2026.09` &nbsp; `개인 프로젝트`

`Python 3.11` `LangChain` `Chroma` `sentence-transformers` `Gemini API`

> 진료 중 남긴 짧은 메모를 **정식 진료기록으로 구조화**하고, 과거 방문 이력을 근거로 **비교 브리핑**을 생성

<a href="https://github.com/2Dokk/Rag-Project"><img src="https://raw.githubusercontent.com/2Dokk/Rag-Project/main/docs/images/architecture.png" width="100%" alt="RAG 파이프라인 구조"></a>

- 과거 방문 기록을 다국어 임베딩(MiniLM, 384차원)으로 Chroma에 적재, **환자 ID로 먼저 필터**해 환자 간 정보 혼입 차단
- 오늘 메모 + 검색된 과거 이력으로 LLM이 **날짜를 인용한 비교 브리핑** 생성
- 결과를 원본과 대조해 **환각(서술 순서를 인과로 오해, 기록에 없는 표현 추가)을 발견** → 근거 규칙 4개를 프롬프트에 명시해 개선
- Anthropic / OpenAI / Gemini 교체 가능 + 429 재시도, API 키가 없으면 **규칙 기반 폴백**

<details>
<summary>🔍 LLM 환각 발견과 개선 과정 보기</summary>
<br>
<img src="https://raw.githubusercontent.com/2Dokk/Rag-Project/main/docs/images/hallucination_before_after.png" width="100%" alt="환각 개선 전후 비교">
</details>

---

### 🎓 [CNU&U — 학회 운영 시스템 · 예산 관리](https://github.com/2Dokk/unu-project)

`2026.03 – 2026.09` &nbsp; `팀 프로젝트 · 4인` &nbsp; `담당: 예산 관리 · 신청자 알림`

`Java 21` `Spring Boot 3.5` `Spring Data JPA` `PostgreSQL` `Spring Security (JWT)` `Apache POI` `Next.js 16` `TypeScript` `shadcn/ui`

> 서강대학교 학회 운영 서비스 위에, 총무가 구글 시트로 하던 **예산 관리**를 옮겨 온 팀 프로젝트
> <br>회원·활동·모집·공지 등 기본 틀은 팀원들이 만들었고, **예산 관리 도메인 전체와 신청자 알림**을 설계·구현했습니다.
> <br>[Project](https://github.com/2Dokk/unu-project) · [Frontend](https://github.com/2Dokk/unu-frontend) · [Backend](https://github.com/2Dokk/unu-backend)

<p align="center">
<a href="https://github.com/2Dokk/unu-project"><img src="https://raw.githubusercontent.com/2Dokk/unu-project/main/docs/images/budget-overview.png" width="60%" alt="월별 예산안 화면"></a>
<br>월별 예산안
</p>

- 총무와 직접 요구사항을 정리해 **기존 시트 양식은 유지하면서 반복 입력을 없애는 것**을 목표로 설계
- **원천 기록과 파생 값 분리**: 스터디 보증금 원장·지출 건별 내역이 원천이고 월 금액은 합계 → 수정 창·엑셀·API 어느 경로로 저장해도 서버에서 원천으로 다시 계산
- 스터디 신청·수료·취소·반려에 따라 **보증금 원장이 자동 연동**, 전월 이월금·15% 환급비 자동 계산
- **엑셀 내려받기/올리기**(Apache POI): 총무 시트와 같은 양식 + 엑셀 수식, 업로드는 **미리보기 → 확인 → 적용**, 오류가 하나라도 있으면 전부 미반영
- 운영진·담당자 헤더에 **활동별 새 신청 수 알림**, 예산 API는 `@PreAuthorize`로 운영진 전용
- 고친 문제: 권한 없는 예산 삭제, 겨울학기 데이터 누락·이월금 0, 보증금 있는 활동 삭제 시 500 오류, 월별 항목 중복

<details>
<summary>🔍 보증금 · 지출 상세 내역 · 자동 계산 잠금 · 엑셀 업로드 · 신청자 알림 화면 보기</summary>
<br>
<table>
<tr>
<td width="50%"><img src="https://raw.githubusercontent.com/2Dokk/unu-project/main/docs/images/deposit-detail.png" alt="스터디 보증금 상세"><br><p align="center">스터디 보증금 상세</p></td>
<td width="50%"><img src="https://raw.githubusercontent.com/2Dokk/unu-project/main/docs/images/edit-locked.png" alt="자동 계산 항목 잠금"><br><p align="center">자동 계산 항목 잠금</p></td>
</tr>
<tr>
<td width="50%"><img src="https://raw.githubusercontent.com/2Dokk/unu-project/main/docs/images/expense-menu.png" alt="지출 상세 내역 메뉴"><br><p align="center">지출 상세 내역 메뉴</p></td>
<td width="50%"><img src="https://raw.githubusercontent.com/2Dokk/unu-project/main/docs/images/expense-detail.png" alt="엠티 건별 내역"><br><p align="center">건별 입력 (엠티)</p></td>
</tr>
<tr>
<td width="50%"><img src="https://raw.githubusercontent.com/2Dokk/unu-project/main/docs/images/excel-upload-preview.png" alt="엑셀 업로드 미리보기"><br><p align="center">엑셀 업로드 미리보기</p></td>
<td width="50%"><img src="https://raw.githubusercontent.com/2Dokk/unu-project/main/docs/images/notification.png" alt="신청자 알림"><br><p align="center">신청자 알림</p></td>
</tr>
</table>
<sub>화면의 이름·학번·금액은 모두 시연용 가상 데이터입니다.</sub>
</details>

