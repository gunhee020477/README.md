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

# 📌 Streamlit 전체 코드

아래는 본 프로젝트의 전체 코드입니다.

```python
import os
import streamlit as st
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import plotly.express as px

# ---------------------------------------------------
# 기본 설정
# ---------------------------------------------------
st.set_page_config(page_title="해외여행 분석 시스템", layout="wide")

st.title("🌍 해외여행 데이터 분석 시스템 ")
st.write("사이드바 메뉴를 이용해 분석 기능을 선택하세요.")

# ---------------------------------------------------
# 파일 경로 자동 설정
# ---------------------------------------------------
BASE_PATH = os.path.dirname(__file__)

FILE1 = os.path.join(BASE_PATH, "한국관광공사_국민 해외관광객 연도별 상세 집계.csv")
FILE2 = os.path.join(BASE_PATH, "한국관광공사_국가별 해외여행 활용 SNS 및 동영상플랫폼_20250915.csv")

@st.cache_data
def load_files():
    if not os.path.exists(FILE1):
        return None, None, f"❌ 파일 없음: {FILE1}"
    if not os.path.exists(FILE2):
        return None, None, f"❌ 파일 없음: {FILE2}"

    df1 = pd.read_csv(FILE1, encoding="cp949")
    df2 = pd.read_csv(FILE2, encoding="cp949")
    return df1, df2, None

df1, df2, error = load_files()

if error:
    st.error(error)
    st.stop()

# ---------------------------------------------------
# 사이드바 메뉴
# ---------------------------------------------------
menu = st.sidebar.selectbox(
    "📌 메뉴 선택",
    ["데이터 미리보기", "국가 검색", "세계 지도 시각화", "국가 추천 기능"]
)

# ---------------------------------------------------
# 1) 데이터 미리보기
# ---------------------------------------------------
if menu == "데이터 미리보기":
    st.header("📁 데이터 미리보기")

    tab1, tab2 = st.tabs(["국민 해외관광객", "국가별 SNS 활용도"])

    with tab1:
        st.subheader("국민 해외관광객 연도별 데이터")
        st.dataframe(df1)

    with tab2:
        st.subheader("국가별 SNS 활용 데이터")
        st.dataframe(df2)

# ---------------------------------------------------
# 2) 국가 검색 기능
# ---------------------------------------------------
elif menu == "국가 검색":
    st.header("🔍 국가 검색 기능")

    search_keyword = st.text_input("검색할 국가명을 입력하세요 (예: 일본, 미국, 베트남)")

    if search_keyword:
        result = df2[df2["국가명"].str.contains(search_keyword, case=False)]

        if len(result) == 0:
            st.warning("❗ 검색 결과가 없습니다.")
        else:
            st.success(f"🔎 '{search_keyword}' 검색 결과")
            st.dataframe(result)

            numeric_cols = result.select_dtypes(include="number").columns.tolist()
            numeric_cols = [col for col in numeric_cols if col not in ["기준연도"]]

            st.subheader("📊 SNS 및 플랫폼 활용도 그래프")
            fig_bar = px.bar(
                result,
                x="국가명",
                y=numeric_cols,
                barmode="group",
                title=f"{search_keyword} SNS 및 플랫폼 활용도"
            )
            st.plotly_chart(fig_bar, use_container_width=True)

            st.subheader("📉 연도별 변화 추세")
            fig_line = px.line(
                result,
                x="기준연도",
                y=numeric_cols,
                title=f"{search_keyword} 연도별 플랫폼 활용 변화"
            )
            st.plotly_chart(fig_line, use_container_width=True)

# ---------------------------------------------------
# 3) 세계 지도 시각화
# ---------------------------------------------------
elif menu == "세계 지도 시각화":
    st.header("🗺️ 세계 지도 기반 SNS 활용도")

    df2["SNS총점"] = df2.select_dtypes(include="number").sum(axis=1)

    fig_world = px.choropleth(
        df2,
        locations="국가명",
        locationmode="country names",
        color="SNS총점",
        hover_name="국가명",
        title="국가별 SNS 활용도 지도",
        color_continuous_scale="Blues"
    )
    st.plotly_chart(fig_world, use_container_width=True)

# ---------------------------------------------------
# 4) 국가 추천 기능
# ---------------------------------------------------
elif menu == "국가 추천 기능":
    st.header("🌟 연령대 · 성별 기반 해외여행 국가 추천")

    col1, col2 = st.columns(2)
    rec_gender = col1.selectbox("성별 선택", df1["성별"].unique())
    rec_age = col2.selectbox("연령대 선택", df1["연령대"].unique())

    df1["총해외출국자수"] = df1.select_dtypes(include="number").sum(axis=1)
    user_strength = df1[(df1["성별"] == rec_gender) & (df1["연령대"] == rec_age)]["총해외출국자수"].sum()

    df2["SNS총점"] = df2.select_dtypes(include="number").sum(axis=1)
    sns_weight = 0.5

    df2["추천점수"] = df2["SNS총점"] * sns_weight + (user_strength / 10000)
    rec_top5 = df2.sort_values("추천점수", ascending=False).head(5)

    st.subheader("🔥 추천 국가 TOP 5")
    st.table(rec_top5[["국가명", "SNS총점", "추천점수"]])

    fig_rec = px.bar(
        rec_top5,
        x="국가명",
        y="추천점수",
        title="연령대·성별 기반 추천 국가 TOP 5",
        color="국가명"
    )
    st.plotly_chart(fig_rec, use_container_width=True)
