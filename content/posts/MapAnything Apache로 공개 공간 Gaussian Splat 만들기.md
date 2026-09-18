# 🧾 MapAnything Apache로 공개 공간 Gaussian Splat 만들기

## 시작하며

이번 과제에서는 짧은 실내 촬영 영상에서 여러 장의 프레임을 만들고, `facebook/map-anything-apache`로 3D 공간을 재구성했습니다. 완성된 결과는 별도의 웹 뷰어에서 바로 확인할 수 있도록 GitHub Pages에 연결했습니다.

[웹 뷰어에서 장면 확인하기](https://na06078.github.io/Rey_Blog/my-open-space/)

## 촬영과 입력

- 원본 영상: `19.13초`
- 원본 해상도: `1080×1920`, `30fps`
- 추출 프레임: `24장`
- MapAnything 입력 해상도: longest-side `518px` (`294×518`)
- MapAnything 추론 시간: `10.269초`

원본 프레임은 1080×1920으로 보존했지만, MapAnything 모델에는 공식 기본 입력 크기에 맞춰 518 해상도로 전달했습니다. AMD ROCm 환경에서는 AOTriton attention과 hipBLAS 선호 설정을 적용해 24장 입력을 처리했습니다.

## 재구성 흐름

```text
촬영 영상
  → 24장 프레임 추출
  → MapAnything Apache metric 3D 재구성
  → point-cloud PLY
  → Gaussian 속성 초기화
  → SplatTransform 형식 변환
  → SOG 웹 뷰어
```

MapAnything 공식 export 결과는 위치와 색상 중심의 일반 point-cloud PLY입니다. 이번 제출본은 각 점에 scale, rotation, opacity, DC 색상 계수를 부여한 **초기 Gaussian PLY**입니다. 별도의 3DGS 학습 결과는 아니므로, 학습된 Gaussian Splat 모델과 구분해 기록했습니다.

## 형식별 결과

이번 공개 페이지에는 raw PLY 대신 용량이 작은 `.sog`를 넣었습니다.

| 형식 | 파일 크기 | Gaussian 수 | Gaussian당 바이트 |
|---|---:|---:|---:|
| `.ply` | 195,268,499 bytes | 3,486,931 | 56.00 |
| `.compressed.ply` | 56,772,269 bytes | 3,486,931 | 16.28 |
| `.sog` | 16,490,623 bytes | 3,486,931 | 4.73 |
| `.spz` | 23,469,160 bytes | 3,486,931 | 6.73 |

`SplatTransform v3.4.2`의 `numGaussians`와 `lodCounts`를 확인했으며, 네 형식의 Gaussian 수는 모두 `3,486,931개`로 동일했습니다.

raw `.ply`는 GitHub의 단일 파일 제한을 넘기므로 공개 파일로 사용하지 않았습니다. 웹 페이지에는 `scene.sog`를 기본 장면으로 연결했습니다.

## 웹 뷰어

웹 페이지는 Spark renderer를 사용합니다. 페이지에 들어가면 `scene.sog`가 자동으로 로드되며, `.ply`, `.compressed.ply`, `.sog`, `.spz` 파일을 끌어 놓아 장면을 교체할 수 있습니다.

- 주소: https://na06078.github.io/Rey_Blog/my-open-space/
- 형식 변환과 웹 표시에서 Gaussian 수가 보존되는지 확인했습니다.
- MapAnything의 OpenCV 좌표계와 Spark/Three.js 좌표계가 달라 뷰어에서 X축 180° 좌표 보정을 적용했습니다.

## 확인한 한계

- 촬영 공간은 실내 공간이며, 대표 프레임에서 사람 얼굴과 차량 번호판은 확인되지 않았습니다.
- 달력과 생활용품이 포함되어 있으므로 공개 전에 화면을 직접 확인해야 합니다.
- 창문 역광, 실내의 어두운 영역, 촬영 중 흔들림 때문에 벽과 가구 가장자리에 얼룩이나 떠다니는 점이 남을 수 있습니다.
- 카메라 퍼짐 정도와 모바일 첫 화면 로딩 시간은 아직 측정하지 않았습니다.
- 초기 Gaussian 표현이므로, 실제 3DGS 학습·densification을 거친 결과와는 품질이 다를 수 있습니다.

## 사용한 자료

- MapAnything Apache: https://huggingface.co/facebook/map-anything-apache
- MapAnything 공식 저장소: https://github.com/facebookresearch/map-anything
- SplatTransform: https://github.com/playcanvas/splat-transform
- Spark viewer: https://github.com/sparkjsdev/spark
