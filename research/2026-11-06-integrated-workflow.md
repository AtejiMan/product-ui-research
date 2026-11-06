# 올인원 UI 작업환경과 실제로 실행되는 점검

**확인일: 2026-11-06 (KST). 조사·설계 판단이며 제품 코드 변경·설치·계정 연결·배포는 수행하지 않았다.** 비공개 프로젝트의 상세 코드·설정·진단 기록은 이 공개 문서에 싣지 않는다.

## 결론과 이전 추천의 범위 수정

**기존 제품들을 모두 Ant Design Pro로 바꾸는 것을 권하지 않는다.** Ant Design Pro full은 신규 운영·관리 UI에 쓸 수 있는 완성 템플릿 후보로 남는다. 이미 React와 다른 UI 라이브러리로 구현된 제품이나 전문 편집기에는 별도 판단이 필요하다.

현재 조건에서 설계→눈으로 보는 시안→기존 코드로 인계를 잇는 **새 통합 작업환경 하나를 고른다면 Claude Design + Claude Code의 공식 통합 흐름**을 먼저 선택한다. 기존 Claude 유료 구독·로컬 개발 흐름을 활용할 수 있고, 이미 쓰는 React 컴포넌트를 그대로 기준으로 삼을 수 있기 때문이다.

**기존 코드 수정·브라우저 실행·테스트·PR까지 클라우드 환경 하나로 옮기고 싶다면 v0가 대안**이다. 기능이 실제로 있는 제품과, 모든 UX 실수를 무인으로 막아 준다는 보장은 구분한다.

새 디자인 스킬을 여러 개 설치하는 것은 현재 추천이 아니다. **설치된 스킬의 발동·프로젝트 맥락·검사 실행 연결을 확인하는 것이 먼저**다.

## 1. 서로 다른 세 종류를 구분한다

| 종류 | 예 | 맡는 일 |
| --- | --- | --- |
| 제품 안에 들어가는 화면 코드 | Ant Design Pro, Mantine | 테이블·폼·상세·공통 컴포넌트와 시각 구조 |
| 설계와 구현 작업환경 | Claude Design/Code, v0 | 기존 자료 읽기, 시안, 실제 코드 인계·수정, 자체 검토 |
| 실행 가능한 점검 도구 | Impeccable detector, React Doctor, 기존 브라우저 회귀 테스트 | 정해진 결함 탐지, 코드·화면·상호작용 확인 |

어느 한 도구 이름을 세 종류 전체의 대체재로 설명하면 안 된다. 통합 작업환경을 채택하려고 모든 기존 앱의 UI 라이브러리까지 바꿀 이유는 없다.

## 2. TypeScript와 React, 전환 난이도

TypeScript는 사용하는 언어이고 React는 UI를 구현하는 라이브러리다. **TypeScript만 쓰는 화면**과 **TypeScript+React 화면**이 모두 가능하다. React를 도입해도 TypeScript나 Go 백엔드를 버릴 필요는 없다.

