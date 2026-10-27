# 데모 영상

모든 실험을 **매 스텝 한 프레임**(30 fps)으로 다시 찍었습니다. 실험마다 두 가지 영상이 있습니다.

- **데이터 영상**: 왼쪽은 장면, 오른쪽은 접촉력(손가락별·손바닥)·변형·관절 토크 그래프입니다. 빨간 세로선이 현재 스텝이고,
  위쪽 줄에 단계·설정·접촉력·변형·관절 토크·마찰 여유를 표시합니다.
- **네 방향 영상**: 정면·가까이·위·회전 카메라를 한 화면에 모았습니다.

[추정값·힘 점검](check.md)의 수정(PET 컵·물병 물성을 문헌 범위로, 힘 계산 수정)을 반영해 13개 실험을 모두 다시 찍었습니다.
영상의 수치는 각 실험 페이지의 CSV와 같은 실행에서 나왔습니다. 관절 토크 그래프에는 Allegro Hand 한계 0.7 N·m와
Isaac Lab 손 모델 설정 0.5 N·m를 함께 그렸습니다. 「관절 토크 최대」는 16개 관절 전체의 최대라, 토크로 조절하지 않는 벌림 관절도 포함합니다.
기준: 2026-10-25, Isaac Sim 5.0.0. 모든 결과는 시뮬레이션입니다. 추정값과 그 한계는 [추정값·힘 점검](check.md)에 정리했습니다.

## 강화학습 병렬 학습 (2026-10-27)

Isaac Lab에서 Allegro Hand가 PET 컵 16 oz를 집어 드는 동작을 강화학습(PPO)으로 배우는 과정입니다. 같은 장면 1024개를 GPU 한 장
(RTX 5080 16 GB)에서 동시에 돌려 1500회(iteration) 학습했고, 렌더링을 포함해 약 22분 걸렸습니다. 학습 중 250회마다 한 episode씩
찍은 장면 뒤에 다 배운 정책을 1024개 장면 전경으로 붙였습니다. 보상 구성과 수치 결과는 정리 중이라 아직 공개하지 않습니다.

<figure><video class="mde-video" src="../media/demo/rl-train-1024.mp4" poster="../media/demo/rl-train-1024.jpg" controls muted loop playsinline preload="none"></video><figcaption>PPO 학습 — 1024개 병렬 환경, 0·250·500·750·1000·1250회와 학습된 정책(56초)</figcaption></figure>

## 냉장고 문 여닫기 (2026-10-27)

Allegro Hand가 일반형 냉장고(폭 600 mm, 브랜드 없음)의 막대 손잡이를 감아 쥐고 문을 95° 열었다 닫습니다. 문 각도와 손목 경로는
정해 둔 스크립트이고, 손가락은 각 마디가 손잡이에 닿을 때까지 굽힙니다. 영상 아래 그래프는 그 움직임에서 **손이 손잡이에 내야 하는 힘**을
문 무게별로 계산한 것입니다(장면의 손이 실제로 힘을 내는 것은 아닙니다).

**위치 프로파일.** 문은 3 s 동안 0°→95°로 열리고, 1.2 s 멈춘 뒤 3 s 동안 닫힙니다(시작과 끝이 부드러운 코사인 곡선).
최대 각속도 50 °/s, 최대 각가속도 52 °/s², 손잡이 최대 속도 0.48 m/s입니다. 손잡이는 경첩 축에서 0.55 m 떨어져 있습니다.

**손의 힘.** 문을 경첩 축에 대해 돌리는 데 드는 힘을 네 가지로 나눴습니다.

| 성분 | 무엇으로 계산 | 크기(손잡이에서) |
|---|---|---|
| 문 패킹 | **MDE** — 문이 닫히는 마지막 몇 도 동안 패킹 눌림과 반력 | 닫힌 상태에서 문을 밖으로 미는 26.5 N 상당(패킹 전체 48.7 N, 눌림 2.0 mm) |
| 자석 띠 | 가정값 — 닫힌 상태에서 패킹 반력의 1.5배, 간격 1 mm마다 약 1/e로 약해짐 | 닫힌 상태에서 문을 안으로 당기는 39.7 N 상당 |
| 문 관성 | 문 무게 × 각가속도 | 아래 표 |
| 경첩 마찰 | 문 무게가 경첩 핀에 거는 마찰(마찰계수 0.15 가정) | 0.1–0.4 N |

