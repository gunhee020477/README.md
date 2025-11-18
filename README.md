# 🌍 해외여행 데이터 분석 시스템 (Travel Data Analysis System)

본 프로젝트는 국민 해외여행 데이터와 국가별 SNS 활용 데이터를 기반으로  
해외여행 트렌드, 국가 선호도, SNS 영향력 등을 종합적으로 분석하는 시스템입니다.  
Streamlit을 활용해 시각적 인터페이스를 제공하여 누구나 쉽게 해외여행 데이터를 탐색할 수 있도록 구성했습니다.

---

## 📌 프로젝트 소개

이 프로젝트는 **한국관광공사 통계 데이터**를 활용하여  
- 해외여행자 수 변화  
- 국가별 SNS 활용도  
- 연령대·성별 기반 추천 국가  
- 세계 지도 기반 데이터 시각화  

등을 제공합니다.

또한 웹 애플리케이션 형태로 Streamlit을 배포하여  
사용자가 국가 검색, 추천 국가 확인, 대시보드 시각화를 쉽게 수행할 수 있습니다.

---

## 🎥 시연 영상

👉 **YouTube 시연 영상**  
https://youtube.com

---

## 🌐 Streamlit 배포 주소 (웹 서비스)

👉 **https://your-streamlit-url.streamlit.app**  
(배포된 URL로 교체하세요!)

---

## 👥 팀원 소개

| 이름 | 역할 |
|------|---------------------------|
| 차은우 | 데이터 수집 및 전처리, 시각화 |
| 변우석 | 추천 알고리즘, Streamlit UI 개발 |
| 팀원A | 통계 분석, 보고서 작성 |
| 팀원B | UX/UI 기획 및 발표 자료 제작 |

---

## 📁 프로젝트 구조

# 🧠 기술 스택

- **Python**
  - Pandas, Numpy
  - Matplotlib, Seaborn
  - Plotly
- **Streamlit**
- **GitHub**
- **CSV 기반 데이터 분석**

---

# 🖥️ Streamlit 주요 기능

### ✔ 1) 데이터 미리보기  
- 해외여행자 연도별 데이터  
- 국가별 SNS 활용 데이터  

### ✔ 2) 국가 검색  
- 국가명 검색  
- SNS 활용도 차트 제공 (Bar/Line Chart)

### ✔ 3) 세계 지도 시각화  
- Plotly Choropleth로 국가별 SNS 총점 표시

### ✔ 4) 국가 추천 기능  
- 연령대 & 성별 기반 추천  
- 추천 점수 가중치 적용  
- TOP 5 국가 제공

---

## 📸 Streamlit 실행 화면 예시

아래는 본 프로젝트의 Streamlit 대시보드 기능별 결과 화면 예시입니다.  
(이미지는 샘플이며, 실제 실행 후 캡처하여 교체 가능합니다.)

---

### 🏠 1) 메인 화면

사용자가 사이드바에서 메뉴를 선택할 수 있는 초기 화면입니다.

![Main Screen](https://via.placeholder.com/1200x600.png?text=Main+Screen+-+Travel+Analysis+Dashboard)

---

### 📁 2) 데이터 미리보기

CSV 두 종류:
- 국민 해외관광객 연도별 데이터
- 국가별 SNS 및 플랫폼 활용 데이터

을 탭으로 구분하여 확인할 수 있는 화면입니다.

![Data Preview](https://via.placeholder.com/1200x600.png?text=Data+Preview+-+df1+%26+df2)

---

### 🔍 3) 국가 검색 기능

- 특정 국가명 입력 → 해당 국가의 SNS 활용 지표 필터링
- Bar Chart / Line Chart 자동 생성
- 연도별 플랫폼 활용도 변화 확인 가능

![Search Screen](https://via.placeholder.com/1200x600.png?text=Country+Search+-+SNS+Usage+Graphs)

---

### 🗺️ 4) 세계 지도 시각화

Plotly Choropleth 지도 기반  
각 나라의 SNS 총점(SNS총점) 분포를 시각적으로 표현합니다.

![World Map](https://via.placeholder.com/1200x600.png?text=World+Map+-+SNS+Score+Visualization)

---

### 🌟 5) 국가 추천 기능

- 성별 + 연령대 입력  
- 해외 출국자수 기반 User Strength 계산  
- SNS 점수와 가중치를 조합해 추천 국가 산출  
- TOP 5 국가를 표와 막대그래프로 제공

![Recommend Screen](https://via.placeholder.com/1200x600.png?text=Recommended+TOP+5+Countries)
