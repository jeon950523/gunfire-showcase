# Weapon Design — Platform을 완성하는 과정

## 핵심 원칙

> 총기는 완제품 드랍을 교체하는 슬롯이 아니라, 파츠를 발견하고 조립·조율하며 숙련시키는 플랫폼입니다.

## Platform과 Part Identity

Platform은 같은 DPS 값으로 수렴하지 않는 운용 정체성입니다. 각 파츠도 고정 장단점을 가진 Identity를 보존합니다.

```text
Part Identity       = 해당 파츠가 하도록 설계된 역할
Precision Quality   = 그 역할을 얼마나 정교하게 수행하는가
```

예를 들어 CQB Barrel의 Precision을 높여도 장거리 Barrel이 되지는 않습니다. Precision은 Trade-off를 지우는 수치가 아니라 동일한 Identity 내부의 품질입니다.

## Completion과 Tier 1–5

핵심 파츠의 Precision을 가중해 무기 Completion을 계산합니다. 이 결과가 Tier 1–5라는 ‘현재 조립·조율 단계’를 만듭니다.

- 랜덤 드랍 색상이나 Affix가 Tier를 결정하지 않습니다.
- T2–T5 승급은 세 가지 조율 방향 가운데 한 가지를 선택합니다.
- 선택은 해당 Weapon Instance에 귀속되어 무기의 운용 이력을 만듭니다.
- 무한한 상위 색상 등급을 추가하지 않습니다.

## Precision Tuning

조율은 파괴·하락·0상승을 전제로 하지 않습니다. 좋은 파츠의 가치는 ‘무작위 실패 회피’가 아니라 시간, 재료, 고급 Capability를 절약하며 원하는 완성도에 더 빨리 도달하게 만드는 데 있습니다.

## Mastery와 Ammo

| 성장 축 | 책임 |
| --- | --- |
| Weapon Tier | 한 자루의 조립·조율 완성 단계 |
| Platform Mastery | 플랫폼을 오래 운용한 영구 숙련 |
| Ammo Tier | Armor 대응력과 운용 판단 |
| Research Capability | 제작·보급처럼 시스템 접근성을 여는 범위 |

이 축을 분리하면 ‘무기 Tier만 높으면 모든 문제를 해결한다’는 단일 성장선이 되지 않습니다.

## Gunsmith UX

조립은 Slot → Compatibility → Preview → Delta 확인 → Commit 순서를 따릅니다. Preview는 외형, 성능, Completion/Tier 변화를 함께 보여 주어야 하며, Replace/Tune/Detach도 동일한 작업 맥락에 놓입니다.

이 공개 문서는 UX 원칙과 결과만 설명합니다. 실제 구현 코드와 전체 파츠 데이터는 공개하지 않습니다.