닫힌 문을 떼어 낼 때는 자석이 패킹보다 세서 손이 약 **13 N**을 당겨야 하고, 닫히는 마지막 순간에는 자석이 문을 끌어당겨
손이 오히려 붙잡아야 합니다(그래프의 두 뾰족한 봉우리). 그 사이 대부분의 구간에서는 문 관성만 남아 힘이 작습니다.

| 문 무게(선반 내용물 포함) | 경첩 축 관성 | 열 때 최대 | 닫을 때 최대 | 관성 성분 최대 |
|---|---|---|---|---|
| 5 kg(빈 문) | 0.60 kg·m² | 8.8 N | 13.6 N | 1.0 N |
| 10 kg | 1.20 kg·m² | 9.8 N | 14.0 N | 2.0 N |
| 15 kg(선반 가득) | 1.79 kg·m² | 10.8 N | 14.4 N | 3.0 N |

이 동작 속도에서는 문 무게가 세 배가 되어도 최대 힘은 2 N 정도만 늘어납니다. 손 힘을 정하는 것은 패킹과 자석입니다.
표의 최대값은 1/30 s 간격 프레임에서 읽은 값이라, 간격 0에서 떼어 내는 순간의 13 N보다 열 때 최대가 작게 나옵니다.

MDE 패킹 지도와 수치는 장면 오른쪽 상자에, 패킹 눌림 그래프는 맨 아래 오른쪽에 있습니다. 패킹 강성(2 mm에서 전체 약 50 N)과
자석 띠는 실측값이 아닌 **가정값**이고, 오래 쓴 패킹이 납작해지는 현상은 모델에 없습니다.

<figure><video class="mde-video" src="../media/demo/fridge-door.mp4" poster="../media/demo/fridge-door.jpg" controls muted loop playsinline preload="none"></video><figcaption>냉장고 문 — 전경과 손잡이 확대(위), 위치 프로파일·문 무게별 손 힘·MDE 문 패킹 그래프(아래, 빨간 선이 현재 시각, 11초)</figcaption></figure>

<figure><img src="../media/demo/fridge-door-profile.png" alt="냉장고 문 위치 프로파일, 문 무게별 손 힘, MDE 문 패킹"><figcaption>위치 프로파일(왼쪽), 문 무게별 손 힘(가운데, +는 여는 방향), MDE 문 패킹 눌림·반력(오른쪽). 노란색: 쥐기·놓기, 파란색: 열기, 빨간색: 닫기</figcaption></figure>

## 비교 영상

같은 단계끼리 맞춰 나란히 재생합니다(단계 길이가 다르면 짧은 쪽을 늘려 맞춤).

<figure><video class="mde-video" src="../media/demo/compare-paper-pet.mp4" poster="../media/demo/compare-paper-pet.jpg" controls muted loop playsinline preload="none"></video><figcaption>종이컵 대 PET 컵 16 oz — 같은 동작, PET 컵은 1/3–1/6 토크로 쥔다</figcaption></figure>

<figure><video class="mde-video" src="../media/demo/compare-water.mp4" poster="../media/demo/compare-water.jpg" controls muted loop playsinline preload="none"></video><figcaption>PET 컵 — 빈 컵 · 물 1/3 · 물 2/3</figcaption></figure>

<figure><video class="mde-video" src="../media/demo/compare-sizes.mp4" poster="../media/demo/compare-sizes.jpg" controls muted loop playsinline preload="none"></video><figcaption>PET 컵 크기 9 · 16 · 20 · 24 oz — 위에서 본 테두리 변형</figcaption></figure>

<figure><video class="mde-video" src="../media/demo/compare-bottle.mp4" poster="../media/demo/compare-bottle.jpg" controls muted loop playsinline preload="none"></video><figcaption>PET 물병 500 ml — 빈 병 · 물 1/3 · 물 2/3 · 가득(마개 닫음) · 가득(마개 엶)</figcaption></figure>

