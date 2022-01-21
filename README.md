# SCSm_Project

### 주제 : 귀납적 방식으로 인공지능 computing을 통한 최적의 PID 계수 계산

> 레퍼런스
> - PID control
> - COP concept
> - LSTM algorithm
> - Reinforcement algorithm

## 개발 목표
**다양한 환경과 온도조절을 위한 많은 기계적 장치들을 비용대비 효과적으로 시스템 열을 관리하는 것이 목표이다.** 엔지니어들이 기계적 장치를 조절하는데 시간적, 인적, 금전적 비용을 절감하고 여러 환경에서 최고의 퍼포먼스를 보조할 수 있는 인공지능 모델을 만들것이다.
임베딩 시스템에서 온도컨트롤은 최적의 성능 유지를 위해 매우 중요한 요소이다. 온도가 너무 높으면 CPU or MPU의 클럭 속도저하를 일으켜 퍼포먼스를 저하시키고, 배터리의 공급효율을 떨어뜨려 시스템 작동에 문제를 발생시킨다. 따라서 최적의 온도(36.5도)를 유지할 수 있는 시스템이 필요하다. 전기에너지를 소모하여 시스템 운영에 차질이 없는 온도 구간까지 온도를 조절하는 기계적 액츄에이터들(Fan, Valve, Evaporator, hitter 등)을 이용하여 온도를 변화시킬 수 있다. 



