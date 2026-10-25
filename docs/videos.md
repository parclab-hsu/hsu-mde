# 데모 영상

모든 실험을 **매 스텝 한 프레임**(30 fps)으로 다시 찍었습니다. 실험마다 두 가지 영상이 있습니다.

- **데이터 영상**: 왼쪽은 장면, 오른쪽은 접촉력(손가락별·손바닥)·변형·관절 토크 그래프입니다. 빨간 세로선이 현재 스텝이고,
  위쪽 줄에 단계·설정·접촉력·변형·관절 토크·마찰 여유를 표시합니다.
- **네 방향 영상**: 정면·가까이·위·회전 카메라를 한 화면에 모았습니다.

영상의 수치는 같은 설정으로 다시 실행한 결과이며, PET 컵과 물병은 각 실험 페이지의 CSV와 값이 일치합니다.
종이컵 두 영상은 그 뒤에 「들고 있는 동안 무게를 받치는 마찰」을 관절 토크 계산에 넣은 판으로 다시 찍어, 종이컵 페이지·대표 데모의
CSV와 접촉력이 최대 0.7 N(빠른 데모), 0.004 N(쥐기) 다릅니다. 단계와 시점은 같습니다.
기준: 2026-10-25, Isaac Sim 5.0.0. 모든 결과는 시뮬레이션입니다. 추정값과 그 한계는 [추정값·힘 점검](check.md)에 정리했습니다.

## 비교 영상

같은 단계끼리 맞춰 나란히 재생합니다(단계 길이가 다르면 짧은 쪽을 늘려 맞춤).

<figure><video class="mde-video" src="../media/demo/compare-paper-pet.mp4" poster="../media/demo/compare-paper-pet.jpg" controls muted loop playsinline preload="none"></video><figcaption>종이컵 대 PET 컵 16 oz — 같은 동작, PET 컵은 1/3 이하의 힘으로 더 찌그러진다</figcaption></figure>

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
