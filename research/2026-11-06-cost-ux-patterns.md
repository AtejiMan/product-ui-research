# 무료 여부와 ‘기본적인 UX 실패’를 막는 방법

> **후속 범위 수정:** Ant Design Pro full은 신규 관리 UI의 완성 템플릿 후보이며, 기존 프로젝트를 일괄 교체하라는 결정이 아니다. 기존 UI·올인원 작업환경·스킬 실행 점검에 관한 [최신 결론](2026-11-06-integrated-workflow.md)을 먼저 읽는다.

**확인일: 2026-11-06.** 이 문서는 [운영·관리 UI 기본 선택](2026-11-06-template-choice.md)의 적용 한계를 구체화한다. 현재 추천은 계속 **Ant Design Pro full 하나**이며, 아래 다른 제품은 별도 유형의 앱을 만들 때 검토하는 예시다. 서로 한 프로젝트에 섞으라는 제안이 아니다.

## 1. 무료 여부

- **Ant Design Pro full: MIT 오픈소스.** 무료 사용·수정·상업적 이용 가능. 라이선스 및 저작권 고지는 유지한다. 상용 Pro UI 구독 구매가 필수는 아니다. 공식 앱 틀과 예제 화면에는 업무용 백엔드/데이터 연동 작업이 남는다.
- 원본이 사용하는 **Ant Design** 및 **ProComponents**도 MIT 오픈소스다. 전부 유료 서비스에 가입해야 작동하는 형태가 아니다.
- **별개로 비용이 생길 수 있는 것:** 앱 서버, 데이터베이스, 배포·모니터링 클라우드, 외부 API, 직접 개발·유지보수 시간. 사용하는 추가 패키지와 서비스의 별도 라이선스는 그 시점에 확인한다.

