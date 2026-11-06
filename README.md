# Product UI Research

이미 잘 만들어진 제품의 화면, 상호작용, 개발 절차를 재사용해 제품 소유자의 디자인 판단 부담을 줄이는 방법을 조사합니다.

**첫 조사: 2026-11-06 · 상태: 공식 문서와 소스 확인 완료, 대상 제품에 이식한 실행 결과는 아직 없음.**

## 현재 결론

운영·관리 화면의 우선 조사 대상은 **React-admin / ra-core 생태계**입니다. 구체적인 참고 구현으로 **Atomic CRM의 완성된 화면 흐름과 Shadcn Admin Kit**, 그 제품에 포함된 개발 절차를 선택했습니다. 목록, 필터, 선택, 상세, 편집, 복귀, 갱신을 연결한 코드를 함께 가져오는 접근입니다. [선정 근거](research/2026-11-06-decision.md)

현재 Atomic CRM은 React + Shadcn Admin Kit + Supabase 기반입니다. 기본 Material UI 화면을 제공하는 React-admin과는 표현 계층이 다릅니다. 다른 도메인에 적용하려면 데이터와 업무의 대응 관계를 정리하고 연결해야 합니다. [코드·기능 비교](research/framework-evidence.md)

**Design OS는 준비와 소스 인계 과정이 가장 구체적인 후보**였습니다. 다만 상위 과정에서 UI를 새로 생성하고 사용자의 디자인 선택을 요구합니다. 기존 완성품을 그대로 쓰고 싶은 요구에 이것만 설치하는 것으로 답할 수는 없습니다. [과정 비교](research/process-evidence.md)

여러 제품의 정보설계부터 실행 성능까지 맡겨도 되는 범용 무인 디자인 시스템은 이번 조사에서 검증하지 못했습니다. 장문 문서 편집기처럼 작업 성격이 다른 화면에는 별도의 기준 구현이 필요합니다.

## 읽는 순서

| 문서 | 내용 |
| --- | --- |
| [첫 결론과 적용 방향](research/2026-11-06-decision.md) | 한국어 요약, 후보 선택 이유, 화면 준비와 기능 확장 방식, 기존 문서 처리, 다음 확인 항목 |
| [완성된 관리 UI 비교](research/framework-evidence.md) | React-admin/Atomic CRM, Refine, Ant Design Pro, Cloudscape의 실제 코드·상태 처리·라이선스·한계 |
| [설계에서 구현까지의 과정 비교](research/process-evidence.md) | Design OS, Superdesign, Agent OS, OOUX/ORCA의 산출물·사용자 개입·검증 범위 |

영문 근거 문서는 공식 문서와 공개 저장소를 직접 읽은 조사 기록입니다. 한국어 결론은 그 사실을 바탕으로 한 선택과 제안을 구분해 설명합니다.

## 실제 참고 대상

- [Atomic CRM 소스](https://github.com/marmelab/atomic-crm) · [실행 데모](https://marmelab.com/atomic-crm-demo/) · [제품 전용 개발 절차](https://marmelab.com/atomic-crm/doc/developers/agent-harness/)
- [Shadcn Admin Kit](https://marmelab.com/shadcn-admin-kit/)
- [React-admin 문서](https://marmelab.com/react-admin/) · [전자상거래 데모](https://marmelab.com/react-admin-demo/)
- [Design OS 소스](https://github.com/buildermethods/design-os)

데모 링크 제공은 해당 데모의 성능이나 모든 상호작용을 실측했다는 뜻이 아닙니다. 검사한 소스는 근거 문서에 커밋을 고정해 남겼습니다.

## 조사에서 유지할 구분

- **확인한 사실:** 문서 또는 소스에서 직접 확인한 내용.
- **판단과 제안:** 확인한 사실을 바탕으로 내린 적용 결정.
- **미검증:** 실제 이식, 사용자 작업, 장시간 갱신, 성능 측정으로 확인해야 하는 내용.

앞으로의 논의는 이 저장소의 결론과 근거를 갱신합니다. 새 후보를 더하는 경우에도 기존 후보보다 어떤 판단과 구현 부담을 줄이는지 기록합니다.
