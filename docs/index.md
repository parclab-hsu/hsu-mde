---
hide:
  - navigation
---

# Manufacturing Deformation Engine (MDE)

<span class="mde-badge">연구개발 진행 중</span> · **한성대학교 PARC Lab** · 기준일 2026-10-29

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

    같은 동작으로 투명 PET 컵을 쥐기. 빈 컵·물 1/3·물 2/3 비교, 컵 크기 9·16·20·24 oz 비교. 옆벽 강성은 문헌 범위의 추정값. CSV.

-   :material-bottle-soda-outline: **[PET 물병 쥐기](bottle.md)**

    ---

    500 ml 생수병을 빈 병·물 1/3·물 2/3·가득(마개 닫음/엶)으로 쥐기. 마개를 닫으면 병 안 압력이 오르고 벽이 덜 들어간다. CSV.

-   :material-movie-open-outline: **[데모 영상](videos.md)**

    ---

    모든 실험을 매 스텝 다시 찍은 영상: 장면 + 접촉력·변형·관절 토크 그래프, 네 방향, 회전 카메라, 단계를 맞춘 비교 영상.

-   :material-scale-balance: **[NVIDIA Newton과 비교](newton.md)**

    ---

    오픈소스 GPU 물리 엔진 Newton(v1.7.0)과 MDE의 역할·대상·영구 변형·찢김 판정·연동 방식 비교. Newton은 움직임과 힘, MDE는 물체에 남는 것.

-   :material-clipboard-check-outline: **[추정값·힘 점검](check.md)**

    ---

    추정값(옆벽 강성·벽 두께·질량·마찰)을 공개 문헌과 대조해 고치고, 힘·관절 토크 계산을 손본 전후 비교와 남은 한계.

-   :material-chart-line: **[관절 토크](torque.md)**

    ---

    각 실험에서 손가락 관절에 걸린 토크와 Allegro Hand 관절 한계(0.7 N·m, Isaac Lab 설정 0.5 N·m) 비교. CSV 내려받기.

</div>

## Mission — 강화학습

Allegro Hand가 과제(Mission)를 강화학습(PPO)으로 배운 결과입니다. 같은 장면 수백–1024개를 GPU 한 장에서 동시에 돌려 학습했고,
물체의 눌림·자국·금·찢김·늘어남과 손끝 패드의 눌림은 MDE가 판정합니다.

<div class="grid cards" markdown>

-   :material-egg-outline: **[구슬·달걀·젤리 집기](rl-grasp.md)**

    ---

    지름 16 mm 유리구슬, 달걀(60 g), 젤리를 집어 10 cm 들기. 받침 위 구슬 128/128·달걀 127/128(금 0회), 탁자 위 구슬 127/128,
    눕힌 달걀 128/128(금 0.8 %), 젤리 128/128(찢어짐 1.6 %).

-   :material-hand-back-right-outline: **[수건 접기](towel.md)**

    ---

    1024개 병렬 환경에서 학습. 엄지–검지 끝이 모서리를 사이에 두고 맞닿아 집도록 고친 뒤 다시 학습해 1번 접기 127/128회 1.37 s,
    가장 빠른 1번 접기 128/128회 0.87 s(찢김 0회). 수건은 MDE 천 모델 — 집은 자리·접힘 오차·늘어남·찢김을 MDE가 냅니다. 2번 접기는 고친 집기로 아직 못 함.

-   :material-hand-back-left-outline: **[수건 집기 — 뭉툭한 손끝](towel-pick.md)**

    ---

    집는 자리·방법을 정하지 않고 1024개 병렬 환경에서 학습. 천이 두 패드 사이에 실제로 끼어야 잡힌다(MDE 접촉 집기·좌굴).
    엄지–검지 끝이 천을 사이에 두고 붙어 들어 올림 85 %, 흔들어도 유지 88 %. 추가 학습으로 끝단 15 mm 안에서 집기 71 %(5 %에서). 여러 손가락 집기는 여섯 번 학습해 모두 한 쌍으로 끝남 — 이 조건에서는 한 쌍이 최적이라는 결론과 실패·찢김 영상·원인을 공개.

-   :material-fridge-outline: **[가전 문 열기](rl-door.md)**

    ---

    냉장고·오븐형 전자레인지·식기세척기·드럼세탁기의 손잡이를 쥐고 문 열기. 연 횟수 128/128·128/128·128/128·124/128
    (스크립트 2·23·123·14). 손끝 패드 눌림·영구변형과 냉장고 문 패킹은 MDE가 냅니다.

