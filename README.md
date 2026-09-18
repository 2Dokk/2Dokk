<div align="center">

# 안녕하세요, 2Dokk입니다 👋

<!-- 소개 문구는 나중에 추가 -->

<!-- 값 채운 뒤 주석 해제
| 이름 | 학교 | 전공 | 복수전공 |
|:---:|:---:|:---:|:---:|
| {이름} | {학교} | {전공} | {복수전공} |
-->

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
![LLM](https://img.shields.io/badge/RAG_·_LLM-191919?style=flat-square)

**Test / Infra** &nbsp;
![JUnit5](https://img.shields.io/badge/JUnit5-25A162?style=flat-square&logo=junit5&logoColor=white)
![Testcontainers](https://img.shields.io/badge/Testcontainers-2496ED?style=flat-square)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white)

---

## 📌 Projects

### 🛰 [위성 지상국 관제 콘솔 (TT&C Console)](https://github.com/2Dokk/ttc-console)
> 위성이 지상국 상공을 지나는 **몇 분 동안만 통신할 수 있다**는 제약을 그대로 구현한 소형 관제 시스템

- 공개 궤도 데이터(Celestrak TLE) + **Orekit SGP4** 로 위성 위치와 **AOS/LOS** 계산
- 가시권 밖 명령은 **PENDING** 으로 대기 → AOS 시 **슬라이딩 윈도우 + Go-Back-N**(COP-1 단순화)으로 순서대로 정확히 한 번 전달
- 교신 불가 구간 텔레메트리는 온보드 레코더에 저장했다가 다음 패스에 **재생(playback)**
- 명령의 **전달 확인(ACK)** 과 **실행 확인(EXECUTED/REJECTED)** 을 분리 검증

`Spring Boot` `Orekit` `STOMP WebSocket` `PostgreSQL` `Flyway` `React` `TypeScript` `Testcontainers`

---

### 💸 [DVP 증권결제 시뮬레이터](https://github.com/2Dokk/dvp-settlement-simulator)
> 증권 이전과 대금 지급이 **반드시 함께 성공하거나 함께 실패**하는 DVP 결제를 넷팅·동시성 제어까지 포함해 구현

- DVP 원자성 = 하나의 `@Transactional` 안에서 **잠금 → 양쪽 검증 → 일괄 반영**
- 배치 넷팅을 CCP 상대방 구조로 정산, 부족 참가자를 한 명씩 제외하며 **정산 가능한 거래 집합을 먼저 확정**
- 처음 설계에서 발견한 **CCP 잔여 불균형 버그**를 구조적으로 불가능하게 재설계하고 테스트로 검증
- 계좌를 **고정 순서로 잠가** 교착 상태 방지

`Java 21` `Spring Boot 3` `PostgreSQL` `Testcontainers` `GitHub Actions`

---

### 📈 [Smart Order Router (KRX · NXT)](https://github.com/2Dokk/smart-order-router)
> 한국거래소와 넥스트레이드 복수시장 환경에서 주문을 가장 유리한 시장으로 나눠 보내는 **SOR 엔진 + 모의 거래소**

- **가격·시간 우선** 매칭엔진 직접 구현 (지정가/시장가, DAY·IOC·FOK, KRX 호가단위 검증)
- 통합 호가창(`ConsolidatedBook`)과 라우팅 전략 분리 — 전략이 틀려도 원주문보다 불리한 주문은 나갈 수 없게 설계
- 자식 주문마다 **최선집행 근거 로그** 기록
- 같은 입력이면 같은 결과가 나오는 **결정적 설계**로 KRX 단독 vs SOR **백테스트 비교 리포트** 생성

`Java 21` `Gradle 멀티모듈` `JUnit5`

---

### 🌿 [한의원 진료 기록 자동 정리 도우미 (RAG)](https://github.com/2Dokk/Rag-Project)
> 진료 중 남긴 짧은 메모를 **정식 진료기록으로 구조화**하고, 과거 방문 이력을 근거로 **비교 브리핑**을 생성

- 메모 구조화 → 벡터DB(Chroma)에서 같은 환자의 **과거 이력 의미 검색** → 이력을 근거로 LLM 브리핑 생성
- LLM 호출 추상화(Anthropic / OpenAI / Gemini) + 429 재시도, API 키 없이도 동작하는 **규칙 기반 폴백 모드**
- 가상 환자 데이터만 사용, 실제 적용 시 필요한 개인정보·의료법 요건 명시

`Python` `Chroma` `LLM API` `RAG`

---

### 🎓 CNU&U — 학회 운영·활동 관리 서비스
[Frontend](https://github.com/2Dokk/unu-frontend) · [Backend](https://github.com/2Dokk/unu-backend)

> 학회원 관리, 활동 모집·신청, 출석, 공지, 예산 관리를 한곳에서 처리하는 웹 서비스

- JWT + `@PreAuthorize` 기반 **역할별 권한 제어** (학회원 / 운영진 / 담당자)
- 월별 예산안(예상·실제), 스터디 보증금 원장, 지출 내역 관리 및 **Apache POI 엑셀 내보내기·업로드**
- 활동 개설 → 모집 → 신청 → 출석 → 수료까지 전체 흐름 구현

`Spring Boot 3.5` `Spring Security` `JPA` `PostgreSQL` `Next.js 16` `shadcn/ui` `Docker`

---

<div align="center">

![GitHub stats](https://github-readme-stats.vercel.app/api?username=2Dokk&show_icons=true&hide_border=true&count_private=true)

</div>
