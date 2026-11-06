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

## 7. 지금 살펴본 UI 스킬·검사 도구와 채택 판단

인기나 설치 수는 실제 제품의 UX 개선 효과를 대신하지 않는다. 아래는 현행 소스에서 확인한 기능과 이 작업에 대한 판단이다. 전부 설치하라는 조합이 아니다.

| 도구 | 실제로 하는 일 | 현재 판단 |
| --- | --- | --- |
| **Impeccable** | `critique`의 모델 기반 UX 검토, `detect`의 실행 가능한 소스·URL 검사, 편집 hook. Operate 모드는 업무용 앱의 밀도·익숙한 조작·일관성·비장식적 움직임을 다룸 | 이미 도입했다면 유지. 발동·맥락·검사 연결부터 점검. 단순 미감 프롬프트만 있는 도구로 평가하면 부정확함 |
| **Vercel web-design-guidelines** | 최신 지침을 가져와 코드를 읽고 파일·행 단위로 위반을 보고하도록 하는 스킬 | 코드 리뷰 참고용. 설치만으로 실행되는 결정론적 linter나 브라우저 검사가 아님 |
| **UI UX Pro Max** | 스타일·색·폰트·업종·스택 지식 검색, 디자인 시스템 제안 | 초기 방향 탐색용. 렌더된 화면의 기능·상호작용 검사 대체재가 아니므로 기존 시스템 위에 기본 추가하지 않음 |
| **Hallmark** | 실제 `sloplint`와 렌더 검사, 모델 기반 별도 리뷰를 포함 | 실제 검사기가 있다는 점은 인정. 그러나 현행 Floor 10의 가운데점 메타문자열 금지처럼 강한 일괄 규칙이 있어, 상황별 판단을 원하는 이 요청에는 기본 선택으로 부적합 |
| **AccessLint** | 실제 렌더된 페이지의 접근성 검사, MCP·CLI와 기준 대비 변경 검토 | 접근성 자동화가 없는 프로젝트에 유용. 이미 axe·브라우저 검사가 있다면 중복 여부부터 확인. 의미상의 정보 우선순위·성능을 모두 해결하지 않음 |
| **React Doctor** | React 상태·효과·구조·성능 코드 검사와 CI. `scan <url>`은 Chrome trace 기반 상호작용 성능 분석 | React 앱의 버벅임 원인 분석에 별도 후보. 기본 디자인 스킬과 역할이 다름. 비React 앱 전체를 검사하는 만능 도구는 아님 |

공개 소스: [Impeccable Operate](https://github.com/pbakaus/impeccable/blob/414603bf14c7a344edb466bb1f85690c77ce8b7d/.agents/skills/impeccable/reference/operate.md), [Vercel 스킬](https://github.com/vercel-labs/agent-skills/blob/1a2c79d4e6c4a2283dc2c614b6538cbe1ed5ca62/skills/web-design-guidelines/SKILL.md), [UI UX Pro Max](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill/blob/b7d5353e0130feb8c5574ef1251f8a1db1873ccb/README.md), [Hallmark 현행 규칙](https://github.com/Nutlope/hallmark/blob/407fa689f4a276f2fd389208d271d0fef08f5058/skills/hallmark/SKILL.md), [AccessLint MCP](https://github.com/AccessLint/accesslint/blob/a839ea727447410e8282c3d1da83fc893b42901a/mcp/README.md), [React Doctor](https://github.com/millionco/react-doctor).

### 점검 범위를 실제 실패에 연결하기

- **사용자 화면에 내부 로그·필드를 그대로 나열:** 의미와 업무 목적을 아는 리뷰가 필요하다. 원시 응답을 그대로 렌더하지 않고 사용자용 요약·상태·상세·진단 필드로 나누는 구현이 필요하며, detector만으로 모든 의미상의 오류를 찾는다고 보장하지 않는다.
- **정보가 모두 같은 강조 수준, 불필요한 버튼, 잘못된 묶음:** 모델 기반 critique와 공통 화면 템플릿의 역할이다. 폰트 크기 차이만 검사하는 규칙은 정보 중요도의 옳고 그름까지 판정하지 못한다.
- **넘침·가림·대비·작은 클릭 영역:** 실행된 페이지의 브라우저 검사와 접근성 검사에 연결한다.
- **갱신 후 스크롤·포커스·입력·선택 상태 손실:** 실제 업무 중 갱신을 발생시키는 브라우저 회귀 테스트에서 확인한다. 스크린샷 한 장이나 정적 코드 검사만으로 통과 처리하지 않는다.
- **메뉴를 바꿀 때 단계적으로 버벅임:** 실제 상호작용 trace로 긴 프레임·긴 작업·재렌더·레이아웃 변경을 구분한다. 원인 측정 전 모든 애니메이션이나 React 자체를 원인으로 단정하지 않는다.

Impeccable hook이 검사 결과를 에이전트에 전달하는 것과 CI가 병합을 차단하는 것은 별개다. 또한 수동 `critique` 기본 흐름에는 소유자에게 우선순위를 묻는 절차가 있어, 그것을 그대로 매 변경의 사용자 승인 절차로 확대하면 이 요청의 목적과 어긋난다. 보통의 구현·검사·수정 책임은 개발 작업에 포함하고, 제품 목적이 실제로 모호할 때만 결정이 필요한 질문을 한다.

React Doctor의 runtime scan은 실제 상호작용과 interactive TTY를 요구하므로 모든 사용자 동작을 스스로 재현하는 무인 회귀 테스트와 다르다. trace는 로컬에 남는다고 설명하지만 CLI telemetry는 기본 켜져 있으며 `--no-telemetry`로 끌 수 있다. 실제 LICENSE는 **Modified MIT**로, 일반적인 앱 검사 외에 ML/AI 훈련·개선·평가용 데이터/파이프라인 활용 및 해당 소프트웨어를 기반으로 하는 유료 재판매 등에 추가 허가 조항이 있다. README의 MIT 표기만 보고 무제한 MIT라고 설명하지 않는다.

근거: [runtime trace CLI](https://www.react.doctor/docs/reference/cli-reference#runtime-performance-traces), [실제 라이선스](https://github.com/millionco/react-doctor/blob/9791c32f61fb1477a4f8dd596ff80184ad26b2e3/LICENSE).

## 적용 방향

- 이미 선택한 정상적인 UI 컴포넌트와 업무 동작을 보존한다.
- 올인원 제작 환경이 필요하면 기존 구독과 코드 흐름에 맞는 Claude Design/Code를 우선 선택한다.
- 설치된 스킬은 실행·맥락·소스/브라우저 검사 연결을 먼저 바로잡는다.
- 기존 접근성·브라우저 테스트도 실제 실패 사례를 검사하는지 확인한다. 테스트가 전혀 없다고 추정하지 않는다.
- 사용자는 매번 디자인 규칙을 만들고 스크린샷을 승인하는 담당자가 아니다. 일반적 설계 판단·검사·수정은 개발 작업에 포함한다.

추천 이유는 기능과 현재 작업방식의 적합성이다. 도구의 존재, 실제 사용한 증거, 대상 제품에서 개선된 결과를 각각 따로 기록한다.
