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


- 데이터 예시
![image](https://user-images.githubusercontent.com/90364187/150448554-8f1f47cb-83b1-45a9-a906-a808da03bb2e.png)


## 개발과정계획
> Phase01 : 다양한 환경에서 시스템 운영의 허용 온도 구간 계산
>  •	외부환경에 따른 적정 온도계산

> Phase02 : LSTM 모델을 통한 시스템 내 상태 변수를 통한 CPU, Battery Prediction model만들기
>  •	적정 온도까지 떨어뜨리기 위한 효율성에 대한 평가기준의 필요성(COP평가)
>  •	어떻게 COP를 계산할 수 있는가
>  •	어떻게 예측 모델을 만들 것인가
>  •	데이터 분류    
>  •	데이터(data detail)  

>  Phase03 : 외부환경을 고려한 최적의 타겟 내부 상태 변수 조합 필터링  
>  •	최적의 상태 변수 조합 실험

>  Phase04 : Reinforcement Learning으로 PID value 계산하기  
>  •	PID value caculation by LSTM algorithm


## 개발과정일정표
