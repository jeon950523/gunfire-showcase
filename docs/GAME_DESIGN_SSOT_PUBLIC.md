# Gunfire — Public Game Design SSOT

> 채용 포트폴리오용 공개 기획 정본입니다. 내부 통합 SSOT의 현재 Authority를 바탕으로, **플레이어 경험·시스템 관계·핵심 의사결정·현재 구현 범위**만 압축해 공개합니다. 세부 밸런스 수치, 내부 작업지시, 테스트 fixture와 전체 구현 코드는 포함하지 않습니다.

## 1. Game Identity

**Gunfire**는 2D/2.5D Side View에서 전투·탐색·수색·총기 조립·귀환을 반복하는 **PvE Tactical Loot RPG**입니다.

플레이어는 봉쇄 도시로 투입된 특수부대원으로 시작해, 추락 이후 호텔을 전초기지로 확보하고 Strategic City Map에서 출정지를 선택합니다. 각 출정에서는 전투와 Tactical Search를 통해 총기·파츠·탄약·방탄장비·재료를 확보하고, 살아서 Extraction해야 전리품을 확정할 수 있습니다.

이 게임의 중심은 더 높은 색상의 완성 총기를 반복 교체하는 것이 아닙니다.

> **좋은 부품을 발견하고, 한 자루의 총을 조립·조율하며, 실제 사용으로 숙련해 ‘내 총’으로 완성하는 경험**을 지향합니다.

## 2. Player Fantasy

플레이어가 느끼길 원하는 핵심 감정은 다음과 같습니다.

- 총을 잘 쏘는 것뿐 아니라 **어떤 탄약·장비·파츠를 준비할지 판단하는 전술성**
- 컨테이너를 더 수색할지, 현재 전리품을 지키고 귀환할지 결정하는 **Risk / Return**
- 같은 총기 플랫폼이라도 파츠 구성과 Grade, Tier 조율에 따라 달라지는 **개인화된 무기 성장**
- 필요한 재료와 장비를 얻기 위해 목적지 자체를 고르는 **목표형 파밍**
- 죽더라도 모든 것을 즉시 영구삭제하기보다 Recovery Expedition을 통해 다시 회수하러 가는 **실패 이후의 선택**

## 3. Core Loop

```text
Hotel Base
→ Strategic City Map에서 Location 선택
→ Loadout / Ammo / Backpack 준비
→ Expedition 진입
→ Combat · Exploration · Tactical Search
→ Weapon / Part / Ammo / Armor / Material 획득
→ 더 깊이 갈지 Extraction할지 판단
→ Extraction 성공
→ Hotel 귀환
→ Gunsmith / Part Grade Upgrade / Research / Facility
→ Shooting Range에서 Build 확인
→ 다음 성장 목표에 맞는 Location 선택
→ 다음 Expedition
```

파밍은 전투력 숫자를 올리는 단일 과정이 아니라, **다음 출정의 목표를 만드는 과정**입니다.

## 4. Core Design Pillars

### 4.1 Side View + Broad Tactical Depth

Side View의 캐릭터·총기 실루엣을 유지하면서 World X/Y를 실제 전술 공간으로 사용합니다.

- X: 전진·후퇴·거리 조절
- Y: 사선 이탈·엄폐 우회·측면각 확보·포위 탈출

기본 회피는 Combat Roll이나 I-frame Dash가 아니라 **Telegraph를 읽고 X/Y 이동으로 공격선에서 벗어나는 것**입니다.

### 4.2 Tactical Search — 수색 자체가 Gameplay

컨테이너를 열었다고 모든 아이템이 즉시 공개되지 않습니다.

```text
Container 접근
→ Search 시작
→ 내부 아이템 순차 Reveal
→ 위험 감지
→ 중단 또는 계속
→ 발견물을 선택해 운반
```

Loot Manifest는 Expedition 생성 시 고정됩니다. Search는 이미 존재하는 결과를 **발견하는 과정**이며, 중단·재개·Save/Load를 Loot reroll 수단으로 사용하지 않습니다.

