# Product UI Research

이미 잘 만들어진 제품의 화면, 상호작용, 개발 절차를 재사용해 제품 소유자의 디자인 판단 부담을 줄이는 방법을 조사합니다.

**첫 조사: 2026-11-06 · 상태: 공식 문서와 소스 확인 완료, 대상 제품에 이식한 실행 결과는 아직 없음.**

## 현재 결론 — 완성 템플릿 하나를 선택

**운영·관리 앱의 개발 중 기본 화면으로 Ant Design Pro의 `full` 템플릿 하나를 추천합니다.** 목록·상세·폼·설정 등 같은 제품에 들어 있는 페이지를 사용하고, 업무 필드와 API를 연결하는 방식입니다. 앞선 Atomic CRM 화면 부분 이식 추천은 이 목적의 우선안에서 내렸습니다.

**[실제 표 화면 열기](https://preview.pro.ant.design/list/table-list/)** · **[기본 입력 화면](https://preview.pro.ant.design/form/basic-form/)** · **[추천 수정 이유와 실제 캡처](research/2026-11-06-template-choice.md)**

공식 공개 데모에서 컴팩트 밀도, 보조 열 숨김, 목록에서 상세 패널 열기를 직접 확인했습니다. 비교 대안은 [React-admin 공식 E-commerce 앱](https://marmelab.com/react-admin-demo/) 한 개입니다. 두 제품의 화면을 혼합하는 제안은 아닙니다.

후보의 문서와 코드에 대한 기존 조사는 아래에 보존합니다. Design OS 등 별도 생성·검토 도구는 현재 기본 채택안에 추가하지 않습니다.

## 읽는 순서

| 문서 | 내용 |
| --- | --- |
| [현재 추천과 시안 링크](research/2026-11-06-template-choice.md) | 한 템플릿으로 채택할 대상, 직접 확인한 화면과 동작, 이전 추천 수정, 설계 문서의 의존 관계 |
| [첫 결론과 적용 방향](research/2026-11-06-decision.md) | 초기 조사 기록. 현재 템플릿 선택은 위 문서가 대체함 |
| [완성된 관리 UI 비교](research/framework-evidence.md) | React-admin/Atomic CRM, Refine, Ant Design Pro, Cloudscape의 실제 코드·상태 처리·라이선스·한계 |
| [설계에서 구현까지의 과정 비교](research/process-evidence.md) | Design OS, Superdesign, Agent OS, OOUX/ORCA의 산출물·사용자 개입·검증 범위 |

영문 근거 문서는 공식 문서와 공개 저장소를 직접 읽은 조사 기록입니다. 한국어 결론은 그 사실을 바탕으로 한 선택과 제안을 구분해 설명합니다.

## 직접 확인한 구현

- [Ant Design Pro 전체 소스](https://github.com/ant-design/ant-design-pro/tree/42f2cb1d303380909ea04c73b5e60679d09c321a) — 현재 기본 추천.
- [React-admin E-commerce 전체 소스](https://github.com/marmelab/react-admin/tree/67914cd9572336d0926d719d0021f7e1835f799c/examples/demo) — 데이터 관리 흐름을 중심으로 한 대안.

화면 캡처는 공개 데모의 예제 데이터입니다. 실제 브라우저에서 확인한 범위, 소스에서 확인한 범위, 대상 앱에서 추가로 연결할 일을 현재 추천 문서에 구분했습니다.

## 조사에서 유지할 구분

- **확인한 사실:** 문서 또는 소스에서 직접 확인한 내용.
- **판단과 제안:** 확인한 사실을 바탕으로 내린 적용 결정.
- **미검증:** 실제 이식, 사용자 작업, 장시간 갱신, 성능 측정으로 확인해야 하는 내용.

앞으로의 논의는 이 저장소의 결론과 근거를 갱신합니다. 새 후보를 더하는 경우에도 기존 후보보다 어떤 판단과 구현 부담을 줄이는지 기록합니다.
