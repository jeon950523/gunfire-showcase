# Validation — 무엇을 확인하는가

## 목적

포트폴리오 공개본은 내부 테스트 코드와 전체 실행 로그를 재배포하지 않습니다. 대신 시스템이 어느 행동 경계까지 연결되었는지를 설명합니다.

## 검증 범위

| 범위 | 확인하려는 경계 |
| --- | --- |
| Broad Tactical Depth | X/Y 이동이 사선 회피·엄폐 우회·거리 조절로 읽히는가 |
| Tactical Search | 중단/재개가 Reveal 진행을 보존하고 reroll이 되지 않는가 |
| Backpack / Carry | Grid, 회전, 무게, 장착 슬롯 제약이 일관되는가 |
| Loot Ownership | 전리품, 사망 캐시, 이동/회수 책임이 중복되지 않는가 |
| Weapon Progression | Part Grade, Core Grade Average, Weapon Tier와 승급 선택의 책임이 분리되는가 |
| Gunsmith | 호환성·Preview·Commit과 시각 반영이 같은 작업 흐름으로 닫히는가 |
| Combat | 관통 규칙, 총격 방향, Recoil/Bloom, 엄폐와 공간 전술이 분리된 책임으로 작동하는가 |

## Current Authority Note

공개 검증 기준은 [GAME_DESIGN_SSOT_PUBLIC.md](GAME_DESIGN_SSOT_PUBLIC.md)의 현재 구현/진행 상태를 따릅니다. P4.0 Police Station은 Functional Integration을 유지하되 Camera Comfort 관련 User Play Correction이 열린 상태입니다.

## Police Station Evidence Boundary

Police Station은 여러 시스템을 따로 나열하는 대신 실제 탐사 흐름에서 함께 확인하는 Production Vertical Slice입니다.

```text
공간 진입
→ 전투와 위치 선택
→ Tactical Search
→ Loot 소유권과 가방 제약
→ 귀환 후 무기 조립/조율 판단
```

## 공개 상태

- 구현·검증: 위 기능 경계의 Runtime/Validation 연결
- 폴리싱 중: 플레이어가 빠르게 읽을 수 있는 UI, Feedback, 환경/사운드 표현
- Capture Pending: 공개 허가가 확인된 GIF·영상·스크린샷만 추가

비공개: 전체 Unity 프로젝트, 실제 소스, 상세 테스트 fixture, 내부 운영 문서 및 전체 로그.


