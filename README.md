# 포트폴리오

## 1. 프로젝트

### 1.1 공통 컴포넌트 라이브러리 관리

**소개**

- Tmax WAPL
- 2024.01 - 진행 중
- **TypeScript, React, Vite**
- 협업 도구 내부의 (메신저, 캘린더와 같은) 여러 애플리케이션에서 **공통으로 사용하는 컴포넌트를 제공하는 라이브러리**를 **관리**했습니다.

**성과**

- 라이브러리 빌드 속도 개선

  - **\[상황\]**
    - 오래된 버전의 Rollup을 사용했었고, 설정 파일이 관리 되지 않고 있었습니다.
    - 빌드 속도가 느려서 팀원들이 개발할 때 불편해했습니다.
  - **\[과정\]**
    - 최근 많은 곳에서 안정적으로 사용되고 빠른 속도를 자랑하는 Vite를 도입해, 빌드 속도를 개선하고, 관련 코드도 최신화하기로 했습니다.
    - vite 공식 문서를 참고해 필요한 플러그인들을 설정했습니다. 라이브러리로 빌드하기 위해 필요한 설정도 추가했습니다.
    - Vite로 마이그레이션 하던 도중, 클라이언트 코드에서 타입 추론이 제대로 되지 않는 문제가 발생했습니다. 원인이라고 생각되는 설정을 수정하고 빌드 결과를 확인하면서, 원인을 찾고 문제를 해결했습니다.
  - **\[결과\]**
    - Vite로 마이그레이션 후, 다른 앱에서 라이브러리를 사용했을 때 문제없이 동작했습니다.
    - **빌드 시간이 `63` 초에서 `13` 초로 단축**되어 **팀 개발 생산성이 향상**되었습니다.
  - **\[회고\]**
    - 빌드 도구와 번들러 설정은 막연히 어렵다고 생각했는데, 성공적으로 Vite로 마이그레이션 하면서 자신감을 얻을 수 있었습니다.

- 공통 컴포넌트의 Props Drilling 제거
  - **\[상황\]**
    - 대부분의 공통 컴포넌트가 깊은 depth를 가지고 있어서 Props Drilling이 발생했습니다.
  - **\[해결\]**
    - 상위 컴포넌트에서 Context를 이용해 데이터를 제공하고 하위 컴포넌트는 해당 데이터가 필요하면 가져다 쓰는 형태로 구조를 변경해서, Props Drilling을 제거했습니다.

### 1.2 유저 모임(Room, 룸) 컴포넌트 개발

**소개**

- Tmax WAPL
- 2024.01 - 진행 중
- **TypeScript, React, Vite, MobX, Emotion, MUI, React Hook Form**
- 룸은 (회사에서 개발 중인 협업도구에서) 유저들의 모임을 의미합니다.
- **서울시교육청**와 **한국농어촌공사**의 협업 도구에 적용했습니다.

#### 1.2.1 룸 리스트 개발

**업무**

- 로그인한 유저가 속한 룸 목록 조회 및 표시 기능 구현
- 룸 이름 기반 검색 기능 구현
- 룸 타입 기반 필터링 기능 구현
- 애플리케이션에 따라 달라지는 메뉴와 버튼을 제공하기 위해, "메신저, 캘린더 앱 프론트엔드 팀"과 소통 및 Props 구조 구상

**성과**

- 룸 리스트 컴포넌트가 리렌더링 될 때마다 상태가 초기화되는 문제 해결
  - **\[상황\]**
    - 메신저 앱에서 룸 리스트 컴포넌트를 사용할 때, 간헐적으로 리스트 컴포넌트의 상태가 초기화되는 문제가 발생했습니다.
  - **\[과정 & 결과\]**
    - 최상단에 위치한 룸 리스트 컴포넌트가 렌더링 될 때마다, MobX Store의 인스턴스가 새로 만들어져서 Context로 제공되었기 때문에 발생했습니다.
    - `useState`와 initializer 함수를 함께 쓰거나 `useRef`를 사용해, 리렌더링이 될 때마다 인스턴스가 생성되는 것을 방지해서 문제를 해결했습니다.