### 4.3 Weapon Platform · Part Grade · Weapon Tier

총기 본체의 색상 Rarity와 Random Affix를 핵심 성장축으로 사용하지 않습니다.

```text
Weapon Platform
+ Part Identity
+ Part Grade 1~5
+ Core Grade Average
+ Weapon Tier 1~5
+ Tier Promotion Choice
+ Tactical / Derivative Parts
+ Platform Mastery
```

**Part Grade는 Rarity가 아닙니다.** 같은 Part Identity 내부에서 품질이 얼마나 완성되었는지를 나타냅니다. G1→G5 Upgrade는 실패·하락·파괴 없이 한 단계씩 결정적으로 진행하며, 더 높은 Grade의 Field Loot는 업그레이드 비용과 고급 Capability를 건너뛸 수 있는 강한 발견 가치가 됩니다.

Required Core의 Grade 평균에서 현재 Weapon Tier가 파생되고, Tier 승급 선택은 해당 Weapon Instance에 남아 한 자루의 성장 이력을 만듭니다.

### 4.4 Predictable Armor / Ammo

Armor Class와 Ammo Tier의 기본 상호작용은 숨은 확률보다 **예측 가능한 FULL / PARTIAL / BLOCKED** 규칙을 우선합니다.

플레이어는 고방탄 적을 상대할 때 다음을 판단합니다.

- 더 높은 관통 탄약을 준비한다.
- Armor Coverage 밖을 노린다.
- Armor 내구도를 먼저 소모한다.
- 다른 위치와 각도를 만든다.

고티어 탄약이 비장갑 적까지 모든 상황에서 정답이 되지 않도록 탄종 역할을 분리합니다.

### 4.5 Light Tetris Inventory + Weight

필드 Loot 공간은 **Single Backpack Grid + Weight**로 단순화합니다.

Grid와 Weight는 별개의 제약이지만, 탄창별 탄수·리그·Pocket·가방 속 가방처럼 관리 노동이 커지는 구조는 초기 핵심에서 제외합니다.

목적은 정리 자체가 아니라:

> **무엇을 버리고 무엇을 가져갈지 선택하게 만드는 것**

입니다.

### 4.6 Hotel / Research = Capability Progression

호텔은 단순 메뉴가 아니라 플레이어가 직접 확보하고 복구하는 전초기지입니다.

시설과 Research는 Damage +X% 같은 반복 버프보다 다음을 엽니다.

- 더 높은 Grade Upgrade Capability
- 탄약 제작·보급
- 방어구 정비
- 의료·생존 기능
- 정찰 정보
- 특수 분석·외계 기술 연구

Facility, Tool, Research는 서로 다른 역할을 유지합니다.

## 5. Systems Relationship

```text
Strategic Map / Expedition Offer
→ 예상 적·Loot·위험 정보 확인
→ Loadout / Ammo / Backpack 결정
→ Combat / Tactical Search
→ Hidden Manifest의 Loot를 발견
→ Backpack Grid / Weight에서 운반 선택
→ Extraction
→ 정확한 Item Ownership 확정
→ Gunsmith / Grade / Tier / Mastery / Research
→ 부족한 Part·Material·Tool이 다음 Location 목표가 됨
```

이 구조의 핵심은 **성장 메뉴와 출정지가 서로 분리되지 않는 것**입니다. Workbench에서 필요한 재료를 확인하면 다음 파밍 목적지가 만들어지고, 필드에서 발견한 좋은 파츠가 다시 무기 Build의 방향을 바꿉니다.

## 6. World / Faction Direction

초반의 세계는 감염 사태로 붕괴한 봉쇄 도시로 보이지만, 진행하면서 세 전투축이 드러납니다.

- **Infected**: 물량·근접 압박·이동 강제
- **Human Factions**: 총격·엄폐·Armor / Ammo·사격각
- **Alien Remnants**: 비정상적 이동·방향성 방어·새 대응 규칙

