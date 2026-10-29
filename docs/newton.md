# NVIDIA Newton과 MDE 비교

기준일 2026-10-30 · Newton **v1.7.0**(2026-10-14) 공개 자료 기준 · MDE는 이 사이트의 실험 기준(Isaac Sim 5.0.0 · Isaac Lab 2.2.1)

**Newton**은 NVIDIA·Google DeepMind·Disney Research가 시작하고 Linux Foundation이 관리하는 오픈소스 GPU 물리 엔진입니다.
로봇 학습을 위해 강체·관절체·천·연성체·입자를 빠르게 계산합니다. **MDE**는 로봇이 물체를 누르고 쥘 때 **물체에 무엇이 남는지**
(눌린 깊이, 손을 뗀 뒤 남은 자국과 주름, 누적 이력, 찢김·금 같은 한계 초과)를 소재별로 계산하는 엔진입니다.

두 엔진은 맡는 층이 다릅니다. Newton은 **움직임과 접촉력**을 푸는 물리 엔진이고, MDE는 물리 엔진이 낸 접촉을 받아
**물체 상태의 변화와 그 판정**을 내는 층입니다. 지금 MDE는 Isaac Sim의 PhysX 위에서 돌며, Newton 위에서는 시험하지 않았습니다.

<p style="text-align:center"><b>물리 엔진</b>(Newton 또는 PhysX) — 움직임·접촉력 → <i>접촉 위치·하중(매 스텝)</i> → <b>MDE</b> — 소재 Profile · 변형·누적 이력 · 판정(남은 자국·찢김·한계 초과) → <i>변형된 형상</i> → 물리 엔진</p>

## 한눈에 비교