출처: [Ant Design Pro 라이선스](https://github.com/ant-design/ant-design-pro/blob/master/LICENSE), [Ant Design Pro 앱과 full 사용법](https://github.com/ant-design/ant-design-pro), [ProComponents MIT](https://github.com/ant-design/pro-components), [Ant Design MIT](https://github.com/ant-design/ant-design/blob/master/LICENSE).

## 2. 문제가 되는 현상에 이미 붙은 이름

공식 UX 기준에 ‘에이전트가 읽는 로그를 그대로 사용자 화면에 적는다’는 단일 고유 명칭이 있는 것은 아니다. 다음 문제가 겹친 결과로 보아야 한다.

| 사용자가 겪는 현상 | 식별할 이름 | 의미 |
| --- | --- | --- |
| 내부 로그·키·식별자·원시 JSON을 그대로 노출 | **Data dump / implementation-detail leakage** | 내부 표현을 사용자의 의사결정 언어로 바꾸지 못함. 표현상의 진단 용어이며 독립된 표준 휴리스틱 명칭은 아님 |
| 중요한 수치와 부가 설명이 똑같이 강조 | **Weak visual hierarchy** | 크기·위치·색·정보 순서를 통한 우선순위가 없음 |
| 모든 항목을 한 곳에 길게 이어 붙임 | **Information overload / poor grouping** | 항목 간 관계·경계와 읽기 단위를 구분하지 못함 |
| 고급 옵션·오류 전문까지 기본 화면에 노출 | **Failure of progressive disclosure** | 기본 화면에 결정적으로 필요한 정보만 보이는 원칙을 놓침 |
| 모든 요소를 버튼으로 만들고 주작업이 묻힘 | **Control clutter / weak action hierarchy** | 기능의 종류와 중요도에 맞는 컨트롤 선택이 없음 |
| 갱신 시 스크롤·필터·선택이 사라짐 | **Loss of user context / disruptive update** | 상태 유지와 갱신 동작 문제. CSS로 해결되는 문제가 아님 |
| 메뉴 이동과 데이터 갱신 때 화면이 움직이거나 끊김 | **Layout shift / jank** | 레이아웃 안정성과 렌더링 성능 문제 |

위 표는 사용자 사례를 UX 용어에 대응시킨 **분석**이다. 용어 자체가 자동 문제 탐지나 해결을 보장하지 않는다. 근거: [NN/g 10 usability heuristics](https://www.nngroup.com/articles/ten-usability-heuristics/), [NN/g progressive disclosure](https://www.nngroup.com/articles/progressive-disclosure/), [NN/g complex applications](https://www.nngroup.com/articles/complex-application-design/), [IBM Carbon dashboard hierarchy](https://www.carbondesignsystem.com/building-blocks/data-visualization/dashboards), [web.dev layout shifts](https://web.dev/articles/optimize-cls).

## 3. 실제 적용에 필요한 최소 단위

**템플릿만 설치하면 자동 해결되는 것**
- 앱 수준의 메뉴/목록/폼/상세/모달/Drawer 등 기존 화면 유형과 해당 기본 시각·상호작용 구조를 활용할 수 있다.
- 실제 [ProTable](https://pro-components.antdigital.dev/en-US/components/table)은 열 표시/숨김, 밀도, 검색/새로고침 같은 인터페이스를 이미 갖고 있다.
- 프로젝트가 원본 페이지 유형과 행동을 유지할수록 개발자의 임의 배치가 줄어든다.

**템플릿이 자동으로 판단할 수 없는 것**
- 각 도메인에서 무엇이 ‘주요 정보’이며 무엇이 ‘기술 진단 정보’인지.
- 실패 이유와 사용자에게 필요한 후속 행동, 권한 및 문구.
- 자동 갱신으로 인한 문맥 손실 방지, 데이터 요청 방식, 실제 페이지 전환 성능.
- 사용자 작업을 마칠 수 있는지의 평가.

이 부분은 개발자가 새 화면을 만들 때 다음의 **짧은 화면 계약**을 생성해 코드에 반영하는 일로 다룬다. 사용자가 각 문장을 매번 지적하는 방식이 아니다.

1. **대상·목적:** 이 화면을 누가 사용하고 어떤 결정을 내리거나 작업을 완료하는가.
2. **첫 화면:** 그 판단에 꼭 필요한 이름, 상태, 핵심 값, 우선 행동은 무엇인가.
3. **보조 정보:** 자세한 설명·기록·원시 데이터는 어느 상세 패널/탭에 있으며 어떻게 접근하는가.
4. **문맥 유지:** 검색·필터·선택·페이지·스크롤·작업 중 입력을 언제 보존해야 하는가.
5. **증거:** 실제 작업 시나리오로 요약→상세→행동→복귀를 확인했는가; 자동 갱신·좁은 화면·오류 상태를 확인했는가.

예: 처리 작업의 원본 `job_id=3921, retry=3, worker=7, error=TIMEOUT, trace=...`가 있을 때, 사용자용 목록은 **대상 이름 / 처리 실패 / 마지막 시도 시각 / 다시 시도**처럼 표현하고, 기술 코드는 **상세 > 진단 정보**로 옮긴다. 다만 관리자가 기술 진단을 주업무로 하는 화면이라면 로그를 1차 정보로 승격할 수 있다. 정보 위계는 사용자 작업을 기준으로 판단한다.

### 개발자 측 검증 방법

- 신규 화면을 임의로 그리지 않고 **원본 full 템플릿의 해당 페이지**에서 출발해 필요한 데이터만 연결한다.
- 사용자 시나리오를 자동화한다: 필터를 건 상태에서 상세를 열고 닫은 후에도 필터와 위치가 보존되는지, 자동 갱신 후에도 스크롤이 유지되는지, 처리 중 오류가 설명 가능한지.
- 접근성 및 시각적 이동은 별도의 자동 점검을 활용하되, **‘중요한 정보가 잘 드러나는가’는 코드와 실제 사용자 작업 맥락을 놓고 점검**한다. 스크린샷 반복 승인만으로는 부족하다.
- 공개 검증이 끝나지 않은 제품의 UX를 ‘검증 완료’라고 부르지 않는다.

중요한 정보의 선별·표시·행동·복귀·상태 보존은 연결된 하나의 기능 계약으로 평가한다. 과거 디자인 문서도 이 연결을 단위로 이식 여부를 판단한다.

## 4. 관리 화면 밖의 다른 기본형

단일한 범용 템플릿이 모든 제품 유형에 적절한 것은 아니다. 아래는 **서로 다른 종류의 완성된 출발점**이며, 동일 프로젝트에 조합하지 않는다.

| 제품의 주된 용도 | 검토할 기본형 | 직접 보기 | 범위·주의 |
| --- | --- | --- | --- |
| 운영·관리, 검색·목록·상세·설정 | **Ant Design Pro full** (현재 추천) | [공식 표 화면](https://preview.pro.ant.design/list/table-list/) / [기본 폼](https://preview.pro.ant.design/form/basic-form/) | 실제 업무 정보의 우선순위는 개발자가 정리 |
| 관측·메트릭·시계열 분석 | **Grafana OSS** | [Grafana Play](https://play.grafana.org/) | 완성된 모니터링 **제품**. 범용 업무 앱 소스 템플릿 아님; OSS는 AGPL-3.0 |
| 문서·가이드·블로그 웹사이트 | **Docusaurus classic** | [공식 Docusaurus 사이트](https://docusaurus.io/) / [실제 사이트 사례](https://docusaurus.io/showcase) | 문서 사이트 기본 구성 제공; 업무용 CRUD 앱 아님 |
| 상품 탐색·장바구니·주문 | **Medusa Next.js storefront starter** | [공식 쇼핑몰 데모](https://next.medusajs.com/) / [설치 안내](https://docs.medusajs.com/resources/nextjs-starter) | 백엔드 포함 전자상거래 기능 연결. 최신 설치는 Medusa 앱 모노레포 경로 사용; 일부 기업 기능/호스팅은 별도 조건 |

출처: [Grafana 공식 오픈소스](https://github.com/grafana/grafana), [Grafana Play 안내](https://grafana.com/blog/grafana-play-updates-a-redesigned-homepage-to-celebrate-our-community/), [Docusaurus 설치 문서](https://docusaurus.io/docs/installation), [Medusa 오픈소스·기업용 범위](https://github.com/medusajs/medusa), [Medusa storefront 공식 소개](https://medusajs.com/nextjs-commerce).

**적용 범위에 관한 결론:** 운영·관리 UI에는 Ant Design Pro를 기본안으로 유지한다. 전문 편집기나 소비자용 앱을 모두 Ant Design Pro로 강제하지 않는다. 먼저 제품의 **주작업**에 맞는 하나의 기준 구현을 고르고, 그 완성된 흐름과 데이터 구조를 출발점으로 삼는다. 도메인 정보의 분류와 실제 동작 검증은 개발 책임으로 남는다.

## 5. 기존 프로젝트에 가져갈 때의 기술적 제약

Ant Design Pro full은 **React 19 / Umi Max 4 기반 애플리케이션**이다. 기존 프런트엔드가 이 구조와 다르면 완성된 앱 틀을 채택하는 순간 프런트엔드 구조 변경이 필요할 수 있다. 현재 화면이 자체 TypeScript·DOM·CSS로 작성된 프로젝트에서는 특히 그렇다. 단순히 CSS 테마를 복사해서 같은 동작을 얻을 수 있다는 주장은 하지 않는다.

따라서 **새 React 관리 앱**과 **기존 비React 앱의 UI 개선**은 실행 계획이 달라진다. 두 경우 모두 정보 분류와 사용자 작업 계약을 먼저 파악해야 한다. 기존 비React 앱에 대해서는 교체 범위·상태 보존·API 영향이 확인되기 전까지 '템플릿 결정=이식 완료'라고 표시하지 않는다.

출처: [Ant Design Pro 원본 프런트엔드 기술 구성](https://github.com/ant-design/ant-design-pro).

## 6. 근거의 한계

- 공식 UI 데모와 공개 소스는 **기본 화면 유형과 일부 상호작용의 존재**를 입증한다.
- 사용자가 지적한 프로젝트의 모든 화면이 올바르게 바뀐다거나 자동 갱신·성능이 좋아진다는 뜻은 아니다. 실제 제품 이식과 작업 시나리오를 검증해야 한다.
- 사용자 제공 Substack 글 `Most AI Design Skills Do Nothing`의 본문은 이번 브라우징에서 읽을 수 없었다. 제목만으로 글의 주장이나 실험 결과를 확정하지 않았다. 이 문서의 판단은 위에 직접 링크한 1차 자료에 근거한다.
