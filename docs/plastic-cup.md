# 플라스틱 컵 쥐기

[종이컵 쥐기](cup.md)와 같은 동작으로 투명 **PET 16 oz 냉음료 컵**(윗지름 98 mm, 아랫지름 58 mm, 높이 115 mm, 벽 두께 0.25 mm)을
쥡니다. 옆에서 감싸 쥐고, 80 mm 들어 올려 더 세게 쥐었다가 풀고, 내려놓습니다. **빈 컵, 물 1/3, 물 2/3** 세 경우와 **컵 크기 네 가지**(9 / 16 / 20 / 24 oz)를 비교합니다.
500 ml 물병은 [PET 물병 쥐기](bottle.md)에 있습니다.
PET 컵은 종이컵보다 훨씬 무르기 때문에 관절 토크를 낮췄습니다(종이컵은 0.10 / 0.35 N·m).
컵 벽의 색은 변형 방향(적색: 바깥으로, 청색: 안쪽으로)입니다. 기준: 2026-10-25, Isaac Sim 5.0.0.
[추정값·힘 점검](check.md)에 따라 PET 컵 옆벽 강성을 문헌 범위로 고치고 힘 계산을 손본 뒤 다시 계산했습니다. 2026-10-24 판보다 컵이 약 4.5배 단단합니다.

## 빈 컵 (쥐기 0.03 N·m, 꽉 쥐기 0.06 N·m)

<video class="mde-video" src="../media/pet-cup-grasp.mp4" poster="../media/pet-cup-grasp.jpg" controls muted loop playsinline></video>

<div class="mde-grid">
<figure><img src="../images/pet-cup-grasped.jpg" loading="lazy" alt="쥐었을 때"><figcaption>쥐었을 때 (0.03 N·m)</figcaption></figure>
<figure><img src="../images/pet-cup-squeezed.jpg" loading="lazy" alt="꽉 쥐었을 때"><figcaption>꽉 쥐었을 때 (0.06 N·m)</figcaption></figure>
<figure><img src="../images/pet-cup-squeezed-top.jpg" loading="lazy" alt="꽉 쥐었을 때 위에서"><figcaption>위에서 본 모습 — 테두리가 타원이 된다</figcaption></figure>
<figure><img src="../images/pet-cup-eased.jpg" loading="lazy" alt="되돌렸을 때"><figcaption>0.03 N·m로 되돌림 — 테두리 변형이 3.4 → 2.1 mm로 줄어든다</figcaption></figure>
</div>

## 물 1/3 — 126 ml, 컵과 물 138 g (쥐기 0.03 N·m, 꽉 쥐기 0.06 N·m)

<video class="mde-video" src="../media/pet-water13-grasp.mp4" poster="../media/pet-water13-grasp.jpg" controls muted loop playsinline></video>

<div class="mde-grid">
<figure><img src="../images/pet-water13-open.jpg" loading="lazy" alt="쥐기 전"><figcaption>쥐기 전 — 물 높이 38 mm</figcaption></figure>
<figure><img src="../images/pet-water13-lifted.jpg" loading="lazy" alt="들었을 때"><figcaption>80 mm 들어 올림</figcaption></figure>
<figure><img src="../images/pet-water13-squeezed-top.jpg" loading="lazy" alt="꽉 쥐었을 때 위에서"><figcaption>꽉 쥐었을 때 위에서</figcaption></figure>
</div>

## 물 2/3 — 310 ml, 컵과 물 322 g (쥐기 0.05 N·m, 꽉 쥐기 0.08 N·m)

빈 컵과 같은 0.03 N·m로는 들지 못합니다. 쥐는 힘 1.7 N에 마찰계수 0.5를 곱한 0.9 N이 받쳐야 하는 힘 2.9 N(무게 3.2 N에서 컵을 밀어 올리는 힘을 뺀 값)보다
작습니다.
그래서 0.05 N·m로 올려 쥐었습니다.

<video class="mde-video" src="../media/pet-water23-grasp.mp4" poster="../media/pet-water23-grasp.jpg" controls muted loop playsinline></video>

<div class="mde-grid">
<figure><img src="../images/pet-water23-open.jpg" loading="lazy" alt="쥐기 전"><figcaption>쥐기 전 — 물 높이 77 mm</figcaption></figure>
<figure><img src="../images/pet-water23-lifted.jpg" loading="lazy" alt="들었을 때"><figcaption>80 mm 들어 올림 (0.05 N·m)</figcaption></figure>
<figure><img src="../images/pet-water23-squeezed-top.jpg" loading="lazy" alt="꽉 쥐었을 때 위에서"><figcaption>꽉 쥐었을 때 위에서 (0.08 N·m)</figcaption></figure>
</div>

## 결과

