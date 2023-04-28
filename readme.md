# KDT AI 7th weekly assignment

## 1. 데이터 전처리

* 모든 결측치를 포함한 데이터를 삭제하였습니다.
* delivered_duration 속성의 생성을 위해 created_at과 actual delivery_time의 값을 datetime으로 바꾸고, 두 값의 차를 초의 형태로 변환하였습니다.
* store_primary_category는 one-hot-encoding으로 변환하였습니다.
* store_id는 배제하였습니다.
* 다른 모델의 예측값 역시 배제하였습니다.

## 2. 학습 모델 및 손실함수

### 2.0. 공통 

* 손실함수는 weighted rmse를 사용하였습니다.
* under prediction한 값에 대하여 가중치를 부여하여, 더 높은 손실값을 가지도록 하였습니다.(base_weight = 4)
* 이외에는 평균을 구할 때 부여한 가중치의 합을 추가로 나누어주는 과정 외에 모두 mse와 동일합니다.
* 학습환경은 google colab으로 진행하였습니다.
* RMSE는 두 delivered_duration(단위 : second) 값으로 진행하였기에, 값이 클 수 있습니다.

### 2.1. linear regression

* linear regression은 Ridge regression의 grid search 방식을 채용하여, 원하는 loss가 가장 낮게 나오는 값을 selection하였습니다.
* cv = 10으로 두고 진행하였습니다.


### 2.2. MLP

* MLP 모델을 통하여 linear regression을 진행하였습니다.
* 손실함수는 앞서 말씀드린 weighted rmse, 옵티마이저는 Adam을 사용하였습니다.


## 3. 결과

| metric | linear_regression | MLP |
| --- | --- | --- |
| RMSE | 1142.07 | 1250.84  |
| Under-prediction percentage(%) | 42.06 | 18.24 |
