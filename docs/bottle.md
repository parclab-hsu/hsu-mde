# PET 물병 쥐기

[플라스틱 컵 쥐기](plastic-cup.md)와 같은 동작으로 **500 ml PET 생수병**(몸통 지름 65 mm, 높이 205 mm, 벽 두께 0.16 mm)을
쥡니다. 옆에서 감싸 쥐고, 80 mm 들어 올려 더 세게 쥐었다가 풀고, 내려놓습니다. **빈 병, 물 1/3, 물 2/3, 가득(마개 닫음),
가득(마개 엶)** 다섯 경우를 비교합니다. 병 벽의 색은 변형 방향(적색: 바깥으로, 청색: 안쪽으로)입니다. 기준: 2026-10-25,
Isaac Sim 5.0.0. [추정값·힘 점검](check.md)에 따라 벽 두께(0.25 → 0.16 mm)와 무게(14 → 12 g)를 경량 생수병 문헌값에 맞추고
힘 계산을 손본 뒤 다시 계산했습니다.

병 몸통은 위아래가 바닥과 어깨에 붙잡혀 있어, 벽이 얇아도 컵만큼 쉽게 타원이 되지 않습니다. 몸통 가운데에서 지름을 6.35 mm 줄이는 데
**3.6 N**이 듭니다(모델 추정값, 2026-10-24 판은 벽 0.25 mm로 9.8 N). 종이컵과 같은 토크(쥐기 0.10 N·m, 꽉 쥐기 0.35 N·m)로 쥐었습니다.

## 가득 — 499 ml, 병과 물 511 g, 마개 닫음 (쥐기 0.12 N·m, 꽉 쥐기 0.35 N·m)

<video class="mde-video" src="../media/bottle-full-grasp.mp4" poster="../media/bottle-full-grasp.jpg" controls muted loop playsinline></video>

<div class="mde-grid">
<figure><img src="../images/bottle-full-open.jpg" loading="lazy" alt="쥐기 전"><figcaption>쥐기 전</figcaption></figure>
<figure><img src="../images/bottle-full-lifted.jpg" loading="lazy" alt="들었을 때"><figcaption>80 mm 들어 올림 (0.12 N·m)</figcaption></figure>
<figure><img src="../images/bottle-full-squeezed.jpg" loading="lazy" alt="꽉 쥐었을 때"><figcaption>꽉 쥐었을 때 (0.35 N·m)</figcaption></figure>
<figure><img src="../images/bottle-full-squeezed-top.jpg" loading="lazy" alt="꽉 쥐었을 때 위에서"><figcaption>꽉 쥐었을 때 위에서</figcaption></figure>
</div>

## 가득 — 마개 엶 (쥐기 0.12 N·m, 꽉 쥐기 0.35 N·m)

<video class="mde-video" src="../media/bottle-open-grasp.mp4" poster="../media/bottle-open-grasp.jpg" controls muted loop playsinline></video>

<div class="mde-grid">
<figure><img src="../images/bottle-open-lifted.jpg" loading="lazy" alt="들었을 때"><figcaption>80 mm 들어 올림</figcaption></figure>
<figure><img src="../images/bottle-open-squeezed.jpg" loading="lazy" alt="꽉 쥐었을 때"><figcaption>꽉 쥐었을 때</figcaption></figure>
<figure><img src="../images/bottle-open-squeezed-top.jpg" loading="lazy" alt="꽉 쥐었을 때 위에서"><figcaption>꽉 쥐었을 때 위에서</figcaption></figure>
</div>

## 빈 병 · 물 1/3 · 물 2/3 (쥐기 0.10 N·m, 꽉 쥐기 0.35 N·m)

<div class="mde-grid">
<figure><video class="mde-video" src="../media/bottle-empty-grasp.mp4" poster="../media/bottle-empty-grasp.jpg" controls muted loop playsinline></video><figcaption>빈 병 (12 g)</figcaption></figure>
<figure><video class="mde-video" src="../media/bottle-13-grasp.mp4" poster="../media/bottle-13-grasp.jpg" controls muted loop playsinline></video><figcaption>물 1/3 — 173 ml, 185 g</figcaption></figure>
<figure><video class="mde-video" src="../media/bottle-23-grasp.mp4" poster="../media/bottle-23-grasp.jpg" controls muted loop playsinline></video><figcaption>물 2/3 — 347 ml, 359 g</figcaption></figure>
</div>

<div class="mde-grid">
<figure><img src="../images/bottle-empty-open.jpg" loading="lazy" alt="빈 병 쥐기 전"><figcaption>빈 병 — 쥐기 전</figcaption></figure>
<figure><img src="../images/bottle-13-open.jpg" loading="lazy" alt="물 1/3 쥐기 전"><figcaption>물 1/3 — 쥐기 전</figcaption></figure>
<figure><img src="../images/bottle-23-open.jpg" loading="lazy" alt="물 2/3 쥐기 전"><figcaption>물 2/3 — 쥐기 전</figcaption></figure>
</div>

## 결과

