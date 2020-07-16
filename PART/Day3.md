# :triangular_flag_on_post:데이터 준비
프로젝트 파일에 데이터 파일을 넣어논다.
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/300.PNG" width = "500px"/></h1><br/>

* 외부 데이터 불러오기
> Working directory에 불러올 파일이 있어야됨

`install.packages("readxl")` : readxl 패키지 설치<br/>
`library(readxl)` : readxl 패키지 로드<br/>
`df_finalexam <- read_excel("finalexam.xlsx", sheet = 1, col_names = T)` : 데이터를 불러와 변수에 저장하기<br/>
`read_excel("finalexam.xlsx", sheet = 1, col_names = T)` : 데이터 읽어오기<br/>
sheet = 1 : 시트 1번을 / col_names = T : 칼럼  이름을 가져오겠다
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/301.PNG" width = "500px"/>
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/301-2.PNG" width = "500px"/>
</h1><br/>

* CSV 파일 불러오기
	* 범용 데이터 형식
	* 값 사이를 쉼표(,)로 구분
	* 용량이 작고 다양한 소프트웨어에서 사용 

`read.csv("csv_exam.csv", header = T)` : csv데이터 값을 불러온다
header = T : 액셀때와 마찬가지로 칼럼을 가져온다는 의미
`write.csv(df_finalexam, file = "output_newdata.csv")` : df_finalexam 데이터를 "output_newdata"라는 이름으로 csv파일 생성

# :heavy_check_mark:데이터 파악
`exam <- read.csv("csv_exam.csv")` : exam 변수에 데이터를 저장
(Working directory에 불러올 파일이 있어야됨)

* 데이터 파악하는 방법
	* `head(exam)` : 첫 행부터 6행까지 출력
		* head(exam, 10) : 첫 행부터 10행까지 출력
	* `tail(exam)` : 뒷 행부터 6행까지 출력
		* tail(exam) : 뒷 행부터 10행까지 출력
	*`View(exam)` : 뷰어창에서 데이터 확인 
	* `dim(exam)` : 행, 열을 출력
	* `str(exam)` : 데이터 속성 출력
	* `summary(exam)` : 요약통계량 출력
	<br/>
* 데이터 변환
	* `mpg <- as.data.frame(ggplot2::mpg)` : ggplot2의 mpg를 데이터 프레임 형태로 불러와 mpg변수에 저장
	<br/>
# :recycle:데이터 변수명 바꾸기
* `df_raw <- data.frame(var1 = c(1,2,1), var2 = c(2,3,2))` : 변수를 생성하고 값을 입력해 데이터 프레임 생성
* `df_new <- df_raw` : 백업을 위해 복사본을 생성
* `df_new <- rename(df_new, v2 = var2)` : 변수 var2를 v2로 수정
> **주의 : 새로운 변수명 = 기존 변수명**

# :trident:파생 변수 만들기
파생변수 : 기존에 있는 변수들을 응용해서 만들어진 변수
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/303.PNG" width = "500px"/></h1><br/>

### 직접 해보기
`df <- data.frame(var1 = c(4,3,8), var2 = c(2,6,1))`

|  | var1 | var2 |
|--|--|--|
|  | 4 | 2 |
|  | 3 | 6 |
|  | 8 | 1 |

`df$var_sum <- df$var1 + df$var2` : var1 + var2 한 var_sum 파생변수 생성
`df$var_mean <- (df$var1 + df$var2)/2` : vat_mean 파생변수 생성
> **주의 : 데이터 프레임$변수**

| | var1 | var2 | var_sum | var_mean |
|--|-----|------|---------|----------|
|  | 4 | 2 | 6 | 3.0 |
|  | 3 | 6 | 9 | 4.5 |
|  | 8 | 1 | 9 | 4.5 |

# :100:파생변수를 이용해 mpg데이터 분석
* 통합 연비 변수(total) 생성
`mpg$total <- (mpg$cty + mpg$hwy)/2` 
* 기준값 정하기
`summary(mpg$total)` 
`hist(mpg$total)`
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/304.PNG" width = "500px"/></h1><br/>

* 조건물으로 합격 판정 변수(test) 생성
`mpg$test <- ifelse(mpg$total >= 20, "pass", "fail")` : 20보다 크거나 같으면 pass 아니면 fail
* 빈도표로 합격 판정 자동차 수 보기
`table(mpg$test)` : pass, fail 숫자만 출력
`qplot(mpg$test)` : 막대 그래프 생성
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/305.PNG" width = "500px"/></h1><br/>

* 중첩 조건문 활용 ex. 연비 등급 변수 생성
`mpg$grade <- ifelse(mpg$total >= 30, "A", ifelse(mpg$total >= 20, "B", "C"))` : A, B둘다 해당되지 않으면 C

# :fire:지금까지 배운 내용으로 복습!!
### 1
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/302.PNG" width = "500px"/></h1><br/>

* A1 
`mpg <- as.data.frame(ggplot2::mpg)` 
`mpg_new <- mpg # 복사본 생성`
* A2
`library(dplyr) #이 패키지가 있어야 가능`
`mpg_new <- rename(mpg_new, city = cty, highway = hwy)`
* A3
`head(mpg_new)`

### 2
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/307.PNG" width = "500px"/></h1><br/>

* A1
`midwest <- as.data.frame(ggplot2::midwest)`
* A2
`midwest <- rename(midwest, total = poptotal, asian = popasian)`
* A3
`midwest$per_asian <- (midwest$asian/midwest$total)*100`
`hist(midwest$per_asian)`
* A4
`mean(midwest$per_asian)`
`midwest$percent_test <- ifelse(midwest$per_asian >= 0.4872462, "large", "small")`
* A5
`table(midwest$percent_test)`
`qplot(midwest$percent_test)`