</div>

!!! warning "결과를 읽을 때"
    - 모든 결과는 **시뮬레이션**입니다. 실물 시편·실제 로봇으로 시험한 값이 아닙니다.
    - 소재 물성은 문헌·제품 자료에서 잡은 **잠정값**이며 실측 보정 전입니다. 특정 제품의 성능 예측으로 쓰지 마십시오.
    - 관절 토크는 관절 센서로 잰 값이 아니라, 시뮬레이션의 접촉력에서 **계산한 값**입니다(소재 가압은 법선력만, 컵·물병은 들고 있는 동안 무게를 받치는 마찰도 포함).
    - 로봇 손은 Isaac Sim 5.0에 포함된 Allegro Hand(Wonik Robotics) 시뮬레이션 모델입니다.

## 설치와 예제 실행

MDE 소스는 공개하지 않습니다. **GitHub 저장소 주소는 [kblee@hansung.ac.kr](mailto:kblee@hansung.ac.kr)로 요청해
허가받은 분들에게만 알려 드립니다.** 요청 메일에 소속, 사용 목적, GitHub 계정을 적어 주시면, 허가 시 저장소 초대와 함께
상세 설치 가이드(저장소의 `docs/INSTALL.md`)를 안내합니다. 받은 소스와 문서는 제3자에게 전달하거나 공개하지 않는 조건입니다.

**필요한 환경**

| 항목 | 내용 |
|---|---|
| OS | Ubuntu 22.04 |
| GPU | NVIDIA RTX 계열, VRAM 12 GB 이상 (검증: RTX 5080 16 GB) |
| 소프트웨어 | NVIDIA driver, Docker + NVIDIA Container Toolkit, Python 3.10 이상 |
| 시뮬레이터 | NVIDIA Isaac Sim 5.0.0 · Isaac Lab 2.2.1 — host에 설치하지 않고 Docker 컨테이너로 실행 |
| 디스크 | 100 GB 이상 (컨테이너 이미지 약 50 GB) |

**설치 순서**

1. **Host 준비** — NVIDIA driver, Docker, NVIDIA Container Toolkit을 설치하고 컨테이너 안에서 GPU가 보이는지 확인합니다.
2. **코어 설치** — 저장소를 받아 Python 패키지로 설치하고 시험을 돌립니다. 코어 엔진은 GPU 없이 동작합니다.
3. **Isaac 준비** — Isaac Sim 5.0.0 이미지를 받고, 로봇 손 모델을 한 번 내려받고, Isaac Lab 이미지를 만듭니다(1회, 네트워크 필요).

**예제** — 순서대로 실행하면 설치의 각 층을 하나씩 확인할 수 있습니다. 기대 결과는 저장소에 함께 들어 있습니다.

| 예제 | GPU | 이 사이트의 해당 결과 |
|---|---|---|
| 패드 반복 가압 (코어 엔진만) | 불필요 | — |
| PET 물병 쥐기 (Isaac Sim 장면) | 필요 | [PET 물병 쥐기](bottle.md) |
| 손가락 가압 · 소재 비교 | 필요 | [소재별 손가락 가압](materials.md) |
| 강화학습 — 수건 접기 (1024개 병렬 환경) | 필요 | [수건 접기](towel.md) |

강화학습 예제는 학습부터 시작합니다(정책 하나에 약 10–60분). 학습·평가·영상 만들기를 각각 명령 한 줄로 실행합니다.

## 개발 단계

| 단계 | 범위 | 현황 |
|---|---|---|
| v0 기준선 | 하중–변형 기준 모델 재현 | 완료 |
| v1 탄성·항복 | 가압·파지 시의 변형과 항복 | 모델 구현, 실측 보정 준비 |
| v2 소성·잔류·구조 | 영구변형, 얇은 벽 용기 | 일부 구현 |
| v3 이력·마모 | 장기 사용 상태·마모·공차 변화 | 계획 |

MDE는 [Robot RFM 데이터팩토리 과제](https://parclab-hsu.github.io/projects/manufacturing-data-factory-rfm/)의
Manufacturing Deformation Engine 개발과 연계됩니다. 연구실 소개와 다른 과제는 [PARC Lab 홈페이지](https://parclab-hsu.github.io/)에 있습니다.
