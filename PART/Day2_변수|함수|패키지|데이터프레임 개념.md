# :fire:R Studio 익히기
* 패키지 설치
`install.packages("dplyr")`
`install.packages("ggplot2")`
* 패키지 로드
`library(dplyr)`
`library(ggplot2)`
* 데이터 검토
	* mpg : ggplot2 패키지에 포함되어 있는 예제 데이터로 자동차의 연비,구동방식 등을 조사한 데이터

	`head(mpg)`  : 데이터 앞부분을 보여준다.
	<h1 align="center">
	  <img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/002.PNG" width = "500px"/></h1><br/>
	  
	`str(mpg)`  : 변수들의 속성을 보여준다
	<h1 align="center">
  <img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/003.PNG" width = "500px"/></h1><br/>
  
  `summary(mpg)` : 요약 통계량을 보여준다.(최소, 1분위수(하위 25%) , 중앙값, 평균,  3분위수(상위25%), 최대)
  <h1 align="center">
  <img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/004.PNG" width = "500px"/></h1><br/>
  
  `View(mpg)` :  데이터가 있는 창을 보여준다.
   <h1 align="center">
  <img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/009.PNG" width = "500px"/></h1><br/>

# :smile:mpg 데이터를 활용한 문제
* Q1.회사별 평균 연비 높은순 정렬
 `mpg %>%`
  `group_by(manufacturer) %>%  # 제조사별로 데이터를 나누어라`
  `summarise(mean.hwy=mean(hwy)) %>%  # hwy를 회사별로 평균을 구해 요약해라`
  `arrange(desc(mean.hwy)) # 내림차순으로 정렬해라`
<h1 align="center">
  <img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/005.PNG" width = "400px"/></h1><br/>
  
* Q2. 포드(ford) 연비 높은순 정렬
`mpg %>%`
 `filter(manufacturer=="ford") %>%`
  `group_by(model) %>%`
  `arrange(desc(hwy))`
  <h1 align="center">
  <img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/006.PNG" width = "500px"/></h1><br/>
  
* Q3-1. 배기량이 연비에 미치는 영향_회귀분석
  `lm.mpg <- lm(data = mpg, hwy ~ displ) # 회귀분석`
  `summary(lm.mpg) # 결과출력`
  <h1 align="center">
  <img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/007.PNG" width = "500px"/></h1><br/>
  
* Q3-2. 그래프 만들기 
 `qplot(data=mpg, x=displ, y=hwy)`
 <h1 align="center">
  <img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/008.PNG" width = "500px"/></h1><br/>

### +추가) $ 는 "여러 변수중 어떤 것을 사용하겠다" 라는 의미이다.
* mean(mpg$hwy)
	* [1] 고속도로 연비 평균 : 23.44017
* max(mpg$hwy)
	* [1] 고속도로 연비 최대값 : 44
* min(mpg$hwy)
	* [1] 고속도로 연비 최소값 : 12
* hist(mpg$hwy)
	* 히스토그램_ [25~30]에 해당하는 자동차가 많다.
	<h1 align="center">
  <img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/010.PNG" width = "500px"/></h1><br/>