![image](https://user-images.githubusercontent.com/90364187/150447996-46914d4c-4489-40a7-8cdf-550a7f177705.png)


### 데이터 예시

![image](https://user-images.githubusercontent.com/90364187/150448554-8f1f47cb-83b1-45a9-a906-a808da03bb2e.png)


> 회귀 문제에서는 실제 값과 모델이 예측하는 값의 차이에 기반을 둔 metric(평가)을 사용합니다. 
> - RSS(단순 오차 제곱 합), MSE(평균 제곱 오차), MAE(평균 절대값 오차)
> - RSS는 예측값과 실제값의 오차의 제곱합, MSE는 RSS를 데이터의 개수만큼 나눈 값, MAE는 예측값과 실제값의 오차의 절대값의 평균입니다.
> - RMSE와 RMAE라는 것도 있는데, 각각 MSE와 MAE에 루트를 씌운 값입니다.
> - MSE의 경우 오차에 제곱이 되기 때문에 이상치(outlier)를 잡아내는 데 효과적입니다. 틀린 걸 더 많이 틀렸다고 알려주는 것입니다. 
> - MAE의 경우 변동치가 큰 지표와 낮은 지표를 같이 예측하는 데 효과적입니다. 둘 다 가장 간단한 평가 방법으로 직관적인 해석이 가능하지만, 평균을 그대로 이용하기 때문에 데이터의 크기에 의존한다는 단점이 있습니다.


### 결측 데이터 처리 => MICE 알고리즘 사용

MICE 는 Multivariate Imputation By Chained Equations 알고리즘의 약자로 , 다른 열의 데이터를보고 각 누락 된 값에 대한 최상의 예측을 추정하여 데이터 세트에서 누락 된 값을 손쉽게 대치 할 수있는 기술

이미지 출처 : 매장 에너지 절감을 위한 LSTM 기반의 전력부하 예측 시스템 설계

- 누락된 데이터의 3가지 유형
	- MCAR (Missing Completely At Random) — 필드의 누락이 완전히 무작위이며 데이터의 다른 값에서 해당 값을 예측할 수 없음을 의미합니다.
	- 무작위 누락 (MAR) — 필드의 누락이 다른 열의 값으로 설명 될 수 있지만 해당 열에서는 설명되지 않음을 의미합니다.
	- MNAR (Not at Random) 누락 — 응답자가 해당 필드를 채우지 않아 데이터가 무작위로 누락되지 않은 이유가 있는지 여부를 나타냅니다. 예를 들어 비만인 경우 체중을 공개 할 가능성이 적습니다.




![MICE 결측치 대체](https://user-images.githubusercontent.com/90364187/150477261-ad1ecc90-49c4-4d4e-b4d3-eac0c5d8a86c.JPG)





출처 : https://ichi.pro/ko/deiteo-seteueseo-gyeol-cheuggabs-eul-daechihaneun-mice-algolijeum-217004654686142







## 개발과정계획
전기차에서 열관리가 필요한 부위는 배터리, 구동모터, 및 전장품, 캐빈

냉각 성능과 소비전력을 최적화할 수 있는 최적운전계획법(Optimal operation scheduling) 적용.

### 전기차 구조와 전기 에너지 흐름


![자동차](https://user-images.githubusercontent.com/90364187/150477051-ae405281-9406-4eb1-b687-9bdb18931fe5.JPG)

![전기 자동차 에너지 흐름](https://user-images.githubusercontent.com/90364187/150477071-a1b5c1fc-a96a-4370-ac38-5038e5a5ea54.JPG)


출처 : 전기자동차용 전자장비 냉각 제어 알고리즘에 관한 연구: Part 1 일반 냉각 제어 로직 유효성 분석

출처 : 최적운전계획법에 의한 전기차의 고전압 배터리셀 온도 관리

> Phase01 : 다양한 환경에서 시스템 운영의 허용 온도 구간 계산
>  •	외부환경에 따른 적정 온도계산

> Phase02 : LSTM 모델을 통한 시스템 내 상태 변수를 통한 CPU, Battery Prediction model만들기
>  •	적정 온도까지 떨어뜨리기 위한 효율성에 대한 평가기준의 필요성(COP평가)
>  •	어떻게 COP를 계산할 수 있는가
>  •	어떻게 예측 모델을 만들 것인가
>  •	데이터 분류    
>  •	데이터(data detail)  

>Keras LSTM 유형


> - 1. 단층-단방향 & many-to-one 유형

> - 2. 단층-단방향 & many-to-many 유형

> - 3. 단층-양방향 & many-to-one/many-to-many 유형

> - 4. 2층-단방향/양방향 & many-to-one 유형



-LSTM은 시간 순서에 따른 데이터에서 과거와 현재의 자기종속구조를 학습하여 이후 시퀀스를 예측한다.

### LSTM 구조



![구조](https://user-images.githubusercontent.com/90364187/150477541-7b8162c2-d298-42ee-8966-03a47d027351.png)



![계산](https://user-images.githubusercontent.com/90364187/150477727-ae0af9d1-4abe-4858-8c15-cac9b262772e.png)



- 모델 코드
model = keras.models.Sequential([
    keras.layers.LSTM(20, return_sequences=True, input_shape=[None, 1]),
    keras.layers.LSTM(20, return_sequences=True),
    keras.layers.TimeDistributed(keras.layers.Dense(10))
])


출처 : https://box-world.tistory.com/73

### GRU(Gated Recurrent Unit) : LSTM의 간소화된 버전.


![GRU](https://user-images.githubusercontent.com/90364187/150477562-daba0c69-076f-429e-a1e1-5a0b4761c8b5.png)



Sine 시계열의 경우는 과거의 패턴이 명확하기 때문에 어느 정도 먼 미래를 예측하는 것이 가능하다.

### Time-Series Forecasting

- Input Data는 타임 스텝마다 하나 이상의 값을 가지는 시퀀스

SCSm의 데이터는 다변량 시계열(multiivariate time series)이다. -> 여러 feature를 이용하므로.

### 해결 과정 가정

- Univariate : 하나의 특성을 사용, Multivariate : 여러개의 특성 사용.

#### 데이터를 살펴본다.
df = pd.read.csv(csv_path)
df.head()

1) 데이터 기록 시간 2) 데이터의 종류 및 개수

- history_size : 과거 information window의 크기입니다.(몇 개의 과거 데이터를 학습할 것인지)
- target_size : 예측해야하는 레이블입니다. 얼마나 멀리 있는 예측을 배워야 하는가.

def univariate_data(dataset, start_index, end_index, history_size, target_size):
	data = []
	labels = []

	start_index = start_index + history_size
	if end_index is None:
	 end_index = len(dataset) - target_size

	for i in range(start_index, end_index):
	 indices = range(i-history_size, i)
	 data.append(np.reshape(dataset[indice], (history_size,1)))
	 labels.append(dataset[i+target_size])
	return np.array(data), np.array(labels)


- 데이터의 처음 300,000개 행은 train dataset이고 나머지는  validation dataset입니다.
- 2100일 분량의 train data에 해당합니다.

#### 단일 특성(온도)만 사용하여 모델 학습하고, 향후 온도를 예측하는데 사용.

1) 데이터 세트에서 온도만 추출

- 시간에 따른 데이터 분석

#### 여러개의 특성을 지정, 조합하여 모델 학습

1) 고려할 특성을 선택

- 시간에 따른 각각의 데이터 분석

2)  Single step model

- 제공된 일부 데이터를 기반으로 미래의 단일 지점을 예측

3) Multi step model

- 과거 히스토리가 주어지면 미래의 값 범위를 예측
- 미래의 시퀀스를 예측

출처 : https://ahnjg.tistory.com/33




>  Phase03 : 외부환경을 고려한 최적의 타겟 내부 상태 변수 조합 필터링  
>  •	최적의 상태 변수 조합 실험

>  Phase04 : Reinforcement Learning으로 PID value 계산하기  
>  •	PID value caculation by LSTM algorithm


## 개발과정일정표
