# 바닐라 JS 프로젝트 성능 개선
- url: https://front-5th-chapter4-2-basic.vercel.app/

<br/>

## 성능 개선 보고서

### ✅ 성능 측정 도구: Google PageSpeed Insights
배포 후 Google PageSpeed Insights 도구를 통해 성능을 측정해본 결과, 다음과 같이 여러 성능 개선 권고사항을 확인할 수 있었습니다.

<br/>

### 📉 개선 전 성능 (점수: 54)

<img width="692" alt="스크린샷 2025-05-31 오후 8 58 13" src="https://github.com/user-attachments/assets/47c8e493-2f17-4f61-9c56-d67338eaf906" />

<br/>
<br/>

### ⚠️ 주요 문제 <br/>
- 🔴 **대규모 레이아웃 변경 발생** (5건)
- 🔴 **차세대 형식의 이미지 미사용** → 약 1,990KiB 절감 가능
- 🔴 **비효율적인 이미지 인코딩** → 약 1,410KiB 절감 가능
- 🔴 **오프스크린 이미지 미지연** → 약 1,174KiB 절감 가능
- 🔴 **이미지 크기 부적절** → 약 861KiB 절감 가능
- 🔴 **렌더링 차단 리소스 존재** → 410ms 절감 가능
- 🔴 **사용하지 않는 JS 포함** → 56KiB 절감 가능
- 🟠 **이미지 요소에 width/height 누락**
- 🟠 **비효율적인 캐시 정책 사용**

<br/>

### 🔧 개선 작업 내용
1. 이미지 리소스 최적화
    - 모든 JPG, PNG 이미지를 용량이 작은 WEBP 포맷으로 변환
    - mogrify 명령어를 사용해 배치 처리
    - 이미지의 width와 height 속성을 명시적으로 지정하여 CLS(레이아웃 쉬프트) 방지

2. 로딩 타이밍 최적화
    - 초기 페이지 로딩 시 모든 요소를 한 번에 렌더링하지 않음
    - 사용자의 스크롤 이벤트를 감지하여 해당 콘텐츠를 지연 로딩
    - 무거운 연산은 event loop를 활용하여 블로킹 없이 처리

<br />

### 📈 성능 개선 전후 비교
| 측정 항목                    | 개선 전  | 개선 후  | 변화          |
| ------------------------ | ----- | ----- | ----------- |
| First Contentful Paint   | 0.7초  | 0.7초  | 유지          |
| Largest Contentful Paint | 3.1초  | 0.8초  | **▼ 2.3초**  |
| Total Blocking Time      | 230ms | 0ms   | **▼ 230ms** |
| Speed Index              | 0.9초  | 0.7초  | **▼ 0.2초**  |
| Cumulative Layout Shift  | 0.477 | 0.011 | **▼ 0.466** |

<br />

### 📊 최종 결과 (점수: 99)
<img width="692" alt="스크린샷 2025-06-01 오후 3 34 56" src="https://github.com/user-attachments/assets/4d51c6cc-7a4d-4480-86d2-4768d37d3969" />

<br />
<br />

### 🧾 결론
- 불필요한 리소스를 줄이고 이미지와 자바스크립트의 로딩 시점을 조절함으로써 성능 점수 54 → 99로 대폭 향상
- 특히 LCP(주요 콘텐츠 렌더링 시간), TBT(총 차단 시간), CLS(레이아웃 안정성)이 크게 개선되었음
- 사용자의 체감 성능과 페이지 반응성 모두 눈에 띄게 향상되었음



