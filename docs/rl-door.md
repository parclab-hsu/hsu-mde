# 강화학습 데모 — 가전 문 열기

Allegro Hand가 가전제품 네 종(냉장고·오븐형 전자레인지·식기세척기·드럼세탁기)의 **손잡이를 쥐고 문을 여는 동작**을
강화학습(PPO)으로 배운 결과입니다. 가전마다 같은 장면 512개를 GPU 한 장(RTX 5080 16 GB)에서 동시에 돌려 800회(iteration)
학습했습니다. 기준: 2026-10-30, Isaac Sim 5.0.0 · Isaac Lab 2.2.1. 모든 결과는 시뮬레이션입니다.

**장면.** 가전은 실제 제품의 3D 모델을 관절체(문·경첩)로 옮긴 것이고, 문 질량·경첩 마찰·걸쇠 힘은 **가정값**입니다.
모델의 손잡이는 문 면에 묻힌 오목형이라, 손이 쥘 수 있도록 **회색 막대 손잡이**(반지름 10–12 mm, 문 면에서 45–50 mm)를
따로 달았습니다. 손은 팔 없이 떠 있는 손목에 달려 있고, 손목은 **최대 80 N**까지만 낼 수 있습니다 — 무한한 팔 힘으로 문을
끌어내지 못하게 한 것입니다. 처음 0.4 s는 손바닥이 막대 앞에 오도록 정해 둔 동작으로 다가가고, 그 뒤 손가락 16개와 손목은
정책이 움직입니다. 보상 구성은 공개하지 않습니다.

**MDE가 계산하는 것.** 손끝·손바닥의 접촉력은 매 스텝 손끝 패드 소재(일반 엘라스토머 패드, 가정값)의 MDE 모델로 들어가
패드가 눌린 깊이, 손을 뗀 뒤 남는 영구변형, 소재가 견디는 한계(항복)를 넘었는지를 냅니다. 이 패드는 접촉 한 곳에 약 32 N에서
항복합니다. 냉장고는 **문 패킹의 눌림과 반력**도 MDE가 계산합니다(닫힌 상태에서 패킹이 문을 미는 힘 − 자석 띠가 당기는 힘).

| 가전 | 문 | 목표 각도 | 닫힌 문을 붙잡는 것(가정) |
|---|---|---|---|
| 냉장고 | 오른쪽 위 문, 10 kg | 90° | MDE 패킹 − 자석 띠 → 손잡이에서 11.7 N |
| 오븐형 전자레인지 | 옆으로 여는 문, 2.5 kg (조리대 높이 0.9 m) | 90° | 스프링 걸쇠 15 N |
| 식기세척기 | 아래 경첩 문, 5 kg (균형 스프링이 무게의 85 %를 받침) | 80° | 걸쇠 20 N |
| 드럼세탁기 | 원형 문, 3.5 kg | 90° | 걸쇠 30 N |

## 결과

정책을 고정하고(결정론) 가전마다 128회 평가했습니다. 「스크립트」는 학습 없이 같은 0.4 s 접근 뒤 손가락을 말아 쥐고 손목을
문 면에서 곧게 뒤로 당기는 비교 기준입니다.

| 가전 | 방법 | 연 횟수 | 목표 각도까지(중앙값) | 막대를 쥔 시간 | 손끝 최대 힘 중앙값(90 %) | MDE 패드 눌림 중앙값 | 영구변형 중앙값 | 항복을 넘은 스텝 |
|---|---|---|---|---|---|---|---|---|
| 냉장고 | **강화학습** | **128/128** | 1.92 s | 96 % | 41.6 N (58.0) | 2.25 mm | 0.022 mm | 3.4 % |
| | 스크립트 | 2/128 | 2.59 s | 33 % | 115 N (197) | 2.75 mm | 0.068 mm | 15.4 % |
| 오븐형 전자레인지 | **강화학습** | **128/128** | 1.60 s | 89 % | 44.2 N (57.0) | 2.47 mm | 0.043 mm | 5.5 % |
| | 스크립트 | 23/128 | 2.45 s | 43 % | 90.7 N (120) | 2.94 mm | 0.085 mm | 30.0 % |
| 식기세척기 | **강화학습** | **128/128** | 2.00 s | 81 % | 58.7 N (72.5) | 2.72 mm | 0.065 mm | 1.6 % |
| | 스크립트 | 123/128 | 2.60 s | 41 % | 337 N (990) | 2.75 mm | 0.068 mm | 12.5 % |
| 드럼세탁기 | **강화학습** | **124/128** | 2.10 s | 52 % | 61.3 N (102) | 2.75 mm | 0.068 mm | 1.4 % |
| | 스크립트 | 14/128 | 3.14 s | 48 % | 77.0 N (496) | 2.75 mm | 0.068 mm | 18.2 % |