| | 빈 컵 | 물 1/3 | 물 2/3 |
|---|---|---|---|
| 컵과 물의 무게 | 12 g (0.12 N) | 138 g (1.36 N) | 322 g (3.16 N) |
| 쥐기 / 꽉 쥐기 설정 | 0.03 / 0.06 N·m | 0.03 / 0.06 N·m | 0.05 / 0.08 N·m |
| 쥐었을 때 접촉력 · 테두리 변형 | 5.4 N · 1.3 mm | 3.2 N · 1.6 mm | 6.8 N · 1.6 mm |
| 들고 있을 때 접촉력 | 5.4 N | 3.8 N | 6.6 N |
| 꽉 쥐었을 때 접촉력 · 테두리 변형 | 10.6 N · 3.4 mm | 9.7 N · 3.5 mm | 13.8 N · 4.4 mm |
| 되돌렸을 때 테두리 변형 | 2.1 mm | 2.4 mm | 4.0 mm |
| 마찰 여유 (들고 있는 동안 최소) | 3.1배 | 1.9배 | **1.4배** |
| 관절 토크 최대 | 0.12 N·m | 0.14 N·m | 0.19 N·m |

- 마찰 여유는 손가락이 마찰로 버틸 수 있는 힘(마찰계수 0.5 × 접촉력)을 마찰이 받쳐야 하는 힘으로 나눈 값입니다. 1보다 작으면 미끄러집니다.
  원뿔형 컵은 손가락이 미는 힘의 일부가 컵을 위로 밀어 올리므로, 받쳐야 하는 힘은 무게보다 작습니다. 2026-10-24 판은 이것을 빼지 않아
  빈 컵의 여유가 19.7배로 크게 나왔습니다.
- 관절 토크에는 손가락 마찰이 컵과 물의 무게를 받치는 힘이 들어 있습니다.
- 꽉 쥐어도 수면 높이는 0.1 mm 이하로만 변합니다. 컵이 타원으로 찌그러져도 단면적은 거의 줄지 않기 때문입니다.

## 컵 크기 — 9 / 16 / 20 / 24 oz (빈 컵, 쥐기 0.03 N·m, 꽉 쥐기 0.06 N·m)

윗지름이 같은 계열(95–98 mm)의 PET 컵 네 가지를 같은 토크로 쥡니다. 벽 두께와 소재는 16 oz와 같고, 치수만 다릅니다.

| | 9 oz | 16 oz | 20 oz | 24 oz |
|---|---|---|---|---|
| 윗지름 / 아랫지름 / 높이 | 95 / 57 / 83 mm | 98 / 58 / 115 mm | 95 / 60 / 140 mm | 95 / 64 / 165 mm |
| 컵 무게 (추정) | 8.9 g | 12 g | 13.8 g | 16.4 g |
| 쥐는 높이 (탁자에서) | 40 mm | 75 mm | 91 mm | 107 mm |
| 지름을 6.35 mm 줄이는 힘 (추정) | 3.3 N | 3.2 N | 3.5 N | 3.6 N |
| 쥐었을 때 접촉력 · 테두리 변형 | 5.3 N · 2.4 mm | 5.4 N · 1.3 mm | 4.5 N · 2.1 mm | 4.5 N · 1.9 mm |
| 꽉 쥐었을 때 접촉력 · 테두리 변형 | 7.4 N · 3.5 mm | 10.6 N · 3.4 mm | 10.0 N · 3.7 mm | 10.4 N · 3.1 mm |
| 되돌렸을 때 테두리 변형 | 1.6 mm | 2.1 mm | 2.0 mm | 1.8 mm |
| 마찰 여유 (들고 있는 동안 최소) | 2.3배 | 3.1배 | 4.5배 | 6.4배 |
| 관절 토크 최대 | 0.18 N·m | 0.12 N·m | 0.13 N·m | 0.14 N·m |

<div class="mde-grid">
<figure><img src="../images/pet-9oz-squeezed-top.jpg" loading="lazy" alt="9 oz 꽉 쥐었을 때 위에서"><figcaption>9 oz — 꽉 쥐었을 때 위에서</figcaption></figure>
<figure><img src="../images/pet-20oz-squeezed-top.jpg" loading="lazy" alt="20 oz 꽉 쥐었을 때 위에서"><figcaption>20 oz — 꽉 쥐었을 때 위에서</figcaption></figure>
<figure><img src="../images/pet-24oz-squeezed-top.jpg" loading="lazy" alt="24 oz 꽉 쥐었을 때 위에서"><figcaption>24 oz — 꽉 쥐었을 때 위에서</figcaption></figure>
</div>

<div class="mde-grid">
<figure><video class="mde-video" src="../media/pet-9oz-grasp.mp4" poster="../media/pet-9oz-grasp.jpg" controls muted loop playsinline></video><figcaption>9 oz</figcaption></figure>
<figure><video class="mde-video" src="../media/pet-20oz-grasp.mp4" poster="../media/pet-20oz-grasp.jpg" controls muted loop playsinline></video><figcaption>20 oz</figcaption></figure>
<figure><video class="mde-video" src="../media/pet-24oz-grasp.mp4" poster="../media/pet-24oz-grasp.jpg" controls muted loop playsinline></video><figcaption>24 oz</figcaption></figure>
</div>