| 항목 | NVIDIA Newton | MDE (한성대학교 PARC Lab) |
|---|---|---|
| 성격 | 범용 GPU 물리 엔진 (로봇 학습용) | 접촉 변형·잔존 상태·판정 엔진 |
| 주 질문 | 로봇과 물체가 **어떻게 움직이고** 얼마의 힘이 걸리는가 | 접촉 뒤 물체에 **무엇이 남고**, 소재 한계를 넘었는가 |
| 기반 | NVIDIA Warp, OpenUSD | Isaac Sim 5.0.0(PhysX) · Isaac Lab 2.2.1, 코어는 Python |
| 계산 방식 | 9종 solver: MuJoCo Warp, Featherstone, Semi-Implicit, XPBD, VBD(실험), Style3D(천), Implicit MPM, Kamino(실험), Coupled ADMM | 소재·대상별 응답 모델을 교체해 씀(단계별로 개정) |
| 다루는 대상 | 강체·관절체, 천, 연성체, 케이블, 입자·입상체(MPM) | 패드·가스켓, 종이컵·PET 컵·물병 옆벽, 수건(천), 냉장고 문 패킹, 소형 물체(구슬·달걀·젤리) 판정 |
| 영구 변형 | MPM의 소성 상태, 케이블의 굽힘·비틀림 이력(permanent set). 천·연성체(FEM/VBD)의 영구 변형은 공개 자료에서 찾지 못함 | 손을 뗀 뒤 남은 자국, 남은 주름(천), 누적 이력 |
| 손상·찢김 | 찢김·파단·손상 모델은 공개 자료에서 찾지 못함 | 소재 한계를 넘는 늘어남(찢김), 금, 설정한 한계 초과를 매 스텝 판정 |
| 학습용 라벨 | 접촉력·관절 하중 관측(v1.7.0, 실험). 사건 라벨은 공개 자료에서 찾지 못함 | 접촉 개시·해제, 모델상 영구 변형 발생, 한계 초과 이벤트 |
| 소재 값 관리 | solver 별 파라미터 | 소재 Profile: 값마다 단위·허용 범위·출처·확정 여부 |
| 미분 가능 | Featherstone·Semi-Implicit 기본 지원, 그 밖의 solver는 미지원 | 목표로 하지 않음 |
| 병렬 학습 | MuJoCo Warp 기반 대규모 병렬(벤더 수치: MJX 대비 이동 252배, 조작 475배, RTX PRO 6000 Blackwell) | Isaac Lab 병렬 환경에서 판정. 수건 1024개 환경을 GPU 한 장(RTX 5080 16 GB)에서 함께 계산 |
| Isaac Lab 연동 | Isaac Lab 3.0(베타)의 물리 백엔드, Isaac Sim 없이도 동작 | Isaac Lab 2.2.1 task 안에서 매 스텝 실행 |
| 공개·라이선스 | 오픈소스, Apache-2.0(코드) | 비공개 — 허가 시 제공([설치와 예제 실행](index.md#설치와-예제-실행)) |
| 성숙도 | 1.0 정식(2026-03), 매월 릴리스 | 연구개발 중. 소재 값은 대부분 잠정값(실측 보정 전) |

## 겹치는 곳과 다른 곳

- **천.** Newton은 Style3D·VBD solver로 천의 움직임과 자기 충돌을 계산합니다. MDE의 수건도 천의 움직임을 계산하지만,
  목적은 접은 뒤 **남은 주름, 가장자리가 얼마나 늘어났는지, 찢김 한계를 넘었는지**를 학습 안에서 판정하는 데 있습니다
  ([수건 접기](towel.md)). Newton의 천 solver에서 영구 주름·찢김은 공개 자료에서 찾지 못했습니다.
- **소성.** Newton의 Implicit MPM은 입자 단위 소성(항복 압력·경화·연화)을 다룹니다. 모래·눈·흙 같은 입상체에 맞는 방식입니다.
  MDE는 부품 **표면**에 남는 자국과 얇은 벽 용기의 변형을 소재 Profile로 다룹니다([소재별 손가락 가압](materials.md), [PET 물병 쥐기](bottle.md)).
- **접촉.** Newton은 CAD 형상 SDF 충돌과 hydroelastic 접촉(Drake 모델 계열)을 제공합니다. MDE는 물리 엔진의 접촉을 받아
  쓰므로, 접촉을 더 정확히 푸는 엔진은 MDE의 입력을 좋게 만드는 쪽입니다.
- **판정과 라벨.** Newton이 주는 것은 상태와 힘입니다. MDE는 그 위에 「이 접촉으로 물체가 상했는가」를 소재 기준으로 판정해
  학습 보상·평가·데이터 라벨로 씁니다. 같은 손 힘이라도 소재가 바뀌면 판정이 바뀝니다.

## 함께 쓸 수 있는가

구조상으로는 가능합니다. MDE가 물리 엔진에 요구하는 것은 매 스텝의 접촉 위치·하중과, 변형된 형상을 되돌려 줄 통로입니다.
Newton은 Isaac Lab 3.0의 물리 백엔드이므로, MDE를 Isaac Lab 3.0으로 옮기면 Newton 위에서 같은 판정을 돌리는 것이 다음 검토 대상입니다.
**아직 시험하지 않았습니다.** 확인할 것은 접촉 정보의 형식, MuJoCo Warp 접촉과 PhysX 접촉의 차이가 판정에 주는 영향, 1024개 환경 처리량입니다.

## 읽을 때 주의

- Newton 항목은 아래 공개 자료(2026-10-30 확인)에서 확인한 것만 적었습니다. 「찾지 못함」은 공개 문서·소스·변경 이력에서
  확인하지 못했다는 뜻이며, 기능이 없다는 확정이 아닙니다. 성능 수치는 NVIDIA 발표값이며 독립 측정이 아닙니다.
- Newton의 Isaac Lab 연동 단계(베타 여부)는 문서 판에 따라 표기가 달라 확정하지 않았습니다.
- MDE 결과는 모두 시뮬레이션이며, 소재 값은 대부분 실측 보정 전의 잠정값입니다.

## 출처

| 내용 | 출처 (확인일) |
|---|---|
| 저장소·라이선스·요구 사항 | [github.com/newton-physics/newton](https://github.com/newton-physics/newton) (2026-10-30) |
| 버전 이력 (1.0.0 2026-03-10, 1.7.0 2026-10-14) | [PyPI newton](https://pypi.org/project/newton/#history) (2026-10-30) |
| Solver 목록·지원 대상·미분 가능 여부 | [Newton 문서 — Solvers](https://newton-physics.github.io/newton/stable/solvers/index.html) (2026-10-30) |
| Implicit MPM 소성 파라미터 | [SolverImplicitMPM API](https://newton-physics.github.io/newton/stable/api/_generated/newton.solvers.SolverImplicitMPM.html) (2026-10-30) |
| 발표 (GTC 2025) | [NVIDIA Technical Blog, 2025-03-18](https://developer.nvidia.com/blog/announcing-newton-an-open-source-physics-engine-for-robotics-simulation/) |
| 1.0 정식 발표·접촉(SDF·hydroelastic)·성능 수치·Isaac Lab 3.0 연동 | [NVIDIA Technical Blog, 2026-03-16](https://developer.nvidia.com/blog/?p=113754) |
| Linux Foundation 이관 | [Linux Foundation 보도자료, 2025-09-29](https://www.linuxfoundation.org/press/linux-foundation-announces-contribution-of-newton-by-disney-research-google-deepmind-and-nvidia-to-accelerate-open-robot-learning) |
| Isaac Lab 백엔드 | [Isaac Lab — Newton physics backend](https://isaac-sim.github.io/IsaacLab/develop/source/concepts/physics-backends/newton.html) (2026-10-30) |
| MuJoCo Warp | [github.com/google-deepmind/mujoco_warp](https://github.com/google-deepmind/mujoco_warp) (2026-10-30) |
