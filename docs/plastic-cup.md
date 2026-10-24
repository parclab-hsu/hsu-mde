# 플라스틱 컵 쥐기

[종이컵 쥐기](cup.md)와 같은 동작으로 투명 **PET 16 oz 냉음료 컵**(윗지름 98 mm, 아랫지름 58 mm, 높이 115 mm, 벽 두께 0.25 mm)을
쥡니다. 옆에서 감싸 쥐고, 80 mm 들어 올려 더 세게 쥐었다가 풀고, 내려놓습니다. PET 컵은 종이컵보다 훨씬 무르기 때문에 관절 토크를
**쥐기 0.03 N·m, 꽉 쥐기 0.06 N·m**로 낮췄습니다(종이컵은 0.10 / 0.35 N·m). 컵 벽의 색은 변형 방향(적색: 바깥으로, 청색: 안쪽으로)입니다.
기준: 2026-10-24, Isaac Sim 5.0.0.

<video class="mde-video" src="../media/pet-cup-grasp.mp4" poster="../media/pet-cup-grasp.jpg" controls muted loop playsinline></video>

<div class="mde-grid">
<figure><img src="../images/pet-cup-grasped.jpg" loading="lazy" alt="쥐었을 때"><figcaption>쥐었을 때 (관절 토크 0.03 N·m)</figcaption></figure>
<figure><img src="../images/pet-cup-lifted.jpg" loading="lazy" alt="들었을 때"><figcaption>80 mm 들어 올림</figcaption></figure>
<figure><img src="../images/pet-cup-squeezed.jpg" loading="lazy" alt="꽉 쥐었을 때"><figcaption>꽉 쥐었을 때 (0.06 N·m)</figcaption></figure>
<figure><img src="../images/pet-cup-squeezed-top.jpg" loading="lazy" alt="꽉 쥐었을 때 위에서"><figcaption>위에서 본 모습 — 테두리가 타원이 된다</figcaption></figure>
<figure><img src="../images/pet-cup-eased.jpg" loading="lazy" alt="되돌렸을 때"><figcaption>0.03 N·m로 되돌림 — 찌그러진 모양이 거의 그대로 남는다</figcaption></figure>
<figure><img src="../images/pet-cup-released.jpg" loading="lazy" alt="놓은 뒤"><figcaption>내려놓고 손을 편 뒤 — 원래 모양</figcaption></figure>
</div>

## 결과

| 시점 | 관절 토크 설정 | 접촉력 합 | 검지 / 중지 / 약지 / 엄지 / 손바닥 | 테두리 변형(안쪽 / 바깥) |
|---|---|---|---|---|
| 쥐었을 때 | 0.03 N·m | 6.5 N | 0.7 / 1.4 / 0.5 / 1.9 / 1.9 N | 6.5 / 6.3 mm |
| 들었을 때 | 0.03 N·m | 6.2 N | 0.6 / 1.2 / 0.8 / 1.7 / 1.8 N | 6.5 / 6.3 mm |
| 꽉 쥐었을 때 | 0.06 N·m | 10.0 N | 1.6 / 1.7 / 1.4 / 2.7 / 2.6 N | 8.1 / 8.4 mm |
| 되돌렸을 때 | 0.03 N·m | 5.4 N | 0.5 / 0.5 / 1.0 / 1.4 / 2.0 N | 7.9 / 7.1 mm |
| 놓은 뒤 | — | 0 N | — | 0 mm (탄성 복원) |

- 컵 무게(약 12 g, 0.12 N)를 들려면 마찰계수 0.5에서 쥐는 힘 0.24 N이면 됩니다. 실제 쥐는 힘 6.2 N은 그 25배 이상이라
  미끄러지지 않습니다.
- 관절 토크 최대는 0.15 N·m입니다(종이컵 1.11 N·m).

## 종이컵과 비교

![접촉력 합과 테두리 변형: 종이컵 대 PET 컵](images/pet-vs-paper.png){ loading=lazy }

| | 종이컵 16 oz | PET 컵 16 oz |
|---|---|---|
| 지름을 6.35 mm 줄이는 힘 (높이의 2/3 지점) | 4.4 N (시판 컵 시험값 3.5–5.3 N에 맞춤) | 0.7 N (추정값, 0.3–1.9 N) |
| 쥐었을 때 접촉력 / 테두리 | 17.2 N / 5.6 mm | 6.5 N / 6.5 mm |
| 꽉 쥐었을 때 접촉력 / 테두리 | 76.8 N / 9.1 mm | 10.0 N / 8.4 mm |
| 되돌렸을 때 테두리 | 4.2 mm | 7.9 mm |

- PET 컵은 1/3 이하의 힘으로 종이컵보다 더 찌그러집니다.
- 힘을 되돌려도 PET 컵은 찌그러진 모양이 거의 남습니다. 무른 컵은 적은 힘으로도 그 모양을 유지할 수 있어, 쥐는 토크가 설정값
  아래로 내려가면 손가락이 더 물러나지 않기 때문입니다.

데이터: [pet-cup-grasp.csv](data/pet-cup-grasp.csv) — 스텝·단계·설정·접촉력(합·손가락별)·테두리 변형·관절 16개 토크

!!! warning "한계"
    - **PET 컵의 옆벽 강성은 실측값이 아닙니다.** 컵 치수·벽 두께·PET 탄성계수에서 계산한 추정값이며, 그 범위만 해도 6배 차이가
      납니다. 종이컵은 시판 컵의 시험값에 맞췄습니다.
    - 컵 벽은 **탄성만** 표현합니다. 벽 변위 8 mm 이상은 모델이 정확한 범위(약 3.4 mm)를 크게 넘는 외삽입니다. 실제 PET 컵은
      이 정도면 옆벽이 꺾이거나 찌그러진 채 남습니다.
    - 컵은 투명하게 그리지 않았습니다(연청색).
    - 관절 토크는 관절 센서 값이 아니라 시뮬레이션의 접촉 법선력에서 계산한 값입니다(마찰 제외).
