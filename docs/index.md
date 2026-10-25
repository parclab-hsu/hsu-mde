---
hide:
  - navigation
---

# Manufacturing Deformation Engine (MDE)

<span class="mde-badge">연구개발 진행 중</span> · **한성대학교 PARC Lab** · 기준일 2026-10-24

MDE는 로봇이 물체를 **누르고 쥘 때 물체가 어떻게 변형되고, 무엇이 남는지**를 계산하는 시뮬레이션 엔진입니다.
NVIDIA Isaac Sim 위에서 로봇 손의 동작과 함께 돌며, 소재별 물성 Profile을 바꾸는 것만으로 같은 동작에서 서로 다른
변형·자국을 만들어 냅니다. 이 사이트는 지금까지의 **시뮬레이션 실험 결과**(영상·이미지·접촉력·관절 토크)를 공개합니다.

<video class="mde-video" src="media/cup-quick.mp4" poster="media/cup-quick.jpg" controls muted loop playsinline></video>

<p style="text-align:center"><small><b>대표 데모</b> — Allegro Hand가 종이컵을 빠르게 쥐고 들었다가 놓쳐 떨어뜨리는 4.8 s 장면(실제 시간 재생). 스텝마다 계산 시간을 함께 기록했습니다 → <a href="demo/">대표 데모</a></small></p>

## 실험

<div class="grid cards" markdown>

-   :material-timer-outline: **[대표 데모 — 빠르게 쥐었다 놓치기](demo.md)**

    ---

    1/30 s 스텝으로 쥐기·들기·놓치기·낙하. 컵 높이·쥐는 힘·마찰 여유와 스텝당 계산 시간(실시간성). CSV 내려받기.

-   :material-gesture-tap: **[소재별 손가락 가압](materials.md)**

    ---

    같은 손, 같은 동작으로 소재 5종(실리콘·엘라스토머·연질 폼·고밀도 폼·점토) 패드를 누른 결과. 눌린 깊이와 손을 뗀 뒤 남은 자국.

-   :material-cup-outline: **[종이컵 쥐기](cup.md)**

    ---

    탁자 위 종이컵을 감싸 쥐고 들어 올린 뒤 더 세게 쥐었다 풀기. 손가락별 접촉력과 컵 테두리의 타원 변형.

-   :material-cup-water: **[플라스틱 컵 쥐기](plastic-cup.md)**

    ---

    같은 동작으로 투명 PET 컵을 쥐기. 빈 컵·물 1/3·물 2/3 비교, 종이컵보다 1/3 이하의 힘으로 더 찌그러진다. 컵 크기 9·16·20·24 oz 비교. CSV.

-   :material-bottle-soda-outline: **[PET 물병 쥐기](bottle.md)**

    ---

    500 ml 생수병을 빈 병·물 1/3·물 2/3·가득(마개 닫음/엶)으로 쥐기. 몸통은 PET 컵보다 14배 단단하다. CSV.

-   :material-movie-open-outline: **[데모 영상](videos.md)**

    ---

    모든 실험을 매 스텝 다시 찍은 영상: 장면 + 접촉력·변형·관절 토크 그래프, 네 방향, 회전 카메라, 단계를 맞춘 비교 영상.

-   :material-clipboard-check-outline: **[추정값·힘 점검](check.md)**

    ---

    추정값(옆벽 강성·벽 두께·질량·마찰)을 공개 문헌과 대조하고, 계산된 힘·관절 토크의 한계를 정리.

-   :material-chart-line: **[관절 토크](torque.md)**

    ---

    각 실험에서 손가락 관절에 걸린 토크와 Allegro Hand 관절 한계(0.7 N·m) 비교. CSV 내려받기.

</div>

!!! warning "결과를 읽을 때"
    - 모든 결과는 **시뮬레이션**입니다. 실물 시편·실제 로봇으로 시험한 값이 아닙니다.
    - 소재 물성은 문헌·제품 자료에서 잡은 **잠정값**이며 실측 보정 전입니다. 특정 제품의 성능 예측으로 쓰지 마십시오.
    - 관절 토크는 관절 센서로 잰 값이 아니라, 시뮬레이션의 접촉력에서 **계산한 값**입니다(종이컵·소재 가압은 법선력만, PET 컵·물병은 들고 있는 동안 무게를 받치는 마찰도 포함).
    - 로봇 손은 Isaac Sim 5.0에 포함된 Allegro Hand(Wonik Robotics) 시뮬레이션 모델입니다.

## 개발 단계

| 단계 | 범위 | 현황 |
|---|---|---|
| v0 기준선 | 하중–변형 기준 모델 재현 | 완료 |
| v1 탄성·항복 | 가압·파지 시의 변형과 항복 | 모델 구현, 실측 보정 준비 |
| v2 소성·잔류·구조 | 영구변형, 얇은 벽 용기 | 일부 구현 |
| v3 이력·마모 | 장기 사용 상태·마모·공차 변화 | 계획 |

MDE는 [Robot RFM 데이터팩토리 과제](https://parclab-hsu.github.io/projects/manufacturing-data-factory-rfm/)의
Manufacturing Deformation Engine 개발과 연계됩니다. 연구실 소개와 다른 과제는 [PARC Lab 홈페이지](https://parclab-hsu.github.io/)에 있습니다.