[React 공식 가이드](https://react.dev/learn/add-react-to-an-existing-project)는 기존 페이지 일부나 특정 경로부터 React를 추가할 수 있다고 설명한다. 다만 Ant Design Pro full 전체의 앱 구조를 채택하는 것과 React 부품 하나를 넣는 것은 다른 범위다.

- **기존 React 앱:** React 전환 비용은 없지만, UI 라이브러리·라우팅·테마·템플릿을 교체하면 화면과 상태 연결을 다시 확인해야 한다.
- **직접 DOM을 조작하는 TypeScript 앱:** 화면 렌더링·이벤트·상태·빌드 경로를 옮겨야 한다. API·업무 로직의 일부는 유지할 수 있다.
- **의존성 금지 정책이 있는 앱:** 구현만의 문제가 아니라 빌드·의존성 정책 변경도 함께 필요하다.
- **편집기·오프라인 앱:** IME, 포커스, 선택 영역, 임시 입력, 데이터 저장·동기화는 관리 화면 템플릿이 대신 해결하지 않는다.

난이도는 일반적인 프런트엔드 전환 작업의 범위로 설명할 수 있지만, 실제 영향 파일과 기능을 분석하지 않고 일수를 확정하지 않는다. **React 미사용과 UI 불량은 같은 말이 아니다.** React에서도 잘못된 갱신·재마운트는 문맥 손실을 일으킬 수 있다.

## 3. 올인원 후보 하나: Claude Design + Claude Code

[제품 화면·공식 시연](https://claude.com/product/design) / [제품 UI·코드 인계 예시](https://academy.claude.com/tutorials/using-claude-design-for-prototypes-and-ux)

확인한 현재 기능:

- Claude 대화·Artifacts·Claude Code 안에서 디자인 캔버스를 사용한다.
- 기존 React 컴포넌트·토큰은 Claude Code의 `/design-sync` 경로로 가져온다.
- `/design`은 디자인 생성·수정, 코드에 디자인 가져오기, 기존 코드를 프로토타입으로 내보내는 흐름을 제공한다.
- 공식 설명상 기존 디자인 시스템과 결과를 대조하고 수정한다.
- 기존 Claude/Claude Code와 **공용 사용량**을 소비하며 별도 Design 주간 한도는 없다.
- Design 자체는 Free에도 있지만, **Design Systems는 유료 플랜의 beta 기능**으로 별도 안내된다.
- 구 독립 사이트 `claude.ai/design`은 2026-12-14 종료 예정이다. 신규 기준은 Claude 안의 통합 Design이다.

근거: [시작 가이드](https://support.claude.com/en/articles/14604416-get-started-with-claude-design), [디자인 시스템 설정](https://support.claude.com/en/articles/14604397-set-up-your-design-system-in-claude-design).

### 무엇이 달라지는가

개발자가 기존 정상 컴포넌트와 기준 화면을 읽고, 같은 맥락에서 시안과 구현을 이어갈 수 있다. 매번 여러 도구에서 독립된 시안을 만든 뒤 새 UI로 옮기는 작업이 줄어든다. 제품 소유자는 필요할 때 실제 시안을 열어볼 수 있지만, 모든 수정의 승인 담당자가 될 필요는 없다.

이것은 **통합·재사용 기능에 근거한 적합성 판단**이다. 사용자 프로젝트에서 정보 위계·사용성·성능이 모두 개선된다는 독립 실험 결과로 소개하지 않는다.

### 한계

공식 Help도 디자인 시스템 import는 원본 품질에 좌우되며, 복잡하게 꼬인 코드나 불완전한 자료의 문제는 결과에 반영된다고 명시한다. 따라서 현재 잘못된 화면 전체를 재현 기준으로 삼아서는 안 된다. 기준 컴포넌트와 올바른 업무 흐름을 고르는 일은 개발자가 맡아야 한다.

자동 갱신·스크롤·입력 보존·실제 API 오류·오프라인 무결성 검증은 실행되는 앱에서 해야 한다. 디자인 캔버스 자체의 미리보기만으로 검증 완료로 처리하지 않는다. 현재 Help에는 대형 저장소 처리와 버전 이력 등 제약도 있으므로 중요한 기준 산출물은 기존 Git 저장소에 남긴다.

## 4. v0와 관리 앱 플랫폼은 언제 더 적절한가

### v0: 기존 저장소에서 실행·테스트·PR까지 웹 작업환경 하나로

[실제 템플릿 갤러리](https://v0.app/templates) / [현재 가격](https://v0.app/pricing)

현재 공식 문서는 기존 공개·비공개 GitHub 저장소와 모노레포 import, 원본 저장소 작업 브랜치, 실행 가능한 개발 환경, 브라우저 조작, 터미널 테스트, PR을 제공한다. Design Systems 2.0은 기존 컴포넌트·토큰·문서도 읽는다. 예전의 새 Next.js 시안 생성기 수준으로 설명하면 안 된다.

현재 가격 페이지는 Free 하루 7 messages, Plus 월 $30/인을 표시한다. 작업량·모델에 따른 사용료와 호스팅 비용은 별개다. 옛 문서의 Premium $20 표를 신규 가격으로 사용하지 않는다.

**선택 조건:** 로컬 개발 대신 기존 GitHub 코드·실행·검증·PR을 클라우드에서 함께 하고, Vercel 연계·권한 부여·추가 비용을 수용하는 경우. 로컬 전용 API와 복수 기기 오프라인 사용 환경까지 repository import만으로 생기는 것은 아니다.

근거: [Git import](https://v0.app/docs/git-import), [브라우저·에이전트 기능](https://v0.app/docs/agentic-features), [Design Systems 2.0](https://v0.app/docs/design-systems-2).

### Appsmith: 관리 화면 자체를 별도 플랫폼으로 대체

[템플릿 보기](https://www.appsmith.com/templates) / [오픈소스 저장소](https://github.com/appsmithorg/appsmith) / [가격](https://www.appsmith.com/pricing)

Community는 무료 자체 호스팅이 가능한 관리 앱 플랫폼이다. 표·폼·조회·API 실행 중심이라면 화면을 전부 직접 만드는 부담을 줄일 수 있다. 하지만 기존 앱을 검사하는 플러그인이 아니라 **새 관리 UI와 플랫폼을 운영하는 선택**이다. 전문 편집기·PWA·노드 작업공간까지 같은 틀로 강제할 때는 적합성이 낮아진다.

### 나머지 후보를 우선하지 않은 이유

| 후보 | 확인한 강점 | 더 적절해지는 조건 / 현재 제약 |
| --- | --- | --- |
| Lovable | 코드 ZIP import, 디자인 시스템 검사·재시도, 브라우저 테스트 | 새 앱을 DB·배포까지 같은 플랫폼에서 시작할 때. 기존 GitHub 원본 직접 import와 ZIP→신규 프로젝트·저장소는 다름 |
| MagicPath | 기존 코드 맥락을 이용하는 캔버스·코드 인계 | 시각 작업공간을 별도로 두고 싶을 때. 실제 제품의 기능 회귀 검증 전체를 대신하지는 않음 |
| Pencil | 로컬 .pen 파일, IDE/MCP, 페이지를 편집 레이어로 가져오기 | 로컬 파일과 Git 중심 캔버스가 중요할 때. 가져온 웹페이지의 JS 상호작용 보존·지속 자동 동기화는 별개 |
| Superdesign | 코드 맥락·디자인 시스템 기반 시안 분기·페이지 흐름 | 여러 시각 방향 탐색이 주업무일 때. 옛 오픈소스 IDE 확장과 현행 cloud+skill/CLI는 구분 |
| Retool | 2026-10-28 React AI app builder GA, React import·운영·권한 통합 | 조직용 관리 앱 플랫폼이 필요할 때. 현재 Git source control·자체 호스팅·BYO AI key는 Enterprise 항목 |

근거: [Lovable import](https://lovable.dev/free-import), [Lovable GitHub](https://docs.lovable.dev/integrations/github), [MagicPath GitHub](https://www.magicpath.ai/documentation/features/work-with-github), [Pencil Design↔Code](https://docs.pencil.dev/design-and-code/design-to-code), [Superdesign 현행](https://superdesign.dev/blog/ai-ui-generator-exports-code), [Retool GA](https://docs.retool.com/changelog/app-builder-ga), [Retool 가격](https://retool.com/pricing).

## 5. 스킬이 ‘있다’와 ‘작동한다’를 구분한다

설치 여부만으로 실효성을 평가하지 않는다. 다음 연결을 확인한다.

1. **발동:** 해당 작업에서 스킬이 실제로 로딩되었는가. 필요 작업에서 명시적으로 호출했는가.
2. **실행 연결:** 편집 hook·CI 또는 명시적인 완료 절차에 검사 실행이 연결되어 있는가.
3. **읽은 맥락:** 실제 프로젝트의 디자인 시스템과 업무 목적을 읽었는가. 오래된 문서나 과도한 절대 금지 규칙을 따르지 않았는가.
4. **검사 대상:** 소스만 봤는가, 실행된 페이지도 봤는가. 사용자의 실제 작업 상태를 재현했는가.
5. **결과:** 발견 항목과 수정·재검사 결과가 남았는가.

수동 복사로 설치한 Impeccable은 자동 hook을 설치하지 않는다. 현재 공식 설치 경로는 지원하는 에이전트에 hook을 연결하며, 에이전트별 신뢰 승인 절차가 있을 수 있다. 이 승인을 우회하지 않는다. 실제 설정은 사용하는 버전과 설치 방식에 따라 확인한다.

Impeccable의 source detector와 URL/browser detector는 검사 범위가 다르다. 예를 들어 소스 검사만으로 실제 텍스트 대비와 크기의 모든 문제를 판단할 수 없다. 의미상의 정보 위계·그룹화·불필요한 내용은 `critique` 같은 모델 판단 영역과 연결된다. 62개 결정론적 규칙이 모든 UX 문제 62종을 완벽히 보증한다는 뜻은 아니다.

또한 `docs/DESIGN.md`처럼 공식적으로 탐색 가능한 위치를 '루트가 아니므로 로딩 실패'라고 오진하지 않는다. 이전 세션의 수동 검사 보고서가 Git에 없다는 사실도 미실행의 증거가 아니다.

근거: [Impeccable 현재 README](https://github.com/pbakaus/impeccable/blob/main/README.md), [검사 항목별 source/browser/review 구분](https://impeccable.style/slop/), [doctor](https://impeccable.style/docs/doctor/).

## 6. Substack 글을 읽고 얻을 수 있는 것과 없는 것

[Most AI design skills do nothing, but three are worth keeping](https://msukhareva.substack.com/p/most-ai-design-skills-do-nothing)의 본문을 브라우저에서 읽었다. 설치한 스킬이 실제로 발동했는지 확인하고, 역할이 겹치는 미적 지시를 계속 쌓지 말자는 취지는 이번 문제와 관련 있다. 그러나 글의 최종 흐름에는 사용자가 직접 시안을 비교·검수하는 역할이 남는다. 제품 소유자가 디자인에서 손을 떼고 싶다는 요구 전체를 해결하지는 않는다.

인용 연구는 그 자체로 구분해야 한다.

- [SWE-Skills-Bench 최신 v2](https://arxiv.org/abs/2603.15401): 98개 스킬 중 92개에서 통계적으로 유의한 효과가 없었고 평균 pass ratio가 76.6%→76.9%. 글의 49개·1.2% 수치는 이전판에 해당한다.
- [SkillsBench 최신 v4](https://arxiv.org/abs/2602.12670): 87개 과제와 18개 모델·harness 구성에서 curated skills 평균 +16.6 percentage points.
- [WebDev-Skills-Bench](https://arxiv.org/abs/2608.23067): 31개 스킬·50개 프로젝트·1,000개 순차 과제에서 대상 스킬 삽입이 모델별 평균 성과를 낮추고 토큰 비용을 높이는 경우가 보고됨.

이것은 서로 다른 과제·모델·평가 조건의 결과다. **시각적 미감·실제 제품의 정보 위계·사용자 만족도를 직접 비교한 종합 디자인 평가가 아니며, '정확히 세 개만 설치하면 최적'이라는 법칙도 아니다.** 공개 연구를 근거로 해당 프로젝트에서 스킬을 어떻게 사용했는지 추적해야 한다.

## 적용 방향

- 이미 선택한 정상적인 UI 컴포넌트와 업무 동작을 보존한다.
- 올인원 제작 환경이 필요하면 기존 구독과 코드 흐름에 맞는 Claude Design/Code를 우선 선택한다.
- 설치된 스킬은 실행·맥락·소스/브라우저 검사 연결을 먼저 바로잡는다.
- 기존 접근성·브라우저 테스트도 실제 실패 사례를 검사하는지 확인한다. 테스트가 전혀 없다고 추정하지 않는다.
- 사용자는 매번 디자인 규칙을 만들고 스크린샷을 승인하는 담당자가 아니다. 일반적 설계 판단·검사·수정은 개발 작업에 포함한다.

추천 이유는 기능과 현재 작업방식의 적합성이다. 도구의 존재, 실제 사용한 증거, 대상 제품에서 개선된 결과를 각각 따로 기록한다.
