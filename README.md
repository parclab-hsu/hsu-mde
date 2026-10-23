# MDE — 한성대학교 PARC Lab

Manufacturing Deformation Engine(MDE)의 시뮬레이션 실험 결과를 공개하는 사이트의 원본입니다.

- 사이트: https://parclab-hsu.github.io/hsu-mde/
- 연구실: https://parclab-hsu.github.io/

이 저장소에는 공개용 결과(영상·이미지·접촉력·관절 토크 데이터)와 페이지 원본만 있습니다. 엔진 소스 코드는 포함하지 않습니다.
`main`에 push하면 GitHub Actions가 MkDocs로 빌드해 GitHub Pages에 배포합니다.

```bash
pip install -r requirements.txt
mkdocs serve        # http://127.0.0.1:8000/hsu-mde/
```

Copyright © 2026 한성대학교 PARC Lab (Hansung University). All rights reserved.
영상·이미지의 로봇 손은 Isaac Sim 5.0에 포함된 Allegro Hand(Wonik Robotics) 시뮬레이션 모델입니다.