![접촉력 합과 테두리 변형: PET 컵 9·16·20·24 oz](images/pet-sizes.png){ loading=lazy }

- 같은 토크로 쥐면 접촉력은 크기와 관계없이 비슷합니다(쥘 때 4.5–5.4 N). 9 oz는 키가 낮아 손가락이 테두리 가까이를 쥐게 되어
  쥘 때 테두리가 가장 많이 찌그러집니다.
- 9 oz의 쥐는 높이(40 mm)는 2026-10-24에 40 / 47 / 54 / 60 mm를 비교해 고른 값입니다(47 mm 관절 토크 튐, 54 mm 들지 못함,
  60 mm 검지가 테두리를 넘음). 이번 강성에서는 다시 비교하지 않았습니다.
- 9 oz는 들어 올린 뒤 약지가 컵 바닥 아래로 내려갑니다. 컵 바닥과 손가락의 접촉은 계산하지 않습니다.
- 2026-10-24 판에서 9 oz를 내려놓는 동안 접촉력이 7.0 N과 10.8 N을 오가던 현상은 힘 계산을 고친 뒤 사라졌습니다(4.2 N으로 일정).

데이터: [9 oz](data/pet-9oz-grasp.csv) · [16 oz](data/pet-cup-grasp.csv) · [20 oz](data/pet-20oz-grasp.csv) · [24 oz](data/pet-24oz-grasp.csv)

## 종이컵과 비교

![접촉력 합과 테두리 변형: 종이컵 대 PET 컵(빈 컵·물 1/3·물 2/3)](images/pet-vs-paper.png){ loading=lazy }

| | 종이컵 16 oz (빈 컵) | PET 컵 16 oz (빈 컵) |
|---|---|---|
| 지름을 6.35 mm 줄이는 힘 (높이의 2/3 지점) | 4.4 N (시판 컵 시험값 3.5–5.3 N에 맞춤) | 3.2 N (추정값, 열성형 플라스틱 컵 문헌값 3–4.5 N 범위) |
| 쥐기 / 꽉 쥐기 설정 | 0.10 / 0.35 N·m | 0.03 / 0.06 N·m |
| 쥐었을 때 접촉력 / 테두리 | 16.8 N / 4.2 mm | 5.4 N / 1.3 mm |
| 꽉 쥐었을 때 접촉력 / 테두리 | 70.0 N / 8.4 mm | 10.6 N / 3.4 mm |
| 되돌렸을 때 테두리 | 4.9 mm | 2.1 mm |

- 두 컵의 옆벽 강성은 비슷한 크기(3.2 대 4.4 N)입니다. PET 컵은 관절 토크를 1/3–1/6로 낮춰 쥐었기 때문에 힘과 변형이 작습니다.
- 2026-10-24 판의 PET 컵 강성(0.7 N)은 문헌값보다 3–6배 낮은 추정이었고, 그때는 PET 컵이 1/3 이하의 힘으로 종이컵보다 더 찌그러졌습니다.

데이터(스텝·단계·설정·접촉력 합과 손가락별·테두리 변형·컵 높이·마찰이 받친 힘·수면 높이·컵을 밀어 올린 힘·힘 평형 미수렴 표시·관절 16개 토크):
[빈 컵](data/pet-cup-grasp.csv) · [물 1/3](data/pet-water13-grasp.csv) · [물 2/3](data/pet-water23-grasp.csv)

!!! warning "한계"
    - **PET 컵의 옆벽 강성은 실측값이 아닙니다.** 같은 계열 플라스틱 컵의 공개 문헌값 범위에서 고른 추정값입니다(2026-10-25 수정,
      [추정값·힘 점검](check.md)). 종이컵은 시판 컵의 시험값에 맞췄습니다. 실물 PET 컵을 재는 것이 다음 단계입니다.
    - 컵 벽은 **탄성만** 표현합니다. 모델이 정확한 범위는 테두리 변위 약 3.0–3.4 mm입니다. 꽉 쥐기에서 16·20·24 oz는 그 근처(3.1–3.7 mm),
      9 oz(3.5)·물 2/3(4.4)은 조금 넘습니다.
    - 손가락 관절 토크는 설정에 맞춰 조절되지만, 꽉 쥐는 구간에서 순간적으로 설정의 1.5–3배까지 기록되는 스텝이 있습니다.
    - 물은 무게로만 들어갑니다. 출렁임·관성은 없고, 컵은 기울지 않습니다. 들어 올린 뒤에는 미끄러짐을 다시 계산하지 않으므로,
      여유가 1보다 작아지는 설정은 결과로 쓰지 않았습니다.
    - 관절 토크는 관절 센서 값이 아니라 시뮬레이션의 접촉력에서 계산한 값입니다.