<figure><video class="mde-video" src="../media/demo/compare-bottle-top.mp4" poster="../media/demo/compare-bottle-top.jpg" controls muted loop playsinline preload="none"></video><figcaption>PET 물병 가득 — 마개 닫음 대 엶, 위에서</figcaption></figure>

## 회전 카메라

<div class="mde-grid">
<figure><video class="mde-video" src="../media/demo/paper-orbit.mp4" poster="../media/demo/paper-orbit.jpg" controls muted loop playsinline preload="none"></video><figcaption>종이컵 16 oz</figcaption></figure>
<figure><video class="mde-video" src="../media/demo/paper-quick-orbit.mp4" poster="../media/demo/paper-quick-orbit.jpg" controls muted loop playsinline preload="none"></video><figcaption>종이컵 — 빠르게 쥐었다 놓치기(실제 시간)</figcaption></figure>
<figure><video class="mde-video" src="../media/demo/pet-orbit.mp4" poster="../media/demo/pet-orbit.jpg" controls muted loop playsinline preload="none"></video><figcaption>PET 컵 16 oz — 빈 컵</figcaption></figure>
<figure><video class="mde-video" src="../media/demo/pet-23-orbit.mp4" poster="../media/demo/pet-23-orbit.jpg" controls muted loop playsinline preload="none"></video><figcaption>PET 컵 16 oz — 물 2/3</figcaption></figure>
<figure><video class="mde-video" src="../media/demo/bottle-full-orbit.mp4" poster="../media/demo/bottle-full-orbit.jpg" controls muted loop playsinline preload="none"></video><figcaption>PET 물병 — 가득, 마개 닫음</figcaption></figure>
<figure><video class="mde-video" src="../media/demo/bottle-open-orbit.mp4" poster="../media/demo/bottle-open-orbit.jpg" controls muted loop playsinline preload="none"></video><figcaption>PET 물병 — 가득, 마개 엶</figcaption></figure>
</div>

## 종이컵

### 종이컵 16 oz (쥐기 0.10 · 꽉 쥐기 0.35 N·m)

<video class="mde-video" src="../media/demo/paper-data.mp4" poster="../media/demo/paper-data.jpg" controls muted loop playsinline preload="none"></video>

<details><summary>네 방향 영상</summary>
<video class="mde-video" src="../media/demo/paper-views.mp4" poster="../media/demo/paper-views.jpg" controls muted loop playsinline preload="none"></video>
</details>

### 종이컵 — 빠르게 쥐었다 놓치기 (1/30 s 스텝, 실제 시간)

<video class="mde-video" src="../media/demo/paper-quick-data.mp4" poster="../media/demo/paper-quick-data.jpg" controls muted loop playsinline preload="none"></video>

<details><summary>네 방향 영상</summary>
<video class="mde-video" src="../media/demo/paper-quick-views.mp4" poster="../media/demo/paper-quick-views.jpg" controls muted loop playsinline preload="none"></video>
</details>

## PET 컵 16 oz — 물

### 빈 컵 (0.03 · 0.06 N·m)

<video class="mde-video" src="../media/demo/pet-data.mp4" poster="../media/demo/pet-data.jpg" controls muted loop playsinline preload="none"></video>

<details><summary>네 방향 영상</summary>
<video class="mde-video" src="../media/demo/pet-views.mp4" poster="../media/demo/pet-views.jpg" controls muted loop playsinline preload="none"></video>
</details>

### 물 1/3 (0.03 · 0.06 N·m)

<video class="mde-video" src="../media/demo/pet-13-data.mp4" poster="../media/demo/pet-13-data.jpg" controls muted loop playsinline preload="none"></video>

<details><summary>네 방향 영상</summary>
<video class="mde-video" src="../media/demo/pet-13-views.mp4" poster="../media/demo/pet-13-views.jpg" controls muted loop playsinline preload="none"></video>
</details>

### 물 2/3 (0.05 · 0.08 N·m)