스토리는 처음부터 세계의 진실을 설명하기보다 **생존 → 실종 팀원 → 도시의 비밀 → BLACK PROJECT → 지하 외계 구조물** 순으로 확장합니다.

## 7. Key Design Decisions

### 왜 총기 색상 Rarity를 쓰지 않는가

같은 총을 더 높은 색상으로 계속 교체하면 파츠 조립과 총기 애착이 약해집니다. 따라서 Weapon의 가치는 **무슨 파츠가 들어 있고, 각 Part가 어떤 Grade와 역할을 갖는가**에서 만들도록 설계했습니다.

### 왜 Upgrade 실패 RNG가 없는가

총기 성장의 재미를 실패 버튼 반복에서 만들지 않습니다. Upgrade는 확정 성장이고, 비용·Capability·좋은 Field Loot 발견 여부가 성장 속도와 파밍 목표를 만듭니다.

### 왜 Combat Roll이 없는가

Broad Tactical Depth를 실제 전투 공간으로 사용하기 위해 회피를 별도 무적 버튼이 아니라 **공격 Telegraph와 사선, 엄폐, X/Y 이동**에서 만들고자 했습니다.

### 왜 Search가 Loot Quality를 올리지 않는가

Search Skill이 좋은 Loot를 생성하면 수색 속도와 보상 품질의 책임이 섞입니다. Loot는 Location·Depth·Security·Container가 결정하고, Search는 **그 결과를 얼마나 빨리 확인하는가**만 담당합니다.

### 왜 Familiar Location을 반복 방문하는가

매 Run 완전히 다른 Random Maze보다 경찰서·병원·공장 같은 장소의 정체성은 기억되게 하고, Enemy·Loot·Modifier·일부 Route가 달라져 같은 장소에 다시 갈 이유를 만들고자 합니다.

## 8. Current Implementation Scope

### Implemented / Validated Foundation

- Production CSV / Weapon·Part Instance Foundation
- Gunsmith / Assembly UX
- Part Grade 1~5와 Core Grade 기반 Weapon Tier
- Backpack Grid / Weight / Equipment
- Ammo Tier / Armor Class / Durability / Coverage
- Tactical Search / Loot Ownership / Extraction / Death Cache
- 8-direction movement, Sprint, ADS, Crouch, Contextual Vault
- LOW / HIGH Cover와 Human Enemy Perception
- Rifleman / Rusher 전투, Projectile, Recoil / Bloom, 기본 총격 피드백
- Police Station Production Location의 Functional Expedition 흐름

### Current Open Work

Police Station P4.0은 기능 통합은 진행되었지만, 실제 User Play에서 Camera Comfort 문제가 발견되어 **Player-centered Camera + Transition Comfort 교정이 현재 열린 상태**입니다.

- Mouse는 Weapon Aim에만 사용
- Camera는 Player 중심 Follow
- ADS는 작은 Zoom-out만 사용
- 층·대형 구역 이동은 Fade-hidden snap으로 전환

카메라 편안함을 다시 확인하기 전 Final Art Pass를 진행하지 않습니다.

### Planned / Not Claimed as Complete

- AI Runtime / Population Density 추가 교정
- Loot Interaction 가독성 개선
- Final Art / Audio / Presentation Polish
- 후속 Location 및 Story Content 확장

## 9. Detailed Public Documents

- [System Design](SYSTEM_DESIGN.md) — 전체 루프와 공간·지역·파밍 관계
- [Combat and Depth](COMBAT_AND_DEPTH.md) — Side View 전술 공간과 총격 설계
- [Weapon Design](WEAPON_DESIGN.md) — Weapon Platform / Part Grade / Tier / Gunsmith
- [Tactical Search](TACTICAL_SEARCH.md) — 수색·중단·재개·Loot 관계
- [Validation](VALIDATION.md) — 공개 검증 범위와 Evidence Boundary

---

이 문서는 **공개용 상위 기획 기준**입니다. 상세 내부 SSOT, 전체 밸런스 테이블, 구현 코드와 작업 로그는 공개하지 않습니다.
