# 📘 고른 공간

## 주소

https://na06078.github.io/Rey_Blog/my-open-space/

## 어디를 골랐나

- 실내 공간을 촬영했습니다.
- 대표 프레임에서 사람 얼굴과 차량 번호판은 확인되지 않았습니다.
- 다만 달력과 생활용품이 포함된 사적 공간이므로, 공개 전 화면을 직접 확인하는 절차가 필요합니다.

## 어떻게 찍었나

- 길이 `19.13초`, 원본 `1080×1920`, `30fps`, 뽑은 장수 `24장`
- MapAnything 입력: longest-side `518px` (`294×518`)
- 카메라가 퍼진 정도: 미측정
- MapAnything 원시 점: `3,486,931개`
- voxel downsample: 적용하지 않음
- 나온 초기 Gaussian: `3,486,931개`
- 초기 Gaussian PLY는 3DGS 학습 결과가 아니라 위치·색상에 기본 Gaussian 속성을 부여한 표현입니다.

## 형식별로 잰 값

| 형식 | 파일 크기 | 알갱이 개수 | 알갱이당 바이트 |
|---|---:|---:|---:|
| `.ply` | 195,268,499 bytes | 3,486,931 | 56.00 |
| `.compressed.ply` | 56,772,269 bytes | 3,486,931 | 16.28 |
| `.sog` | 16,490,623 bytes | 3,486,931 | 4.73 |
| `.spz` | 23,469,160 bytes | 3,486,931 | 6.73 |

`SplatTransform v3.4.2`의 `numGaussians`와 `lodCounts`를 확인했으며, 네 형식의 알갱이 수는 모두 `3,486,931개`로 동일합니다.

## 폰에서 첫 화면까지

- 내 폰: 미측정
- 남의 폰: 미측정

## 안 나온 자리

- 창문 주변의 역광과 실내의 어두운 영역에서 세부 구조가 약하게 보입니다.
- 벽·유리·단색 영역은 특징점이 부족해 검은 배경이나 빈 영역이 남을 수 있습니다.
- 촬영 중 흔들림과 실내 조명 차이로 일부 표면이 얼룩이나 떠다니는 점처럼 보일 수 있습니다.
- 이번 결과는 학습된 3DGS가 아니라 초기 Gaussian 표현이므로, 실제 3DGS 학습 결과와 품질이 다를 수 있습니다.

## 확인 방법

페이지를 열면 `scene.sog`가 자동으로 로드됩니다. 다른 형식은 파일 영역에 끌어 놓아 비교할 수 있습니다.

- `.ply`
- `.compressed.ply`
- `.sog`
- `.spz`

## 사용한 자료

- MapAnything Apache: https://huggingface.co/facebook/map-anything-apache
- SplatTransform: https://github.com/playcanvas/splat-transform
- Spark viewer: https://github.com/sparkjsdev/spark