- 스크립트는 막대를 놓쳤다 다시 부딪치며 손끝 힘이 튑니다(식기세척기 90 % 값 990 N은 충돌입니다). 강화학습 정책은 손끝 힘을
  중앙값 42–61 N으로 묶고, 패드가 항복을 넘는 시간을 스크립트의 1/2–1/13로 줄였습니다.
- 다만 **강화학습 정책도 패드 항복(약 32 N/접촉)을 넘습니다.** 이 패드로 이 문들을 여는 데 드는 힘이 항복 근처라는 뜻이고,
  실물 손이라면 패드 소재를 고를 때 따져야 할 부분입니다. 남는 영구변형은 0.02–0.07 mm입니다.
- 냉장고 문 패킹(MDE): 닫힌 상태의 눌림 2.00 mm, 한 번 여닫은 뒤 남은 눌림 0입니다(패킹 수명 판정은 아닙니다).
- 「막대를 쥔 시간」은 목표에 닿은 뒤까지 포함한 에피소드 전체의 비율입니다. 영상의 장면 하나(env 0)에서는 접근이 끝난 뒤
  목표 각도에 닿을 때까지 세탁기·식기세척기 100 %, 오븐 88 % 쥐고 있었습니다(나머지 장면의 구간별 값은 재지 않았습니다).
- 손목 힘은 강화학습·스크립트 모두 상한 80 N에 닿습니다.

## 영상

각 가전마다 영상이 두 개입니다. 위는 학습 전(0회)·300회·학습 후(799회) 한 장면 확대와 학습된 정책 16개 장면,
아래는 학습된 정책 한 장면에 문 각도·손끝 힘·MDE 패드 눌림(·냉장고 패킹) 그래프를 붙인 것입니다.

### 냉장고

<figure><video class="mde-video" src="../media/demo/rl-door-fridge.mp4" poster="../media/demo/rl-door-fridge.jpg" controls muted loop playsinline preload="none"></video><figcaption>냉장고 문 — 학습 과정(학습 전·300회·799회)과 16개 장면(32초)</figcaption></figure>

<figure><video class="mde-video" src="../media/demo/rl-door-fridge-mde.mp4" poster="../media/demo/rl-door-fridge-mde.jpg" controls muted loop playsinline preload="none"></video><figcaption>냉장고 문 — 학습된 정책과 MDE 판정(문 각도·손끝 힘·패드 눌림·패킹 눌림)</figcaption></figure>

### 오븐형 전자레인지

<figure><video class="mde-video" src="../media/demo/rl-door-oven.mp4" poster="../media/demo/rl-door-oven.jpg" controls muted loop playsinline preload="none"></video><figcaption>오븐형 전자레인지 옆문 — 학습 과정과 16개 장면(32초)</figcaption></figure>

<figure><video class="mde-video" src="../media/demo/rl-door-oven-mde.mp4" poster="../media/demo/rl-door-oven-mde.jpg" controls muted loop playsinline preload="none"></video><figcaption>오븐형 전자레인지 — 학습된 정책과 MDE 판정</figcaption></figure>

### 식기세척기

<figure><video class="mde-video" src="../media/demo/rl-door-dish.mp4" poster="../media/demo/rl-door-dish.jpg" controls muted loop playsinline preload="none"></video><figcaption>식기세척기 아래 경첩 문 — 학습 과정과 16개 장면(32초)</figcaption></figure>

<figure><video class="mde-video" src="../media/demo/rl-door-dish-mde.mp4" poster="../media/demo/rl-door-dish-mde.jpg" controls muted loop playsinline preload="none"></video><figcaption>식기세척기 — 학습된 정책과 MDE 판정</figcaption></figure>

### 드럼세탁기

<figure><video class="mde-video" src="../media/demo/rl-door-washer.mp4" poster="../media/demo/rl-door-washer.jpg" controls muted loop playsinline preload="none"></video><figcaption>드럼세탁기 원형 문 — 학습 과정과 16개 장면(32초)</figcaption></figure>

<figure><video class="mde-video" src="../media/demo/rl-door-washer-mde.mp4" poster="../media/demo/rl-door-washer-mde.jpg" controls muted loop playsinline preload="none"></video><figcaption>드럼세탁기 — 학습된 정책과 MDE 판정</figcaption></figure>

## 한계

- 학습은 가전마다 한 번(seed 1개)입니다.
- 가전의 질량·경첩 마찰·걸쇠·자석 띠 힘은 가정값이고, 패드 소재는 일반 엘라스토머의 문헌값입니다. 실물로 재지 않았습니다.
- 손은 팔 없이 떠 있는 손목에 달린 Allegro Hand입니다. 실제 팔의 관절 한계·자세는 반영하지 않았습니다.
- 막대 손잡이는 학습을 위해 덧붙인 것으로, 제품의 실제 손잡이 모양과 다릅니다.
