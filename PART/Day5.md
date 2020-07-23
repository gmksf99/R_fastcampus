# :ocean: R로 만들 수 있는 그래프
* 2차원 그래프, 3차원 그래프
* 지도 그래프
* 네트워크 그래프
* 모션 차트
* 인터랙티브 그래프

# :fish: 가장 많이 사용하는 그래프
### ggplot() vs qplot()
* qplot() : 전처리 단계 데이터 확인용 문법 간단, 기능 단순
* qqplot() : 최종 보고용 색, 크기, 폰트 등 세부 조작 가능
> qplot은 간단하게 확인할때 qqplot은 본격적으로 확인할때
 
### ggplot2패키지
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/500.PNG" width = "500px"/><br/>

* **산점도(Scater Plot)**
	* 데이터를 x축과 y축에 점으로 표현한 그래프
	* 두 변수 간 관계 표현할때 사용
	> 배경 생성 : `ggplot(data = mpg, aes(x = displ, y = hwy))`
	<h1 align="center">
	<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/501.PNG" width = "500px"/></h1><br/>
	
	> "**geom**" 으로 그래프 모양을 설정한다.
	> 산점도 추가 : `ggplot(data = mpg, aes(x = displ, y = hwy)) + geom_point()`
	<h1 align="center">
	<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/502.PNG" width = "500px"/></h1><br/>

	> x축, y축 범위 제한 : `ggplot(data=mpg, aes(x=displ, y= hwy))+geom_point()+xlim(3,6)+ylim(10,30)`\
	<h1 align="center">
	<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/503.PNG" width = "500px"/></h1><br/>
	
* **막대 그래프(Bar Chart)**
	* 데이터의 크기를 막대의 길이로 표현한 그래프
	* 집단 간 차이를 표현할 때 주로 사용
	
	> **<평균 막대 그래프>**
	> 데이터 생성 : `df_mpg <- mpg %>% group_by(drv) %>% summarise(mean_hwy = mean(hwy))`
	> 막대 그래프 생성 : `ggplot(data = df_mpg, aes(x = drv, y = mean_hwy)) + geom_col()`\
	> Defult : 알파벳순
	<h1 align="center">
	<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/505.PNG" width = "500px"/></h1><br/>
	
	> mean_hwy기준으로 내림차순(-) : `ggplot(data = df_mpg, aes(x = reorder(drv, -mean_hwy), y = mean_hwy)) + geom_col()`
	<h1 align="center">
	<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/506.PNG" width = "500px"/></h1><br/>

	> **<빈도 막대 그래프>**
	> x축 범주 변수, y축 빈도 : `ggplot(data = mpg, aes(x = drv)) + geom_bar()`
	<h1 align="center">
	<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/507.PNG" width = "500px"/></h1><br/>

	> 

* **선 그래프(Line Chart)**
	* 데이터를 선으로 표현한 그래프
	* 시계열 그래프(Time Series Chart) 
		* 일정 시간 간격을 두고 나열된 시계열 데이터(Time Series Data)를 선으로 표현한 그래프. 환율, 주가지수 등 경제 지표가 시간에 따라 어떻게 변하는지 표현할 때 활용
	
	> `ggplot(data = economics, aes(x = date, y = unemploy)) + geom_line()`
	<h1 align="center">
	<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/509.PNG" width = "500px"/></h1><br/>
	
	> **해석** 
	> * 실업자 수가 70년대부터 점점 등락을 반복하면서 증가하다가 2008~2009년에 급격히 증가했다가 지금은 떨어지는 경향이 있다 

* **상자 그림(Box Plot)** 
	* 데이터의 분포(퍼져 있는 형태)를 직사각형 상자 모양으로 표현한 그래프
	* 분포를 알 수 있기 때문에 평균만 볼 때보다 데이터의 특성을 좀 더 자세히 이해할 수 있음
	> `ggplot(data = mpg, aes(x = drv, y = hwy)) + geom_boxplot()`
	<h1 align="center">
	<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/510.PNG" width = "500px"/></h1><br/>

	> **해석**  
	> * **r구동**에서 상자 속 가로선은 중앙값, 상자 아래는 하위25%, 위는 상위 25%, 세로 선 맨 위는 최대, 맨 아래는 최소	
	> 	* 상자의 폭이 넒으므로 다양한 고속도로 연비가 있다	

	> * **f구동**에서 점은 극단치이다. 1분위 수  + 1분위 수에 1.5를 곱한다(1.5IQR)  한 값보다 밖에 있을때 점으로 나타낸다. (위쪽 부분도 같다.)
	> 	* 상자의 폭이 좁으므로 상대적으로 비슷한 고속도로 연비가 있다.	
	
