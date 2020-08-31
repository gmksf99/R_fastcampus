# 한국복지패널 데이터 분석:wind_chime:
### 한국복지패널에는 변수가 1000여개가 있다!
1. 가구원 배경 및 개인사
2. 가구여건 및 복지욕구
3. 사회복지 가입 및 수급여부
4. 경제 상황
5. 근로

### 한국인의 삶을 파악하기
* 분석1: 성별에 따른 소득 
* 분석2: 나이와 소득의 관계 
* 분석3: 연령대에 따른 소득 
* 분석4: 연령대 및 성별에 따른 소득

# 기본 설정:computer:
> foreign 패키지 : 통계분석 소프트웨어인 SPSS, SAS, STATA 등의 파일을 불러오는 기능을 제공한다.

### 패키지 설치
* `install.packages("foreign")`
* `install.packages("dplyr")`
* `install.packages("ggplot2")`
### 패키지 불러오기
* `library(foreign)`
* `library(dplyr)`
* `library(ggplot2)`
### 데이터 로드 및 카피하기
* `raw_ welfare <- read.spss("data_spss_koweps2014.sav",to.data.frame = T)`
* `welfare <- raw_welfare`
### 데이터 검토
* `dim(welfare)` : 객체의 치수(크기, 규모, 차원)를 보여주거나 설정하는 함수
* `str(welfare)` : 객체의 구조(데이터타입, 변수명, 변수 개수, 관측치 수)를 보여주는 함수
* `head(welfare)`
* `summary(welfare)`
* `View(welfare)`
### 사용할 변수의 변수명 전환
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/img2/1.PNG" width = "500px"/></h1>

* `welfare <- rename(welfare, sex = h0901_4, birth = h0901_5, income = h09_din)` : rename을 사용해 한 번에 바꿔준다

# 분석1 : 성별에 따른 소득:couple: 
### 절차
1. 변수 검토 및 정제 - 성별 
 * 1-1.변수 검토, 수정 
	 * `class(welfare$sex)` : 데이터 속성을 파악한다. (남 1, 여 2)
	 * `summary(welfare$sex)` : 성별을 나타내는 숫자 데이터는 의미가 없다.
	 * `table(welfare$sex)` : 총 수를 한 번에 알 수 있다.
 *  1-2.정제 - 이상치 확인 및 결측처리 
	 * 이상치는 9를 나타내므로 9가 있다면 결측처리를 한다.
	 * `table(is.na(welfare$sex))` : 결측치 확인
	 * `welfare$sex <- ifelse(welfare$sex == 9, NA, welfare$sex)` : NA로 바꾸고 저장
* 성별 결과
	* `welfare$sex <- ifelse(welfare$sex == 1, "male", "female")` : 변수명을 바꿔준다
	* `qplot(welfare$sex)`
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/img2/2.PNG" width = "500px"/></h1>

> 가구주를 의미하기때문에 남성 데이터가 월등하게 많다.

 2. 변수 검토 및 정제 - 소득 
 * 2-1.변수 검토, 수정 
	 * `class(welfare$income)`
	 * `summary(welfare$income)`  : 가구 구성원의 소득 합으로 부채가 소득보다 많으면 -가 나올 수 있다.
	*	<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/img2/12.PNG" width = "600px"/>
	* `qplot(welfare$income) + xlim(0, 10000)` : 그래프가 보기 힘들어지므로 x값 범위를 설정한다.
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/img2/3.PNG" width = "500px"/></h1>

* 2-2 정제 - 이상치 확인 및 결측처리
3. 성별 소득 평균 분석 
* 성별 소득 평균표 생성 
	* `sex_income <- welfare %>% group_by(sex) %>% summarise(mean_income = mean(income))`
* 그래프 생성
	* `ggplot(data = sex_income, aes(x = sex, y = mean_income)) + geom_col()`
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/img2/4.PNG" width = "500px"/></h1>

> 가구주의 성별별 소득 평균으로 여성 데이터가 낮은 이유는 1인 가구 혹은 한부모 가정 이 있을 수 있기때문이다.

### 가구주의 소득이므로 분석 결과를 확정짓기 어렵다... (ex. 남성이 여성보다 소득이 높다) 

# 분석2 : 나이와 소득의 관계:man:
### 절차
1. 변수 검토 및 정제 - 나이 
* 1-1.태어난 연도 변수 검토 
	* `class(welfare$birth)`
	* `summary(welfare$birth)`
	* `qplot(welfare$birth)`
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/img2/5.PNG" width = "500px"/></h1>

> 이 데이터는 주로 노년층을 대상으로 수집해서 노년층 데이터가 다른 집단에 비해 많다.
*  1-2.정제 - 이상치 확인 및 결측처리
*  1-3.나이 변수 생성 
	* `welfare$age <- 2014-welfare$birth+1`
	* `summary(welfare$age)`
	* `qplot(welfare$age)`
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/img2/6.PNG" width = "500px"/></h1>

2. 변수 검토 및 정제 - 소득 
* 앞에서 완료
3. 나이별 소득 평균 분석 
* 나이별 소득 평균표 생성 
	* `age_income <- welfare %>% group_by(age) %>% summarise(mean_income = mean(income))` : 나이대별로 소득 평균을 구한다
*  그래프 생성
	* `ggplot(data = age_income, aes(x = age, y = mean_income)) + geom_point()`
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/img2/7.PNG" width = "500px"/></h1>

> 샘플의 개수가 각각 다르므로 대표성이 없다.
> => 연령대 구간을 설정하자
# 분석3 : 연령대에 따른 소득:older_woman:
### 절차
1. 변수 검토 및 정제 - 연령대 
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/img2/8.PNG" width = "500px"/></h1>

* 1-1.연령대 변수 생성 
	* `welfare <- welfare %>% mutate(ageg = ifelse(age < 30, "young", ifelse(age <= 59, "middle","old")))`
	* `table(welfare$ageg)`
	* `qplot(welfare$ageg)`
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/img2/9.PNG" width = "500px"/></h1>

> "young"은 대표성이 없으므로 제외한다.
3. 변수 검토 및 정제 - 소득
* 앞에서 완료됨 

4. 연령대별 소득 평균 분석 
* 연령대별 소득 평균표 생성 
	* `welfare_income <- welfare %>% filter(ageg != "young") %>% group_by(ageg) %>% summarise(mean_income = mean(income))` : "young"을 제외하고 평균 소득을 구한다.
* 그래프 생성
	* `ggplot(data = welfare_income, aes(x = ageg, y = mean_income)) + geom_col()`
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/img2/10.PNG" width = "500px"/></h1>

# 분석4 : 연령대 및 성별에 따른 소득:running:
### 절차
1. 연령대 및 소득 평균표 생성
	* `sex_income <- welfare %>% filter(ageg != "young") %>% group_by(ageg, sex) %>% summarise(mean_income = mean(income))`
2. 그래프 만들기
	* `ggplot(data = sex_income, aes(x = ageg, y = mean_income, fill = sex)) + geom_col(position = "dodge")`
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/img2/11.PNG" width = "500px"/></h1>

> fill = sex : 성별을 각각 다른 색으로 칠해준다.
> position = "dodge" : 같은 공간에 차지하는 값을 따로 떨어뜨려 정렬한다.  (디폴트값 = 스텍)
