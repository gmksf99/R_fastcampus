# 가설검정
### 가설을 검정(TEST)한다_ 두 집단의 평균 차이 검정

**1. 가설설정 - 귀무가설 / 대립가설**

* 귀무가설 : 기존에 존재하던 가설, 분석가의 주장과 반대 가설
* 대립가설 : 분석가가 새롭게 제시한 가설, 분석가의 주장

> 파랑색 집단 VS 노랑색 집단 : 수입 차이 분석
> - 귀무가설 : "두 집단 수입 차이가 없다,"
> - 대립가설 : "두 집단 수입 차이가 있다."(양측검정) OR "파랑 집단보다 노랑 집단 수입이 더 높다."(단측검정)
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/img3/000.PNG" width = "500px"/></h1>

* 데이터를 보고 가설을 설정하기 때문에 단측검정이 주로 사용

**1-1. 가설 검정 방법**

<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/img3/001.PNG" width = "500px"/></h1>

+) 대표본 : 데이터 개수 > 30 / 소표본 : 데이터 개수 < 30
+) 대응표본 / A집단, B집단이 같은 사람일때 Ex. 1학기때 점수, 2학기때 점수

**2. 검정통계량을 구한다.**
#### 기준>
1. 평균
2. 분산 : 편자 제곱의 평균
	* 편차 : 데이터값 - 평균
	* 식 : 편차 제곱의 합/n-1
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/img3/002.PNG" width = "500px"/></h1>

### **t-검정**
* T값 = 그룹1 평균 - 그룹2 평균/표준편차 = 평균 - 평균/분산
* 표준편차 = 루트(분산)
* 분산 동질성 여부
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/img3/003.PNG" width = "500px"/></h1>

> n1 : X집단 개수   Sp : 합동 표준 편차   S1제곱 : X분산
> n2 : Y집단 개수   Sp제곱 : 합동분산  S1제곱 : Y분산

**분산이 같을 경우**

 <h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/img3/004.PNG" width = "500px"/></h1>

<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/img3/005.PNG" width = "500px"/></h1>

**분산이 다를 경우**
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/img3/007.PNG" width = "500px"/></h1>

**t-검정 결론**
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/img3/006.PNG" width = "500px"/></h1>

3. 결론을 내린다(P-value)
* p-value
	* 귀무가설이 참이라고 했을 때, 표본데이타기 수집될 확룔
	* p-value가 낮을 수록, 대립가설 채택(=표본데이터 수집 획률이 낮다)
	* 통상적으로 p-value < 0.05 면 대립가설 채택
	* 0.05를 유의 수준이라하며, 주로 0.05/ 0.01을 많이 사용