<video class="mde-video" src="../media/demo/pet-23-data.mp4" poster="../media/demo/pet-23-data.jpg" controls muted loop playsinline preload="none"></video>

<details><summary>네 방향 영상</summary>
<video class="mde-video" src="../media/demo/pet-23-views.mp4" poster="../media/demo/pet-23-views.jpg" controls muted loop playsinline preload="none"></video>
</details>

## PET 컵 크기

### 9 oz

<video class="mde-video" src="../media/demo/pet-9oz-data.mp4" poster="../media/demo/pet-9oz-data.jpg" controls muted loop playsinline preload="none"></video>

<details><summary>네 방향 영상</summary>
<video class="mde-video" src="../media/demo/pet-9oz-views.mp4" poster="../media/demo/pet-9oz-views.jpg" controls muted loop playsinline preload="none"></video>
</details>

### 20 oz

<video class="mde-video" src="../media/demo/pet-20oz-data.mp4" poster="../media/demo/pet-20oz-data.jpg" controls muted loop playsinline preload="none"></video>

<details><summary>네 방향 영상</summary>
<video class="mde-video" src="../media/demo/pet-20oz-views.mp4" poster="../media/demo/pet-20oz-views.jpg" controls muted loop playsinline preload="none"></video>
</details>

### 24 oz

<video class="mde-video" src="../media/demo/pet-24oz-data.mp4" poster="../media/demo/pet-24oz-data.jpg" controls muted loop playsinline preload="none"></video>

<details><summary>네 방향 영상</summary>
<video class="mde-video" src="../media/demo/pet-24oz-views.mp4" poster="../media/demo/pet-24oz-views.jpg" controls muted loop playsinline preload="none"></video>
</details>

## PET 물병 500 ml

### 빈 병 (0.10 · 0.35 N·m)

<video class="mde-video" src="../media/demo/bottle-data.mp4" poster="../media/demo/bottle-data.jpg" controls muted loop playsinline preload="none"></video>

<details><summary>네 방향 영상</summary>
<video class="mde-video" src="../media/demo/bottle-views.mp4" poster="../media/demo/bottle-views.jpg" controls muted loop playsinline preload="none"></video>
</details>

### 물 1/3 (0.10 · 0.35 N·m)

<video class="mde-video" src="../media/demo/bottle-13-data.mp4" poster="../media/demo/bottle-13-data.jpg" controls muted loop playsinline preload="none"></video>

<details><summary>네 방향 영상</summary>
<video class="mde-video" src="../media/demo/bottle-13-views.mp4" poster="../media/demo/bottle-13-views.jpg" controls muted loop playsinline preload="none"></video>
</details>

### 물 2/3 (0.10 · 0.35 N·m)

<video class="mde-video" src="../media/demo/bottle-23-data.mp4" poster="../media/demo/bottle-23-data.jpg" controls muted loop playsinline preload="none"></video>

<details><summary>네 방향 영상</summary>
<video class="mde-video" src="../media/demo/bottle-23-views.mp4" poster="../media/demo/bottle-23-views.jpg" controls muted loop playsinline preload="none"></video>
</details>

### 가득, 마개 닫음 (0.12 · 0.35 N·m)

<video class="mde-video" src="../media/demo/bottle-full-data.mp4" poster="../media/demo/bottle-full-data.jpg" controls muted loop playsinline preload="none"></video>

<details><summary>네 방향 영상</summary>
<video class="mde-video" src="../media/demo/bottle-full-views.mp4" poster="../media/demo/bottle-full-views.jpg" controls muted loop playsinline preload="none"></video>
</details>

### 가득, 마개 엶 (0.12 · 0.35 N·m)

<video class="mde-video" src="../media/demo/bottle-open-data.mp4" poster="../media/demo/bottle-open-data.jpg" controls muted loop playsinline preload="none"></video>

<details><summary>네 방향 영상</summary>
<video class="mde-video" src="../media/demo/bottle-open-views.mp4" poster="../media/demo/bottle-open-views.jpg" controls muted loop playsinline preload="none"></video>
</details>
