# :rose: 변수의 개념
### ◆ 변수(Variable) = 변하는 수

|  <center>소득</center> |  <center>성별</center> |  <center>학점</center> | <center>국적</center> |
|:--------|:--------:|--------:|--------:|
|1000만원| <center> 남자 </center> |3.8 |대한민국|
|2000만원| <center> 남자 </center> |4.2 |대한민국|
|3000만원| <center> 여자 </center> |2.6 |대한민국|
|5000만원| <center> 여자 </center> |4.5 |대한민국|

   **`데이터상 변수는 "소득, 성별, 학점"이다.`**
    
* 하나의 속성
* 다양한 값
* 분석의 대상
	* 남녀 중 누가 소득이 높은가?
	* 성별에 따라 학점이 다른가?
	* 학점이 증가할 수록 소득이 증가하는가?

# :sunflower: 함수의 개념
* 기능이 들어있다
* 변수를 넣으면 새로운 변수 탄생
* 분석 = 함수를 이용해서 변수를 조작하는 일

# :hibiscus: 패키지의 개념
* 패키지(packages) = 함수꾸러미
* CRAN 등록 패키지 15,556개
<br/>
	* 함수를 쓰려면 반드시 필요! <br/>
		* 패키지 설치 & 로드 <br/>
		* RStudio 실행할 때마다 패키지를 로드 <br/>
		* 내장 함수는 X
		<br/>
	* 필요에 따라 골라서 설치 <br/>
		* 필요한 기능에 따라 <br/>
		* 최신 분석 기법 수시로 업데이트 <br/>
		<br/>
	* ex) ggplot2 <br/>
		* 시각화 패키지
			
# :blossom: 데이터 프레임의 개념
* 가장 일반적인 데이터 형태
* 행(Row)과 열(Column)의 조합

|  <center>소득</center> |  <center>성별</center> |  <center>학점</center> | <center>국적</center> |
|:--------|:--------:|--------:|--------:|
|1000만원| <center> 남자 </center> |3.8 |대한민국|
|2000만원| <center> 남자 </center> |4.2 |대한민국|
|3000만원| <center> 여자 </center> |2.6 |대한민국|
`3개의 Row와 4개의 Column으로 이루어져있다.`
* 행(Row) = 한 사람의 데이터
	* 100명이면 100 행
	* 활용 예시) Row가 몇이에요? case가 몇 개에요?
		(행이 몇 개이지, 몇 명의 자료인지를 물어보는 것)
		<br/>
* 열(Column) = 변수
	* 변수가 100개면 100 열
	* 활용 예시) Column이 몇 개에요? 변수가 몇 개에요?
	   (열이 몇 개 인지 물어보는 것이다.)

### +) "데이터가 많다"
1. Row가 많다 -> 컴퓨터가 버벅 -> 고사양 장비 구축(upgrade)
2. Column이 많다 -> 분석방법의 한계 -> 고급 분석방법(machin learning)<br/>
`Row가 많은 것보다 Column이 많아지는거에 더 예민하게 된다.`

# 1. :bouquet: 변수, 함수 사용해보기
### **:bulb:변수** <br/>
`a <- 1` : 변수 a에 1 저장 <br/>
`b <- 2` : 변수 b에 2 저장 <br/>
* **연산** <br/>
	   `a+b` : 결과 3 <br/>
	   `5*b` : 결과 10
	   <br/>
* **변수에 연속값 저장**<br/>
`c <- c(1,2,3,4,5)` <br/>
`d <- c(1:5)` <br/>
`e <- seq(1,5)` <br/>
모두 변수에 1, 2, 3, 4, 5가 저장된다. <br/>
`f <- seq(1,10, by=2)` : 1~10까지 2씩 증가 <br/>
	* 연산 <br/>
	   `c+2` : 결과 3, 4, 5, 6, 7 <br/>
	   `c+d` : 결과 2, 4, 6, 8, 10	
	   <br/>
* **변수에 문자 저장** <br/>
`a2 <- "a"`  : 변수 a2에 "a"를 저장 <br/>
`b2 <- "Hello world!"`  # 문자 및 특수기호를 저장 <br/>
`c2 <- c("Hello!","world","is","good!")` # 연속된 문자를 저장 <br/>
 > **사칙연산은 숫자값에만 적용가능!!**  
### **:bulb:함수** <br/>
* `a <- c(1,2,3)`
		`mean(a)` : 결과 2 <br/>
		`max(a)` : 결과 3  <br/>
		`min(a)` : 결과 1 <br/>
	* `b <- c("a", "a", "b", "c")`
	   `qplot(b)` # 빈도그래프 
	   <h1 align="center">
	  <img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/101.PNG" width = "500px"/></h1><br/>
	*  collapse : 구분자로 구분하고 문자를 붙여준다.
	* `c2 <- c("Hello!","world","is","good!")` <br/> 
	`paste(c2, collapse = " ")` :  "Hello! world is good!" <br/>
	`c2_paste <- paste(e2, collapse = " ")` :  위 값을 변수 c2_paste에 저장

# 2. :bouquet: 패키지, 데이터 프레임 사용해보기
### **:bulb:패키지**
`qplot(data = mpg, x = hwy)` # x는 x축을 의미
 <h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/102.PNG" width = "500px"/></h1><br/>

`qplot(data = mpg, x = cty)`
 <h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/103.PNG" width = "500px"/></h1><br/>

`qplot(data = mpg, y = hwy, x = drv, geom = "point")` # geom : 그래프모양 결정
 <h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/104.PNG" width = "500px"/></h1><br/>

`qplot(data = mpg, y = hwy, x = drv, geom = "boxplot")`

 <h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/105.PNG" width = "500px"/></h1><br/>

`qplot(data = mpg, y = hwy, x = drv, geom = "boxplot", colour = drv)` #colour : 변수별로 색 구별

 <h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/106.PNG" width = "500px"/></h1><br/>

`?qplot` : 함수 설명 <br/>
>**+) 함수 설명 속에 있는 코드들**  <br/>
> qplot(mpg, wt, data = mtcars) <br/>
qplot(mpg, wt, data = mtcars, colour = cyl) <br/>
qplot(mpg, wt, data = mtcars, size = cyl) <br/>
qplot(mpg, wt, data = mtcars, facets = vs ~ am)

### **:bulb:데이터 프레임** <br/>
`history <- c(90, 80, 60, 70)` # 역사점수 생성 <br/>
`math <- c(50,60,100,20)` # 수학점수 생성 <br/>
`df_midterm <- data.frame(history,math)` # 데이터프레임 생성 <br/>
|  | history | math |
|--|---------|------|
| 1 | 90 | 50 |
| 2 | 80 | 60 |
| 3 | 60 | 100 |
| 4 | 70 | 20 |

**+ 학년까지 추가 된다면** <br/>
`class <- c(1,1,2,2)` <br/>
`df_midterm <- data.frame(history,math,class)` <br/>
|  | history | math | class |
|--|---------|------|------|
| 1 | 90 | 50 | 1 |
| 2 | 80 | 60 | 1 |
| 3 | 60 | 100 | 2 |
| 4 | 70 | 20 | 2 |
* 역사점수 평균
`mean(df_midterm$history)` : 결과 75
* 수학점수 평균
`mean(df_midterm$math)` : 결과 57.5
>(복습) $ : 데이터 중 특정 변수를 선택할때 사용
