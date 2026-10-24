# 종이컵 쥐기

Allegro Hand가 탁자 위 16 oz 종이컵(윗지름 90 mm, 아랫지름 60 mm, 높이 136 mm)을 옆에서 감싸 쥐고, 80 mm 들어 올린 뒤
더 세게 쥐었다가 풀고, 내려놓는 동작입니다. 각 손가락 관절은 정해진 토크까지만 힘을 내는 **토크 제한 쥐기**로 닫습니다.
컵 벽의 색은 변형 방향(적색: 바깥으로, 청색: 안쪽으로)입니다. 기준: 2026-10-24, Isaac Sim 5.0.0.

<video class="mde-video" src="../media/cup-grasp.mp4" poster="../media/cup-grasp.jpg" controls muted loop playsinline></video>

<div class="mde-grid">
<figure><img src="../images/cup-grasped.jpg" loading="lazy" alt="쥐었을 때"><figcaption>쥐었을 때 (관절 토크 0.10 N·m)</figcaption></figure>
<figure><img src="../images/cup-lifted.jpg" loading="lazy" alt="들었을 때"><figcaption>80 mm 들어 올림</figcaption></figure>
<figure><img src="../images/cup-squeezed.jpg" loading="lazy" alt="꽉 쥐었을 때"><figcaption>꽉 쥐었을 때 (0.35 N·m)</figcaption></figure>
<figure><img src="../images/cup-squeezed-top.jpg" loading="lazy" alt="꽉 쥐었을 때 위에서"><figcaption>위에서 본 모습 — 테두리가 타원이 된다. 손가락 끝은 테두리보다 높아 원근상 입구 안쪽에 겹쳐 보인다</figcaption></figure>
<figure><img src="../images/cup-eased.jpg" loading="lazy" alt="되돌렸을 때"><figcaption>0.10 N·m로 되돌림</figcaption></figure>
<figure><img src="../images/cup-released.jpg" loading="lazy" alt="놓은 뒤"><figcaption>내려놓고 손을 편 뒤 — 원래 모양</figcaption></figure>
</div>

## 동작 순서

| 단계 | 내용 |
|---|---|
| 접근 | 손을 편 채 옆에서 다가간다 |
| 예비 자세 | 손가락마다 컵에 닿기 직전까지 미리 굽힌다 |
| 쥐기 | 관절 토크 0.10 N·m까지 닫는다. 탁자 위의 가벼운 컵은 엄지에 끌려 손바닥 쪽으로 약 21 mm 미끄러진다 |
| 들기 | 손가락 마찰로 무게를 버틸 수 있으면 80 mm 들어 올린다 |
| 꽉 쥐기 → 되돌리기 | 0.35 N·m까지 올렸다가 0.10 N·m로 되돌린다 |
| 내려놓기 → 펴기 → 물러나기 | 컵을 내려놓고 손을 편다 |

## 결과

| 시점 | 관절 토크 설정 | 접촉력 합 | 검지 / 중지 / 약지 / 엄지 / 손바닥 | 테두리 변형(안쪽 / 바깥) |
|---|---|---|---|---|
| 쥐었을 때 | 0.10 N·m | 17.2 N | 2.3 / 2.4 / 2.3 / 3.4 / 6.8 N | 5.6 / 5.3 mm |
| 들었을 때 | 0.10 N·m | 18.7 N | 3.3 / 1.7 / 2.2 / 4.3 / 7.1 N | 5.6 / 5.3 mm |
| 꽉 쥐었을 때 | 0.35 N·m | 76.8 N | 7.2 / 16.8 / 8.5 / 20.9 / 23.5 N | 9.1 / 8.0 mm |
| 되돌렸을 때 | 0.10 N·m | 15.5 N | 1.8 / 2.6 / 0.8 / 4.3 / 6.0 N | 4.2 / 3.7 mm |
| 놓은 뒤 | — | 0 N | — | 0 mm (탄성 복원) |

- 컵 무게(약 14 g, 0.14 N)를 들려면 마찰계수 0.5에서 쥐는 힘 0.27 N이면 됩니다. 실제 쥐는 힘 17–19 N은 그 60배 이상이라 미끄러지지 않습니다.
- 컵 옆벽의 단단함은 시판 16 oz 종이컵의 옆벽 강성 시험값(지름 6.35 mm를 줄이는 데 3.5–5.3 N)에 맞췄습니다.
- 접촉력과 관절 토크의 시간 이력은 [관절 토크](torque.md)에 있습니다.
- 같은 동작으로 투명 PET 컵을 쥔 결과는 [플라스틱 컵 쥐기](plastic-cup.md)에 있습니다.
- 2026-10-24 판은 손이 컵 벽을 파고든 것처럼 보이던 문제(최대 약 1.6 mm)를 고쳐 다시 찍었습니다. 화면의 손과 컵 벽 겹침은
  전 구간 최대 0.34 mm로, 종이 두께 0.46 mm보다 작습니다.

!!! warning "한계"
    - 컵 벽은 **탄성만** 표현합니다. 실제 종이컵은 이 정도 힘이면 주름이 잡히거나 찌그러집니다. 꽉 쥐기(77 N, 벽 변위 약 9 mm)는 모델이 정확한 범위(약 3 mm)를 크게 넘는 외삽입니다.
    - 컵은 미끄러지기만 하고 기울지는 않습니다. 마찰은 들기 판정과 탁자 미끄러짐에만 쓰고 관절 토크에는 넣지 않았습니다.
    - 물성(종이 탄성계수·두께·질량·마찰)은 잠정값입니다.
