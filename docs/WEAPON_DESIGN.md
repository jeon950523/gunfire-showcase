# Weapon Design — Platform을 완성하는 과정

## 핵심 원칙

> 총기는 완제품 드랍을 교체하는 슬롯이 아니라, 파츠를 발견하고 조립·성장시키며 숙련해 한 자루의 ‘내 총’을 만드는 플랫폼입니다.

## Platform과 Part Identity

Platform은 같은 DPS 값으로 수렴하지 않는 운용 정체성입니다. 각 파츠도 고정 장단점을 가진 Identity를 보존합니다.

```text
Part Identity   = 해당 파츠가 하도록 설계된 역할
Part Grade 1~5 = 같은 Identity 안에서의 완성 품질
```

CQB Barrel의 Grade를 높여도 Match Barrel이 되지 않습니다. Grade는 Trade-off를 지우는 상위 희귀도가 아니라 동일한 Identity 내부의 품질 단계입니다.

## Part Grade 1–5

PartInstance의 품질은 G1~G5로 표현합니다.

- Grade는 Rarity 색상이 아닙니다.
- G1 → G2 → G3 → G4 → G5로 한 단계씩 성장합니다.
- Upgrade는 실패·하락·파괴·0상승 없이 결정적으로 진행합니다.
- 높은 Grade Field Loot는 여러 Upgrade 비용과 상위 Capability를 건너뛸 수 있어 강한 발견 가치가 됩니다.
- 같은 PartInstance를 Upgrade하므로 Instance Identity와 소유 위치는 유지합니다.

## Core Grade Average와 Weapon Tier 1–5

Required Core가 모두 존재하는 완성 Weapon은 Core Part Grade의 평균으로 현재 Weapon Tier를 계산합니다.

```text
Core Grade Average
→ floor
→ Weapon Tier 1~5
```

Required Core가 빠지면 Tier 1이 아니라 **INCOMPLETE**입니다.

- 랜덤 드랍 색상이나 Affix가 Tier를 결정하지 않습니다.
- Tier는 현재 한 자루의 조립 완성 단계입니다.
- Tier 2~5 최초 달성 시 플랫폼별 고정 3-choice 중 하나를 선택하는 방향을 유지합니다.
- 선택 이력은 해당 Weapon Instance에 귀속됩니다.
- Current Tier가 내려가도 과거 Highest Tier와 선택 이력은 보존합니다.

## Deterministic Upgrade와 Capability

Part Grade Upgrade는 반복 실패 버튼이 아니라 성장 목표입니다.

```text
G1 → G2 / G2 → G3
= Basic Capability

G3 → G4
= Professional Capability

G4 → G5
= Precision Calibration Capability
```

상위 Grade로 갈수록 더 전문적인 재료·공구·Research Capability가 필요합니다. 좋은 Field Loot는 이 과정을 일부 건너뛰게 하므로 파밍 가치와 Upgrade 가치가 함께 유지됩니다.

## Mastery와 Ammo

| 성장 축 | 책임 |
| --- | --- |
| Part Grade | 각 PartInstance의 품질 단계 |
| Weapon Tier | 한 자루의 Core 조립 완성 단계 |
| Tier Choice | 해당 Weapon Instance의 성장 이력 |
| Platform Mastery | 플랫폼을 오래 운용한 영구 숙련 |
| Ammo Tier | Armor 대응력과 운용 판단 |
| Research Capability | 제작·보급·상위 Grade Upgrade 접근성 |

이 축을 분리하면 ‘무기 Tier만 높으면 모든 문제를 해결한다’는 단일 성장선이 되지 않습니다.

## Gunsmith UX

조립은 Slot → Compatibility → Preview → 외형/성능/Core Grade/Tier 변화 확인 → Commit 순서를 따릅니다. 보이는 파츠는 실제 무기 레이어에 반영하고, 내부 부품은 조립 맥락을 잃지 않도록 내부도식과 Highlight로 표현합니다.

Part 선택 상태에서는 Replace / Upgrade / Detach를 같은 작업 맥락에서 다룹니다.

이 공개 문서는 UX 원칙과 현재 기획 결과만 설명합니다. 실제 구현 코드와 전체 파츠 데이터는 공개하지 않습니다.