# :fire:연습문제 1
### 산점도
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/504.PNG" width = "700px"/></h1><br/>

* A1
	* `ggplot(data = mpg, aes(x = cty, y = hwy)) + geom_point()`
* A2
	* `ggplot(data = midwest, aes(x = poptotal, y = popasian)) + geom_point() + xlim(0,500000) + ylim(0,10000)`
 
### 막대
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/508.PNG" width = "700px"/></h1><br/>

* A1
	* `suv_mpg <- mpg %>% `<br/>
	  `filter(class == "suv") %>% `<br/>
	  `group_by(manufacturer) %>%` #제조사별로<br/>
	  `summarise(mean_cty = mean(cty)) %>%` # cty 평균을 구하고<br/>
	  `arrange(desc(mean_cty)) %>%` # 내림차순 정렬<br/>
	  `head(5)`
  
	* `ggplot(data = suv_mpg, aes(x = reorder(manufacturer, -mean_cty), y = mean_cty)) + geom_col()`

* A2
	* `ggplot(data = mpg, aes(x = class)) + geom_bar()`

### 선
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/516.PNG" width = "700px"/></h1><br/>

* A1
	* `ggplot(data = economics, aes(x = date, y = psavert)) + geom_line()`

### 박스 플롯 
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/512.PNG" width = "700px"/></h1><br/>

* A1
	* `css_mpg <- mpg %>% filter(class %in% c("compact", "subcompact", "suv"))`
	* `ggplot(data = css_mpg, aes(x = class, y = cty)) + geom_boxplot()`
		* 주의> summarise 하면 안된다!!
		
# :mortar_board: 그래프관련 참고
• 10만 단위가 넘는 숫자는 지수 표기법(Exponential Notation)에 따라 표현됨<br/>
• 1e+05 = 10만(1 × 10의 5승) <br/>
• 정수로 표현하기 : options(scipen = 99) 실행 후 그래프 생성 <br/>
• 지수로 표현하기 : options(scipen = 0) 실행 후 그래프 생성 <br/>
• R 스튜디오 재실행시 옵션 원상 복구됨
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/511.PNG" width = "500px"/></h1><br/>

* 1.5 IQR: 사분위 범위(Q1~Q3간 거리)의 1.5배

# :sparkler: 그래프 정제
## 1. 결측치 정제


*  결측치(Missing Value) 
	*  누락된 값, 비어있는 값 
	* 함수 적용 불가, 분석 결과 왜곡 
	* 제거 후 분석 실시
	
* 결측치 표기 - NA (겹따옴표 X)
`df <- data.frame(sex = c("M", "F", NA, "M", "F"), score = c(5, 4, 3, 4, NA))` 
	* `is.na(df)` : 결측치 확인	
	* `table(is.na(df))` : 결측치 빈도 출력

* 변수별로 결측치 측정
	* `table(is.na(df$sex))`
	* `table(is.na(df$score))`
* 결측치가 있으면 NA를 반환
	* `mean(df$sex)`
	* `sum(df$score)` 
		* 둘다 NA를 반환
* 결측치 있는 행 제거 _ filter
	* `df %>% filter(is.na(score))` :결측치 있는 행 출력
	* `df %>% filter(!is.na(score))` : score 결측치 제거
		* 제거된 데이터를 저장해줘야한다.
	* 변수가 2개 이상인 경우 결측치 제거
		* `df_nomiss <- df %>% filter(!is.na(score) & !is.na(sex)) `
		* 	단점 : 변수가 많을때 쓰기 힘들다
* 모든 변수 결측치 제거
	1. na.omit()
	* `df_nomiss2 <- na.omit(df)` : 모든 변수 결측치 제거
	* 단점 : 분석에 필요한 데이터까지 손실시킬 수 있기때문에 잘 쓰지 않는다.
	2. na.rm = T
	* `sum(df$score, na.rm = T)` : 결측치 제외하고 합계 산출
	* `mean(df$score, na.rm = T)` : 결측치 제외하고 평균 산출
	
#### 데이터에 값 할당 후 평균, 결측치 제외 평균 구하기
* `exam[c(3,8,15),"math"]` <- NA 
		*  3, 8, 15행의 math에 NA 할당_ 요즘은 안쓰는 문법
		*  [ 행조건 , 열조건 ]
* 평균 구하기
	* `exam %>% summarise(mean_math = mean(math))`
