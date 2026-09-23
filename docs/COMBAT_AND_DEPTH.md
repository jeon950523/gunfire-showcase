# Combat and Depth — Side View의 전술 공간

## Broad Tactical Depth

Gunfire의 Side View는 1차원 통로가 아닙니다. 캐릭터와 무기의 옆모습 가독성을 유지하면서도 X/Y 이동을 전투 판단에 사용합니다.

| 전술 행동 | Y축이 만드는 선택 |
| --- | --- |
| 원거리 사격 회피 | Commit된 사선 밖으로 이동 |
| 엄폐 활용 | 차량·기둥·장애물을 위/아래로 우회 |
| 근접 위협 대응 | 돌진·광역 경고를 피해 거리 재조정 |
| 공격 기회 | 측면 각도·안전한 발사선 확보 |
| 위기 탈출 | 포위 구도에서 이탈 경로 확보 |

## Gun Feel: Recoil과 Bloom

지속 사격의 부담을 Recoil 하나로만 처리하지 않습니다.

```text
Final Shot Direction
= Aim
+ Mechanical Recoil
+ Sustained-fire Dispersion
```

Tap/First Shot, Short Burst, Long Full Auto가 서로 다른 운용 판단을 만들도록 Recoil과 Bloom/Recovery를 분리합니다. 플레이어가 수직 반동을 보정해도 장시간 자동 사격이 완전한 Laser가 되지 않게 합니다.

## Armor / Ammo의 가독성

Armor Class 1–6과 Ammo Tier 1–5의 기본 관통은 결정적 표로 읽힙니다. 숨은 확률표 대신 필요한 준비와 위험을 예측하게 하며, Armor 내구도와 Coverage는 별도 책임으로 유지합니다.

## 구현/폴리싱 경계

전투 공간, 엄폐, 탄도, 조준·반동·분산, 적 전술 행동의 핵심 연결은 구현·검증 범위입니다. 총격/피격 피드백, 환경 밀도, 시각·사운드 표현은 현재 폴리싱 중심 영역입니다.


