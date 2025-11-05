<h1>202230231 이하늘</h1>
<hr>

## 11월 5일 (11주차)

<h2>데이터 가져오기<h2>

- fetch 응답은 기본적으로 캐싱되지 않음
- 개발 중에는 가시성과 디버깅 개선을 위해 fetch 호출을 기록할 수 있음
- 서버 컴포넌트(Server Component) 는 서버에서 렌더링되므로 ORM이나 데이터베이스 클라이언트를 사용해 안전하게 쿼리 실행 가능
- 컴포넌트를 비동기 함수로 변환하고 await 호출하면 데이터 처리 가능
- 클라이언트 컴포넌트(Client Component) 에서 데이터를 가져오는 방법 두 가지: eact의 use Hook SWR 또는 React Query 같은 통신 라이브러리 사용

## 10월 29일 (10주차)

<h2>React 19 주요 특징 및 Server Actions</h2>

- React 19에서는 Server Actions와 같은 기능을 통해 서버와 클라이언트의 경계가 명확해짐
- Server Actions를 통해 클라이언트에서 직접 서버 함수를 호출 가능
- Server에서 데이터를 받아오고, 그 결과를 클라이언트로 스트리밍하여 렌더링 최적화 가능
- useOptimistic 훅을 사용하면 서버 응답을 기다리지 않고 UI를 즉시 업데이트하는 낙관적 렌더링 구현 가능
- Suspense와 함께 사용하면 대기 상태를 효과적으로 처리 가능

<h2>서버 및 클라이언트 컴포넌트 인터리빙</h2>

- Client의 state를 사용하여 표시 여부를 전환하는 모달 컴포넌트 안에 Server에서 데이터를 가져오는 카트 컴포넌트가 있음
- 모든 Server Component는 서버에서 미리 렌더링되고, Client Component가 렌더링되어야 하는 위치에 대한 참조가 포함됨

<h2>Context란 무엇인가?</h2>

- 전역 상태 관리 도구
- props drilling 문제 해결
- React 컴포넌트 간 데이터 공유
- 클라이언트 컴포넌트에서 사용 가능
- 서버 컴포넌트에서는 제한적

<h2>Context Provider (컨텍스트 제공자)</h2>

- React Context는 전역 상태를 공유하는 데 사용
- Server Component에서는 Context가 지원되지 않음
- Provider Component를 트리 깊숙이 렌더링하는 것이 권장됨
- 속성 선택자(Attribute Selector)를 이용하면 CSS 충돌을 줄일 수 있음

---

## 10월 17일 (8주차)

<h2>3-1. Client Component</h2>

- 브라우저 환경에서 렌더링되는 컴포넌트로 상호작용이 필요한 UI에 사용
- 상태(state), 이벤트 핸들러(event handler), 브라우저 API 접근 가능
- 예시: Counter, Like Button

<h2>3-2. JS Bundle 크기 줄이기</h2>

- Layout 컴포넌트는 기본적으로 Server Component
- 대화형이 필요한 일부 요소만 Client Component로 지정
- `'use client'` 선언을 통해 명시적으로 클라이언트 컴포넌트로 설정

<h2>3-3. Server ↔ Client Component 관계</h2>

- Server Component는 Client Component를 포함할 수 있으나, 반대는 불가능
- Client Component는 props를 통해 Server Component 데이터를 전달받음
- 데이터 직렬화 필요
- fetch 로직은 Server에서 수행하고 결과만 Client로 전달

---

## 10월 1일 (6주차)

<h2>Client-side transitions (클라이언트 측 전환)</h2>

- 서버 렌더링 페이지 이동 시 전체 페이지가 다시 로드됨
- <Link> 컴포넌트를 사용하면 상태 초기화 방지 및 빠른 전환 가능
- 프리패칭(prefetching)과 스트리밍(streaming)으로 동적 경로에서도 빠른 전환 구현 가능

<h2>generateStaticParams 비교</h2>

- 없는 경우: slug를 빌드 타임에 알 수 없어 요청마다 동적 렌더링
- 있는 경우: 정적 HTML + JSON을 빌드 타임에 생성 → SSR 불필요

<h2>느린 네트워크 환경</h2>

- 프리패칭 완료 전 클릭 시 지연 발생 가능
- loading.tsx가 즉시 표시되지 않을 수 있음
- useLinkStatus Hook 사용으로 상태 추적 가능

---

## 9월 24일 (5주차)

<h2>searchParams란?</h2>

- URL 쿼리 문자열을 읽는 방법
- searchParams는 props로 전달되어 URLSearchParams처럼 동작

<h2>Linking between pages (페이지 간 연결)</h2>

- <Link> 컴포넌트를 사용하여 페이지 간 탐색
- HTML a 태그를 확장하여 prefetching 및 client-side navigation 제공

<h2>Streaming (스트리밍)</h2>

- 동적 경로 일부를 미리 전송 가능
- 공유 레이아웃 및 로딩 스켈레톤을 빠르게 렌더링

---

## 9월 17일 (4주차)

<h2>git checkout vs git switch</h2>

- checkout은 브랜치 이동 및 파일 변경 가능 (위험함)
- switch는 브랜치 이동만 가능 (안전함)
- switch 사용 권장

<h2>Creating a nested route (중첩 라우트)</h2>

- 폴더 구조를 중첩하여 다중 URL 세그먼트 생성
- [slug] 폴더를 사용해 동적 경로 구현 가능

<h2>Rendering with search params</h2>

- Server Component에서 searchParams prop을 통해 검색 매개변수 접근 가능
- 해당 페이지는 동적 렌더링 처리됨

---

## 9월 10일 (3주차)

<h2>Folder and file conventions (폴더 및 파일 규칙)</h2>

- Next.js는 폴더를 URL 세그먼트로 매핑
- layout은 경로별 공유, template은 새 인스턴스로 초기화
- Route groups: (폴더명) 형식으로 그룹화 가능

---

## 9월 3일 (2주차)

<h2>Next.js 기본 설정 및 구조</h2>

<h3>strict 모드 및 eslint</h3>
- Next.js의 기본 ESLint 구성은 엄격한 코드 품질 검사 제공  
- eslint.config.mjs 사용 권장 (ESLint v9 이상 공식 방식)  
- .eslintrc.json보다 유연하고 모듈화된 설정 가능

<h3>자동 생성 항목</h3>
- package.json에 scripts 자동 추가  
- tsconfig.json / eslint.config.mjs / Tailwind CSS / src 디렉토리 자동 생성 가능  
- App Router 기본 포함

<h3>Core Web Vitals</h3>
- LCP: 가장 큰 콘텐츠 표시까지의 시간  
- FID: 첫 입력 후 응답 시간  
- CLS: 페이지 레이아웃 이동 빈도

<h3>pnpm 개요</h3>
- 효율적(Performant) NPM의 약자  
- 하드링크 기반 저장공간 절약  
- 빠른 패키지 설치 및 의존성 관리

<h3>Hard Link vs Symbolic Link</h3>
- 하드링크: 원본과 동일한 파일로 저장  
- 심볼릭 링크: 원본 경로를 참조 (바로가기와 유사)  
- 원본 삭제 시 심볼릭 링크는 끊어짐

<h3>용어 정리</h3>
- route: 경로  
- routing: 경로 탐색 과정  
- directory: 상위 폴더, folder: 일반 폴더

---

## 8월 27일 (1주차)

- 오리엔테이션(OT) 진행
- 개발 환경 및 설치 실습
