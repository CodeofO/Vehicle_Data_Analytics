# 🏭 자동차 생산 공정 데이터 분석을 통한 생산성 개선 방안 도출
      
|구분|설명|
|------|---|
|프로젝트 명|자동차 생산 공정 데이터 분석을 통한 생산성 개선 방안 도출|
|제안 배경|공정 데이터 분석 기반 생산성 개선 방안을 찾기 위해 제안되었습니다.|
|기간|2023.11 ~ 2023.12|
|주최|전공 프로젝트|
|요약|target이 주어지지 않은 bottom-up 형식의 과제입니다.<br>다양한 변수간의 관계, 특징 등을 시각화해서 발견하고 가설을 수립했습니다.<br>수립한 가설은 통계적 검정을 통해 검정했고 최종 방안을 제안했습니다.|
|역할|리더/ 프로젝트 일정 수립/ EDA/ 가설검정|


## 1. EDA, 가설수립
생산수량 변수에 대한 시각화 2개, 불량률 1개, 시간가동률 1개를 확인했습니다.
### 1) 생산수량

**[ 생산수량-1 : 아반떼의 생산수량의 분산이 타 모델들에 비해 높을 것이다. ]**
![image](https://github.com/CodeofO/v/assets/99871109/083c8119-7e06-44b2-93b5-ada1d96a49da)
![image](https://github.com/CodeofO/v/assets/99871109/bd5e6a18-664f-4df4-8c76-54161a19547c)
<br>
👉 아반떼 모델의 생산수량이 넓게 퍼져있는 것을 확인할 수 있다.
<br>
<br>
**[ 생산수량-2 : LINE_A에서 22년 4월 29일~22년 8월 1일 사이에 평균 생산수량이 다른 날에 비해 높을 것이다.  ]**
![image](https://github.com/CodeofO/v/assets/99871109/ea7d339a-1539-4678-8ee4-1e4ebf58f40d)
![image](https://github.com/CodeofO/v/assets/99871109/87fa13ec-dcb7-4451-9fe7-11d781efeee6)
<br>
👉 LINE_A에서 22년 4월 29일~22년 8월 1일 사이 평균 생산수량이 다른 날에 비해 높은 것을 확인할 수 있다. 


<br>
<br>
<br>

### 2) 불량률
**[ 불량률-1 : 근속년수가 00-04년, 25년 이상인 경우 평균 불량률이 다른 년수에 비해 높을 것이다. ]** 
![image](https://github.com/CodeofO/v/assets/99871109/6a691b32-1d86-4c6d-9f22-03cb6ee0c334)
![image](https://github.com/CodeofO/v/assets/99871109/4b6c1fb9-edfc-4386-ba22-8627f4dee392)
<br>
👉 근속년수가 낮거나, 높을수록 불량률이 높은 것을 확인할 수 있다.
<br>
<br>
<br>

### 3) 시간가동률
**[ 시간가동률-1 : LINE_C에서 생산수량이 375개 이상일때 시간가동률이 높을 것이다. ]**
![image](https://github.com/CodeofO/v/assets/99871109/61ba0093-ce07-4d2b-a1c5-64b753b0ec2d)
<br>
👉 생산수량이 375개 아래로 떨어지면 시간가동률이 현저히 낮아지는 것을 확인할 수 있다. 
(시간가동률 = 가동시간 / 부하시간)
<br>
<br>

**가설** 🔻
| <font size="4">**가설 번호**</font> | <font size="4">**가설 설명**</font> | <font size="4">**도표**</font> |
| ----------------------------------- | ----------------------- | ----------------------- |
| <font size="4">생산수량-1</font> |  <font size="4">아반떼의 생산수량의 분산이 타 모델들에 비해 높을 것이다.</font> | <font size="4">EDA - 생산수량, 모델</font> |
| <font size="4">생산수량-2</font> |  <font size="4">LINE_A에서 22년 4월 29일~22년 8월 1일 사이에 평균 생산수량이 다른 날에 비해 높을 것이다.</font> | <font size="4">EDA - 생산수량, 4월 29일 ~ 8월 1일, 설비(LINE_A)</font> |
| <font size="4">불량률-1</font> |<font size="4">근속년수가 00-04년, 25년 이상인 경우 평균 불량률이 다른 년수에 비해 높을 것이다.</font> | <font size="4">EDA - 불량률, 근속년수</font> |
| <font size="4">시간가동률-1</font> | <font size="4">LINE_C에서 생산수량이 375개 이상일때 시간가동률이 높을 것이다.</font> | <font size="4">EDA - 시간가동률, 설비(LINE_C)</font> |

<br>
<br>
<br>

## 2. 가설 검정
**[ 생산수량-1 : 아반떼의 생산수량의 분산이 타 모델들에 비해 높을 것이다. ]** <br>
1. levene의 등분산검정 : 모델 2개씩 비교 <br>
      $H_0$ : $s_{생산수량, 아반떼}^2 = s_{생산수량, model}^2$  for some $models$ <br>
      $H_1$ : $s_{생산수량, 아반떼}^2 > s_{생산수량, model}^2$ for some $models$ <br>

      |모델명|p-value|결과||
      |--|--|--|--|
      |아반떼 / 니로|0.05424536|귀무가설 채택|아반떼의 생산수량 분산이 니로의 분산과 유의미한 차이가 없다.|
      |아반떼 / 소나타|3.786e-06|아반떼의 생산수량 분산이 소나타의 분산보다 크다.|
      |아반떼 / 아이오닉|0.0|귀무가설 채택|아반떼의 생산수량 분산이 아이오닉의 분산보다 크다.|
      |아반떼 / 투싼|0.0|귀무가설 채택|아반떼의 생산수량 분산이 투싼의 분산보다 크다.|
      |아반떼 / 플러그인 투싼|0.0|아반떼의 생산수량 분산이 플러그인투싼의 분산보다 크다.|
<br>

2. levene의 등분산검정 : 모든 모델 비교 <br>
  $H_0$ : $s_{생산수량, 아반떼}^2 = s_{생산수량, model}^2$  for some $models$ <br>
  $H_1$ : $s_{생산수량, 아반떼}^2 \neq s_{생산수량, model}^2$ for some $models$ <br>
  
  기각역 : 0.05  
  W-statistic: 58.7177
  P-value: 0.0000
  
✅ 결론 : 대립가설 일부 채택
* 아반떼의 생산수량 분산이 니로를 제외한 다른 모델들의 분산보다 크다.
* 전체를 한 번에 검정했을 때는 모델별 분산에 차이가 있다는 결과
<br>
<br>

**[ 생산수량-2 : LINE_A에서 22년 4월 29일~22년 8월 1일 사이에 평균 생산수량이 다른 날에 비해 높을 것이다.  ]** <br>
독립표본 t 검정 (단측)

$H_0$ : $\mu_{생산수량, 22.04.29 ~ 22.08.01} = \mu_{생산수량, 그\ 외\ 일자}$ <br>
$H_1$ : $\mu_{생산수량, 22.04.29 ~ 22.08.01} > \mu_{생산수량, 그\ 외\ 일자}$ <br>

<< 22/04/29~22/08/01 / 다른 날 >>
기각역 : 0.05
P-value: 0.0

✅ 결론 : 대립가설 채택
22/04/29~22/08/01때 LINE_A에서의 생산수량 평균이 다른 날의 평균보다 크다.
<br>
<br>

**[ 불량률-1 : 근속년수가 00-04년, 25년 이상인 경우 평균 불량률이 다른 년수에 비해 높을 것이다. ]** <br>

1. 근속년수 : 00-04년 <br>
    $H_0 : \mu_{불량률, 00-04년} = \mu_{불량률, bined\_\ 근속년수}$  for some 근속년수(25년 이상 제외) <br>
    $H_1$ : $\mu_{불량률, 00-04년} > \mu_{불량률, bined\_\ 근속년수}$  for some 근속년수(25년 이상 제외) <br>
 
|근속년수|p-value|결과||
|--|--|--|--|
|00-04년 / 05-09년|0.0|대립가설 채택|00-04년의 불량률 평균이 05-09년의 평균보다 크다|
|00-04년 / 10-14년|0.0|대립가설 채택|00-04년의 불량률 평균이 10-14년의 평균보다 크다|
|00-04년 / 15-19년|0.0|대립가설 채택|00-04년의 불량률 평균이 15-19년의 평균보다 크다|
|00-04년 / 20-24년|0.0|대립가설 채택|00-04년의 불량률 평균이 20-24년의 평균보다 크다|
<br>
 
2. 근속년수 : 25년 이상 <br>
    $H_0$ : $\mu_{불량률, 25년 이상} = \mu_{불량률, bined\_\ 근속년수}$  for some 근속년수(00-04년 제외) <br>
    $H_1$ : $\mu_{불량률, 25년 이상} > \mu_{불량률, bined\_\ 근속년수}$  for some 근속년수(00-04년 제외) <br>

|근속년수|p-value|결과||
|--|--|--|--|
|25 년 이상 / 05-09년|0.0|대립가설 채택|25 년 이상의 불량률 평균이 05-09년의 평균보다 크다.|
|25 년 이상 / 10-14년|0.0|대립가설 채택|25 년 이상의 불량률 평균이 10-14년의 평균보다 크다.|
|25 년 이상 / 15-19년|0.0|대립가설 채택|25 년 이상의 불량률 평균이 15-19년의 평균보다 크다.|
|25 년 이상 / 20-24년|0.0|대립가설 채택|25 년 이상의 불량률 평균이 20-24년의 평균보다 크다.|
<br>

3. ANOVA : 모든 구간화된 근속년수를 비교
      $H_0$ : $\mu_{불량률, 근속년수} = \mu_{불량률, 근속년수}$  for some $구간화\ 된\ 근속년수$ <br>
      $H_1$ : $\mu_{불량률, 근속년수} \neq \mu_{불량률, 근속년수}$ for some $구간화\ 된\ 근속년수$ <br>

      기각역 : 0.05
      F-statistic: 1385.8033
      P-value: 0.0000

   
<br>
<br>

**[ 시간가동률-1 : LINE_C에서 생산수량이 375개 이상일때 시간가동률이 높을 것이다. ]** <br>
1. 독립표본 t 검정(단측)**  
$H_0 : \mu_{시간가동률, 생산수량\ 375개\ 이상} = \mu_{시간가동률, 생산수량 \ 375개\ 이하}$ <br>
$H_1$ : $\mu_{시간가동률, 생산수량\ 375개\ 미만} > \mu_{시간가동률, 생산수량 \ 375개\ 이하}$ <br>



## 3. 활용방안
