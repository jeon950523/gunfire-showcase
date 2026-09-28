# Gunfire — 2D PvE Tactical Loot RPG Showcase

> **2D/2.5D Side View의 총격·탐색·파츠 조립을 연결한 PvE Tactical Loot RPG입니다.** 완성 총기를 반복 교체하기보다, 발견한 파츠를 조립·조율해 한 자루의 ‘내 총’을 완성하는 경험을 설계합니다.

## 현재 상태 | Current Status

| 구분 | 상태 |
| --- | --- |
| 핵심 시스템 | **구현 및 검증** — Broad Tactical Depth, Tactical Search, Weapon Platform, Gunsmith, Inventory, Armor/Ammo 규칙 |
| 수직 슬라이스 | **Functional Integration PASS / User Play Correction OPEN** — Police Station에서 전투·수색·루팅·인벤토리·무기 조립·Extraction 흐름 연결, Player-centered Camera / Transition Comfort 교정 중 |
| 프레젠테이션 | **Final Art HOLD** — Camera Comfort 재검증 후 UI·환경·오디오 폴리싱 진행 |
| 캡처 자료 | **Capture Pending** — 공개 가능 범위를 개별 확인한 뒤 GIF·스크린샷을 추가 예정 |

## Core Loop

```text
Base
→ 지역 선택
→ Expedition
→ 전투 · 건물 탐색 · Tactical Search
→ Loot 선별 · 귀환 판단
→ Gunsmith 조립/조율 · 사격장 테스트 · Platform Mastery
→ 다음 Expedition
```

파밍은 단순한 전투력 수치 상승이 아닙니다. 필요한 파츠·탄약·조율 도구에 따라 탐사지와 위험을 고르고, 획득물이 다음 무기 세팅과 출정 목표를 만듭니다.

## 대표 시스템 | Featured Systems

### 1. Side View + Broad Tactical Depth

Side View의 캐릭터·총기 실루엣을 유지하면서 World X/Y를 실제 전술 공간으로 사용합니다. Y축은 장식이 아니라 사선 이탈, 엄폐 우회, 측면 사격각 확보, 거리 조절과 포위 탈출에 쓰입니다. 기본 회피는 무적 대시가 아니라 **Telegraph를 읽고 X/Y 이동으로 위험에서 벗어나는 것**입니다.

### 2. Tactical Search

컨테이너를 클릭하는 즉시 Loot 전부가 공개되지 않습니다. 수색 중에도 위험은 계속되고, 아이템은 순차적으로 발견됩니다. 이동·사격·피격·취소로 수색을 멈출 수 있으며, 중단은 Loot 재추첨 수단이 되지 않습니다. Search 자체가 시간과 안전을 저울질하는 Gameplay입니다.

### 3. Weapon Platform · Part Grade · Tier

- 플랫폼은 고유 운용 정체성을 유지합니다.
- 각 PartInstance는 **Grade 1–5**를 가지며, Grade는 Rarity가 아니라 같은 Part Identity 내부의 완성 품질입니다.
- G1→G5 Upgrade는 실패·하락·파괴 없이 한 단계씩 결정적으로 진행합니다.
- Required Core의 Grade 평균에서 Weapon Tier 1–5가 파생되며, Weapon Tier는 드랍 색상이 아니라 현재 조립 완성 단계입니다.
- 승급 시 세 가지 방향 중 하나를 고르고, 선택은 해당 Weapon Instance에 귀속됩니다.
- Platform Mastery와 Ammo Tier는 별도 성장 축으로 유지됩니다.

### 4. Gunsmith

Weapon-centric UI에서 Slot → 호환 파츠 → Preview → 외형/성능/Completion 변화 확인 → Commit 흐름으로 조립합니다. 보이는 파츠는 실제 무기 레이어에 반영하고, 내부 부품은 조립 맥락을 잃지 않도록 별도 시각화합니다. Replace, Tune, Detach를 한 작업 문맥에서 다룹니다.

### 5. Light Tetris Inventory + Weight

필드 인벤토리는 단일 Backpack Grid, 무게, 장착/Quick Slot을 함께 사용합니다. Grid와 무게는 서로 다른 제약입니다. 회전 가능한 직사각 아이템과 전리품 선택은 남길 것·가져갈 것·더 깊이 갈지를 판단하게 하지만, 과도한 관리 노동은 의도적으로 제외합니다.

### 6. Predictable Armor / Ammo

Armor Class 1–6과 Ammo Tier 1–5는 숨은 확률 대신 결정적 규칙으로 읽힙니다.

```text
Ammo Tier ≥ Armor Class      → FULL
Ammo Tier = Armor Class - 1  → PARTIAL
Ammo Tier ≤ Armor Class - 2  → BLOCKED
```

Armor Durability와 Coverage도 별도 책임으로 유지합니다.

## 구현·검증 증거 | Implementation Evidence

Police Station Production Vertical Slice는 다음 흐름을 한 공간에 연결해 확인합니다.

```text
Room / Door / Transition
→ Combat / Cover / Ballistics
→ Tactical Search / Container
→ Loose Loot / Inventory / Carry Weight
→ Weapon Assembly / Gunsmith
```

기능별 Validation은 Broad Tactical Depth, Armor Protection, Carry Weight, Backpack Grid, Loot Ownership/Death Cache, Part Grade Upgrade, Gun Feel, Gunsmith, Weapon Production Closeout을 회귀 확인 범위로 둡니다. 공개본은 내부 테스트 코드나 전체 검증 로그가 아니라, 어떤 행동 경계가 검증 대상인지에 집중합니다.

## Media | Capture Pending

| 예정 자료 | 공개 상태 |
| --- | --- |
| Broad Tactical Depth 전투 | Capture Pending |
| Tactical Search 중단/재개 | Capture Pending |
| Gunsmith 조립·조율 | Capture Pending |
| Police Station 탐사 | Capture Pending |

공개 가능성을 개별 검토하기 전에는 GIF나 스크린샷을 포함하지 않습니다.

## 공개 범위 | Scope

이 저장소는 채용 포트폴리오용 Showcase입니다.

- 포함: 시스템 의도, 플레이 흐름, 구현·검증 경계, 공개 승인된 미디어
- 제외: Unity 프로젝트 전체, 실제 C# 소스 전체, 전체 설계 정본, 내부 운영/인계 문서, 작업 로그, 비공개 자산 및 민감정보

전체 기획의 공개 상위 기준은 [Public Game Design SSOT](docs/GAME_DESIGN_SSOT_PUBLIC.md)에서 확인할 수 있습니다. 세부 시스템 문서는 [docs](docs/)에 정리합니다.


