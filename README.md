# tsfresh tutorial

## 사용 목적
![데이터의 다양한 특징](https://tsfresh.readthedocs.io/en/latest/_images/introduction_ts_exa_features.png)

- tsfresh를 사용하면 최대, 최소, 평균 등 다양한 데이터의 특징을 편하게 추출할 수 있음
- pandas, scikit-learn과 사용하기 편함
- 시계열 분류/회귀 모델을 위한 전처리
- 새로운 인사이트 발견

## 사용 방법
### Data format
- 입력 포맷은 pandas.DataFrame 형태
- 해당 dataframe에는 4가지 중요한 columns가 있음


#### 필수 columns
    column_id: 시계열이 속한 entities를 나타냄.
    column_sort: 시계열을 정렬할 수 있는 값. 없으면 오름차순으로 정렬된 것으로 판단. 동일한 간격을 가질 필요는 없으나, 일부 특징은 동일한 간격에서만 의미를 가짐.

#### 부가 columns
    column_value: 시계열의 실제 값
    column_kind: 시계열 유형의 이름

***중요: 이러한 열들에는 `NaN`, `Inf`, `-Inf`가 포함되면 안됩니다.***

### Input option 1. Flat DataFrame
`column_value`와 `column_kind`가 `None`일 경우 해당 데이터를 flat하다고 판단

예) `extract_features(timeseries, column_id="id", column_sort="time", column_value=None)`

### Input option 2. Stacked DataFrame
`column_value`와 `column_kind`를 세팅할 경우 stacked로 판단

예) `extract_features(timeseries, column_id="id", column_sort="time", column_kind="kind", column_value="value")`

### Input option 3. Dictionary of flat DataFrames
`column_kind`를 주지 않고 dict에 문자열로 매핑할 수 있음

예) 데이터의 형태가 `{'x': pandas.DataFrame, 'y': pandas.DataFrame}` 인 경우 `extract_features(timeseries, column_id="id", column_sort="time", column_value="value")`

### Output format
위의 세 가지 입력 형태에 대해 출력 형태는 동일

|id|	x_feature_1|	…|	x_feature_N|	y_feature_1|	…|	y_feature_N|
|----|---|---|---|---|-----------|--------|
|A|	…|	…|	…|	…|	…|	…|
|B|	…|	…|	…|	…|	…|	…|

이 형태는 feature selection 함수인 `tsfresh.select_features()`의 입력 형태

### Overview on extarcted features
https://tsfresh.readthedocs.io/en/latest/text/list_of_features.html 를 참고


---
출처: https://tsfresh.readthedocs.io/en/latest/index.html