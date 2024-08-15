# 웹 성능 측정 및 성능 개선 

## 프로젝트 배포
배포 url: https://web-performance-initial.web.app

## 평가지표 확인
https://pagespeed.web.dev/analysis/https-web-performance-initial-web-app/o5oy7ah26s?form_factor=desktop

### 프로젝트 초기 성능 (데스크톱 기준)
<img width="858" alt="스크린샷 2024-08-16 오전 1 18 18" src="https://github.com/user-attachments/assets/de2ab69a-01c0-4107-9cd6-5c0bc40c1e89">
 
### 프로젝트 최종 성능 (데스크톱 기준)
<img width="856" alt="스크린샷 2024-08-16 오전 1 19 30" src="https://github.com/user-attachments/assets/5c77fa3b-886b-4a6a-abe2-d1bd9a6454ff">

### 프로젝트 초기 진단 사항
<img width="860" alt="스크린샷 2024-08-16 오전 1 22 57" src="https://github.com/user-attachments/assets/a688f066-98e5-49fe-a432-4daeae8a9618">

## 변경 사항
1. 이미지 사이즈 조정
   - 모바일, 태블릿, 데스크톱에서 실질적으로 사용되는 최대 사이즈로 이미지 사이즈 조정 
2. 이미지 포맷 변환, 이미지 압축
   - jpg -> webp 확장자 변경 (https://www.freeconvert.com/jpg-to-webp)
   - 이미지 압축하여 용량 감소 (https://tinypng.com/)
3. 스크린 사이즈에 따른 이미지 렌더링 (responsive images)
   - 기존 모든 사이즈의 이미지를 불러오던 방식에서 `<picture>` element를 사용하여 해당 스크린 사이즈에 부합하는 이미지만 로드
4. 이미지의 고정된 width와 height 설정
   - 레이아웃 시프트 방지 (CLS 개선)
   - 렌더링 성능 향상
   - 이미지 로드 속도 최적화
5. 이미지 조건부 로딩 적용
   - `img.loading = "lazy"`를 추가하여, 브라우저가 이미지를 필요할 때 (즉, 사용자가 이미지를 스크롤해서 볼 때) 로드함
6. JavaScript 코드의 초기 실행 시간 감소
   - 페이지의 초기 로딩 시 무거운 연산을 즉시 실행하지 않고, 사용자가 스크롤하여 특정 요소가 화면에 나타날 때까지 연산을 지연시킴
7. 폰트 로딩 성능 최적화
   - 외부 폰트 로딩을 제거하고, 로컬 폰트를 사용함으로써 외부 네트워크 요청을 줄여 로딩 시간을 단축시키고, 폰트 로딩 실패 시에도 안정적인 텍스트 표시를 보장함
8. 비필수적인 서비스(쿠키 동의 및 Google 태그 관리자)의 실행을 지연시켜 초기 페이지 로딩 성능을 최적화
   - `defer` 속성 추가: 스크립트가 병렬로 다운로드되지만, HTML 문서의 파싱이 완료된 후에 스크립트가 실행되도록 함. 스크립트가 HTML 파싱을 차단하지 않도록 하여 페이지의 초기 로딩 성능을 개선
   - `DOMContentLoaded` 이벤트 리스너 추가: 쿠키 동의 배너 설정 코드가 HTML 파싱이 완료된 후 실행되도록 지연시켜, 초기 렌더링 성능에 미치는 영향을 최소화 함