| | 빈 병 | 물 1/3 | 물 2/3 | 가득, 마개 닫음 | 가득, 마개 엶 |
|---|---|---|---|---|---|
| 병과 물의 무게 | 12 g | 185 g | 359 g | 511 g | 511 g |
| 쥐기 / 꽉 쥐기 설정 | 0.10 / 0.35 N·m | 0.10 / 0.35 | 0.10 / 0.35 | 0.12 / 0.35 | 0.12 / 0.35 |
| 쥐었을 때 접촉력 | 17.7 N | 18.5 N | 18.2 N | 19.2 N | 19.5 N |
| 들고 있을 때 접촉력 | 17.6 N | 16.9 N | 17.6 N | 20.3 N | 20.9 N |
| 꽉 쥐었을 때 접촉력 | 67.5 N | 69.1 N | 64.4 N | 65.9 N | 68.8 N |
| 벽 변위 최대 | 3.06 mm | 3.12 mm | 3.12 mm | 2.73 mm | 3.14 mm |
| 병 안 압력 상승 최대 | 0.0 kPa | 0.2 kPa | 0.4 kPa | 1.9 kPa | — |
| 마찰 여유 (들고 있는 동안 최소) | 67배 | 4.6배 | 2.5배 | 1.9배 | 2.1배 |
| 관절 토크 최대 | 0.73 N·m | 0.85 N·m | 0.77 N·m | 0.73 N·m | 0.74 N·m |
| 0.7 N·m 넘은 스텝 | 1 | 8 | 2 | 2 | 1 |

![접촉력 합과 벽 변위 최대: 500 ml PET 물병 다섯 경우](images/bottle-runs.png){ loading=lazy }

- 마개를 닫은 병은 연 병보다 벽 변위 최대가 13 % 작습니다(2.73 대 3.14 mm). 벽이 얇아져 같은 힘에 병 부피가 더 줄고, 병 안 압력이
  1.9 kPa까지 올라갑니다(2026-10-24 판 1.2 kPa). 다만 두 경우 손가락이 닿는 순서와 힘이 조금씩 달라, 차이가 모두 마개 때문은 아닙니다.
- 가득 찬 병의 쥐기 토크 0.12 N·m는 2026-10-24에 정한 값입니다(0.10 N·m에서 마개를 연 경우 마찰 여유가 한 스텝 0.98).
- 관절 토크 최대는 0.73–0.85 N·m로 2026-10-24 판(0.84–1.09 N·m)보다 작아졌습니다. 엄지 회전 관절이 한계(0.7 N·m)에서 밀리도록
  바꾸고, 손가락 관절이 설정을 크게 넘지 않도록 조절을 고쳤습니다. 0.7 N·m를 넘는 스텝은 다섯 경우 1–8스텝입니다.
- Isaac Lab의 손 모델은 관절 한계를 0.5 N·m로 둡니다. 그 기준이면 다섯 경우 모두 꽉 쥐는 동안 61–85스텝이 한계를 넘습니다.

데이터(스텝·단계·설정·접촉력 합과 손가락별·벽 변위·병 높이·마찰이 받친 힘·수면 높이·병 안 압력·힘 평형 미수렴 표시·관절 16개 토크):
[빈 병](data/bottle-empty-grasp.csv) · [물 1/3](data/bottle-13-grasp.csv) · [물 2/3](data/bottle-23-grasp.csv) ·
[가득, 마개 닫음](data/bottle-full-grasp.csv) · [가득, 마개 엶](data/bottle-open-grasp.csv)

!!! warning "한계"
    - **병의 옆벽 강성은 실측값이 아닙니다.** 병 치수·벽 두께(경량 생수병 무게에서 정한 0.16 mm)·PET 탄성계수에서 계산한
      추정값입니다. 실제 생수병에는 대부분 가로 줄무늬(리브)나 그립 패널이 있어 이 모델보다 단단합니다.
    - 꽉 쥐기에서 손가락 하나의 힘(17–19 N)과 손바닥 힘(34–38 N)은 Allegro Hand 손끝 능력(약 7–15 N, 추정)을 넘습니다 → [추정값·힘 점검](check.md)
    - 병 벽은 **탄성만** 표현합니다. 모델이 정확한 범위는 벽 변위 약 2.6 mm이고, 꽉 쥐기(2.7–3.1 mm)는 조금 넘습니다.
      꺾이거나 찌그러진 채 남는 변형, 어깨와 바닥의 변형은 없습니다. 어깨·목·마개는 그림입니다.
    - 들고 있는 동안 0–2스텝(약 300스텝 중)은 병의 수평 힘 평형이 끝까지 맞지 않은 채 기록되었습니다(데이터의 표시 열).
    - 물은 무게(마개를 닫은 경우 병 안 압력 포함)로만 들어갑니다. 출렁임·관성은 없고, 병은 기울지 않습니다.
    - 병 무게(12 g)와 손가락 마찰계수(0.5)는 실측값이 아닙니다. 관절 토크는 시뮬레이션의 접촉력에서 계산한 값입니다.