* 결측치 제외하고 평균 구하기
	*  `exam %>% summarise(mean_math  = mean(math, na.rm = T))`

### 1-2. 결측치 대체
* 결측치 많을 경우 모두 제외하면 데이터 손실이 크다
* 대안 : 다른 값 채워넣기
##### 결측치 대체법(imputation)
* 대표값(평균, 최빈값, 등)으로 일괄 대체
* 통계분석 기법 적용, 예측값 추정해서 대체
* `exam$math <- ifelse(is.na(exam$math),55, exam$math)` : math가 NA면 55로 대체

## 2. 이상치 정제
* 이상치(Outlier) : 정상범주에서 크게 벗어난 값 
	* 이상치 포함시 분석 결과 왜곡 
	* 결측 처리 후 제외하고 분석
	<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/517.PNG" width = "500px"/>

### 존재할 수 없는 값 제거
* 예시) 성별은 1, 2로 점수는 5점 만점
	* `outlier <- data.frame(sex = c(1,2,1,3,2,1), score = c(5,4,3,4,2,6))` : sex 3,score 6 이상치
* 빈도로 이상치를 찾음
	* `table(outlier$sex)`
	* `table(outlier$score)`
* 이상치를 NA로 변환
	* `outlier$sex <- ifelse(outlier$sex == 3, NA, outlier$sex)`
	* `outlier$score <- ifelse(outlier$score == 6, NA, outlier$score)`
* 결측치 제외 후 분석
	* `outlier %>% filter(!is.na(sex) & !is.na(score)) %>% group_by(sex) %>% summarise(mean_score = mean(score))` : NA값을 제외하고 성별로 평균 점수를 구해라

### 극단적인 값
* 정상범위 기준을 정해서 벗어나면 결측 처리한다.
* 기준 정할 때 제일 많이 사용하는 방법 : 표준편차, 상자그림(boxplot)
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/518.PNG" width = "500px"/> 

* 예시) 상자 그림으로 극단치 기준 정하기
	* `boxplot(mpg$hwy)`
	
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/521.PNG" width = "500px"/><br/>

* `boxplot(mpg$hwy)$stats` : 통계치 출력

<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/522.PNG" width = "200px"/><br/>

* 해석>
	* 밑의 경계 : 12
	* 상자 밑면(1분위 수) : 18
	* 중앙값 : 24
	* 상자 윗면(3분위 수) : 27
	* 윗쪽 경계 : 37
* 결측치 처리
	* `mpg$hwy <- ifelse(mpg$hwy < 12 | mpg$hwy > 37, NA, mpg$hwy)` : 12미만 37초과면 NA 할당, 그외는 원래값 할당
	* `table(is.na(mpg$hwy))` : NA 개수 확인
* 결측치 제외 후 분석
	* `mpg %>% group_by(drv) %>% summarise(mean_hwy =mean(hwy, na.rm = T))`

# :fire:연습문제 2
### 결측치
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/514.PNG" width = "700px"/></h1><br/>
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/515.PNG" width = "700px"/></h1><br/>

* A1
	* `table(is.na(mpg$drv))` : 0개
	* `table(is.na(mpg$hwy))` : 5개
* A2
	* `mpg %>% filter(!is.na(hwy)) %>% group_by(drv) %>% summarise(mean_hwy = mean(hwy)) %>% arrange(desc(mean_hwy))` : 결측치를 제외하고 drv별로 분리해서 hwy 평균을 구하고 내림차순으로 정렬
	
### 이상치
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/523.PNG" width = "700px"/></h1><br/>
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/524.PNG" width = "700px"/></h1><br/>

* A1
	* `table(mpg$drv)` : 이상치 "k" 확인
	* `mpg$drv <- ifelse(mpg$drv %in% c("4","f","r"), mpg$drv, NA)` : "4", "f", "r" 외에 값에 NA를 할당
	* `table(mpg$drv)` : 이상치가 사라짐
* A2
	* `boxplot(mpg$cty)$stats` : 상자 그림 생성 및 통계치 출력
	* `mpg$cty <- ifelse(mpg$cty < 9 | mpg$cty > 26, NA,mpg$cty)` : 9~26 벗어나면 NA할당
	* `boxplot(mpg$cty)` : 이상치가 사라진 상자 그림
* A3
	* `mpg %>% filter(!is.na(drv) & !is.na(cty)) %>% group_by(drv) %>% summarise(mean_cty =mean(cty))` : drv, cty에사 NA값을 제외하고 drv별로 cty평균 구하기

