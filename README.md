# Product UI Research

이미 잘 만들어진 제품의 화면, 상호작용, 개발 절차를 재사용해 제품 소유자의 디자인 판단 부담을 줄이는 방법을 조사합니다.

**첫 조사: 2026-11-06 · 상태: 공식 문서와 소스 확인 완료, 대상 제품에 이식한 실행 결과는 아직 없음.**

## 현재 결론 — 기존 UI와 통합 작업환경을 구분

**기존 제품들을 모두 Ant Design Pro로 교체하는 것을 권하지 않습니다.** 이미 쓰는 정상 컴포넌트와 업무 동작을 유지하면서, 설계·시안·코드 인계를 하나로 묶고 싶다면 **Claude Design + Claude Code의 공식 통합 흐름**을 우선 추천합니다. 기존 GitHub 코드 수정·실행·테스트·PR까지 클라우드에서 진행하고 싶다면 **v0**가 대안입니다.

**[최신 결론: 올인원과 실제 스킬 실행 점검](research/2026-11-06-integrated-workflow.md)** · [Claude Design 공식 시연](https://claude.com/product/design) · [제품 UI·코드 인계 예시](https://academy.claude.com/tutorials/using-claude-design-for-prototypes-and-ux)

Ant Design Pro full은 **신규 운영·관리 UI용 완성 템플릿 후보**로 유지합니다. [공식 표 화면](https://preview.pro.ant.design/list/table-list/)의 밀도·열 숨김·상세 패널 동작은 실제 확인했습니다. 하지만 그 사실이 기존 여러 제품의 UI 기반을 모두 교체해야 한다는 근거는 아닙니다.

설치된 디자인 스킬이 실제로 발동하고, 올바른 프로젝트 맥락을 읽으며, 소스와 실행 화면을 검사하도록 연결되어 있는지 별도로 확인해야 합니다. 여러 미적 스킬을 새로 겹쳐 설치하는 것을 현재 해법으로 제시하지 않습니다.

## 읽는 순서

| 문서 | 내용 |
| --- | --- |
| [최신 통합 작업환경·점검 결론](research/2026-11-06-integrated-workflow.md) | Claude Design/Code와 v0, 기존 스택 유지, 스킬 실행 연결, Substack 및 연구 해석 |
| [관리 UI 템플릿과 실제 화면](research/2026-11-06-template-choice.md) | Ant Design Pro full의 화면·동작 확인. 기존 앱 전체의 교체 권고는 최신 문서로 범위 수정 |
| [무료 여부와 기본 UX 실패 방지](research/2026-11-06-cost-ux-patterns.md) | MIT 비용 조건, 로그 나열·시각적 위계·과밀 화면의 UX 명칭, 개발자가 검증할 화면 계약, 관리 외의 기본형 |
| [첫 결론과 적용 방향](research/2026-11-06-decision.md) | 초기 조사 기록. 현재 템플릿 선택은 위 문서가 대체함 |
| [완성된 관리 UI 비교](research/framework-evidence.md) | React-admin/Atomic CRM, Refine, Ant Design Pro, Cloudscape의 실제 코드·상태 처리·라이선스·한계 |
| [설계에서 구현까지의 과정 비교](research/process-evidence.md) | Design OS, Superdesign, Agent OS, OOUX/ORCA의 산출물·사용자 개입·검증 범위 |

영문 근거 문서는 공식 문서와 공개 저장소를 직접 읽은 조사 기록입니다. 한국어 결론은 그 사실을 바탕으로 한 선택과 제안을 구분해 설명합니다.

## 직접 확인한 구현

- [Ant Design Pro 전체 소스](https://github.com/ant-design/ant-design-pro/tree/42f2cb1d303380909ea04c73b5e60679d09c321a) — 신규 관리 UI의 완성 템플릿 후보.
- [React-admin E-commerce 전체 소스](https://github.com/marmelab/react-admin/tree/67914cd9572336d0926d719d0021f7e1835f799c/examples/demo) — 데이터 관리 흐름을 중심으로 한 대안.

화면 캡처는 공개 데모의 예제 데이터입니다. 실제 브라우저에서 확인한 범위, 소스에서 확인한 범위, 대상 앱에서 추가로 연결할 일을 현재 추천 문서에 구분했습니다.

## 조사에서 유지할 구분

- **확인한 사실:** 문서 또는 소스에서 직접 확인한 내용.
- **판단과 제안:** 확인한 사실을 바탕으로 내린 적용 결정.
- **미검증:** 실제 이식, 사용자 작업, 장시간 갱신, 성능 측정으로 확인해야 하는 내용.

앞으로의 논의는 이 저장소의 결론과 근거를 갱신합니다. 새 후보를 더하는 경우에도 기존 후보보다 어떤 판단과 구현 부담을 줄이는지 기록합니다.
