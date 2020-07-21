# :point_up: 데이터 전처리
* dplyr 패키지를 사용

| 함수 | 기능 |
|--|--|
| filter() | 행 추출 |
| select() | 열 추출 |
| arrange() | 정렬 |
| mutate(0 | 변수 추가 |
| summarise() | 통계치 산출 |
| group_by() | 집단별로 나누기 |
| left_join() | 데이터 합치기(열) |
| bind_rows() | 데이터 합치기(행) |

* R에서 사용하는 기호_ 논리연산자

| 논리 연산자 | 기능 |
|--|--|
| < | 작다 |
| <= | 작거나 같다 |
| > | 크다 |
| >= | 크거나 같다 |
| == | 같다 |
| != | 같지 않다 |
| & | 그리고 |
| %in% | 매칭확인 |

 +) | : 또는(써지지 않아서 별도로 씀)

* R에서 사용하는 기호_ 산술 연산자

| 산술 연산자 | 기능 |
|--|--|
| + | 더하기 |
| - | 빼기 |
| * | 곱하기 |
| / | 나누기 |
| ^ , ** | 제곱 |
| %/% | 나눗셈의 몫 |
| %% | 나눗셈의 나머지 |

* 파이프 연산자
	* %>% : 앞에 있는 출력 결과를 뒤에 함수에 보내준다.
	* 가독성을 위해 %>% 뒤는 줄바꿈을 해준다.
 
# 1. 조건에 맞는 데이터만 추출
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/400.PNG" width = "500px"/>

*  `exam <- read.csv("csv_exam.csv")`
 * `exam %>% filter(class == 1)` : exam에서 class가 1인 경우만 추출하여 출력
 * `exam %>% filter(math > 50)` : 수학 점수가 50점을 초과한 경우 추출하여 출력
 * `exam %>% filter(english > 90 | science > 50)` : ' | '는 또는이라는 의미로, 둘 중 하나라도 해당하면 추출
 * `exam %>% filter(class %in% c(1,3,5))` : class가 1,3,5  중 하나라도 해당하는 경우 추출하여 출력(위 코드랑 동일한 의미)
 
### 추출한 행으로 데이터 만들기
 * `class1 <- exam %>% filter(class == 1)`
 * `mean(class1$math)` : 1반 수학 점수 평균 구하기

# 2. 필요한 변수만 추출
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/404.PNG" width = "500px"/>

* select()를 사용해 필요한 변수만 추출한다.
* `exam %>% select(english)` : 영어점수만 추출하여 출력
* `exam %>% select(math, english)` : 영어, 수학점수만 추출하여 출력
* `exam %>% select(-math)` : 수학 점수 제외하고 모두 출력
* `exam %>% filter(class == 1) %>% select(english)` : class가 1인 행만 추출한 다음 english 추출
* `exam %>% select(id, math) %>% head` : id, math를 추출하고 앞부분 10행까지 출력
# 3. 데이터 정렬
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/403.PNG" width = "500px"/>

* `exam %>% arrange(math)` : 오름차순 정렬
* `exam %>% arrange(desc(math))` : 내림차순 정렬
* `exam %>% arrange(class ,math)` : 여러 개 오름차순 정렬
> **데이터 순서 주의**
>` exam %>% arrange(math, class)`로 데이터 순서가 바뀌게 되면 제대로 출력이 되지 않는다.

# 4. 파생변수 추가
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/406.PNG" width = "500px"/>

* `exam %>% mutate(total = math + english + science) %>% head` : 모든 점수를 더한 total 변수를 추가하고 일부 추출
* `exam %>% mutate(total = math + english + science, mean = (math + english + science)/3)` : 여러 파생변수 한 번에 추가
* `exam %>% mutate(test = ifelse(science >= 60, "pass", "fail"))` : 조건문을 사용해 파생변수 생성
* `exam %>%  mutate(total = math + english + science) %>% arrange(total)` : 생성한 파생변수 바로 활용 가능

> **여기서 잠깐!!**
> Day3때 `df$var_sum <- df$var1 + df$var2` 이런 방법으로 파생변수를 생성했는데 왜 여기서는 [데이터$변수]를 쓰지 않는 것일까!?

> **dplyr 패키지 함수를 사용해서 그렇다!! [데이터$]부분이 생략되있다고 생각하면 된다**

# 5. 집단 별로 데이터 요약
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/408.PNG" width = "500px"/>

* 요약
`exam %>%`
  `group_by(class) %>%` #class별로 분리
  `summarise(mean_math = mean(math),` # math 평균
            `sum_math = sum(math),`   # math 합계
            `median_math = median(math),`  # math 중앙값
            `n = n())` # n : 행의 개수(=학생수)
            
 * 자주 사용하는 요약 통계량

| 함수 | 의미 |
|--|--|
| mean() | 평균 |
| sd() | 표준편차 |
| sum() | 헙계 |
| median() | 중앙값 |
| min() | 최솟값 |
| max() | 최댓값 |
| n() | 빈도 |

* `mpg %>%`<br/>
  `   group_by(manufacturer, drv) %>%` # 회사별, 구방방식별 분리<br/>
  `   summarise(mean_cty = mean(cty)) %>%` # cty 평균 산출<br/>
  `   head(10)`

# 6. 데이터 합치기
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/410.PNG" width = "500px"/>

### 가로 데이터
* 중간고사 데이터 생성
	* `test1 <- data.frame(id = c(1,2,3,4,5), midterm = c(60,70,80,90,85))`
	* `test2 <- data.frame(id = c(1,2,3,4,5), final = c(70,83,65,95,80))`
* 가로로 데이터 합치기
	* `total <- left_join(test1, test2, by = "id")` : id를 기준으로 test1과 test2 데이터를 합쳐라

* 기존의 데이터자료에 합치기
	* name 데이터 생성
		*  `name <- data.frame(class = c(1,2,3,4,5), teacher = c("kim","lee","park","choi","jung"))`
	* 기존 exam 데이터에 name데이터 합치기
		* `exam_new <- left_join(exam, name, by = "class")`
		
### 세로 데이터
*  1반~ 5반, 6반 ~ 10반 시험 데이터 생성
	*  `group_a <- data.frame(id=c(1,2,3,4,5), test = c(60,70,80,90,85))`
	* `group_b <- data.frame(id=c(6,7,8,9,10), test=c(70,83,65,95,80))`
* 세로로 데이터 합치기
	* 행을 붙여주는 것이므로 'bind_rows'를 쓴다
		* `group_all <- bind_rows(group_a, group_b)` 
		
# :fire: 연습문제
### :heart: 조건에 맞는 데이터 추출 문제
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/401.PNG" width = "700px"/></h1><br/>

* mpg데이터 불러오기<br/>
`mpg <- as.data.frame(ggplot2::mpg)`
* A1<br/>
`mpg_d4 <- mpg %>% filter(displ <= 4)`<br/>
`mpg_d5 <- mpg %>% filter(displ >= 5)`<br/>
`mean(mpg_d4$hwy) `<br/>
`mean(mpg_d5$hwy)`  <br/>
결과 : 4 이하가 더 높다

* A2<br/>
`mpg_audi <- mpg %>% filter(manufacturer == "audi")`<br/>
`mpg_toyota <- mpg %>% filter(manufacturer == "toyota")`<br/>
`mean(mpg_audi$cty)`<br/>
`mean(mpg_toyota$cty)`<br/>
결과 : toyota가 더 높다

* A3<br/>
`mpg_manu3 <- mpg %>% filter(manufacturer == "chevrolet" | manufacturer == "ford" | manufacturer == "honda")`
`mean(mpg_manu3$hwy)`<br/>
결과 : 22.50943

### :yellow_heart: 필요한 변수 추출 문제
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/402.PNG" width = "700px"/></h1><br/>

* A1<br/>
 `mpg_new <- mpg %>% select(class, cty)`
* A2<br/>
`mpg_suv <- mpg_new %>% filter(class == "suv")`<br/>
`mpg_cp <- mpg_new %>% filter(class == "compact")`<br/>
`mean(mpg_suv$cty)`<br/>
`mean(mpg_cp$cty)` <br/>
결과 : compact 자동차가 더 높다 

### :green_heart: 데이터 추출 문제
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/405.PNG" width = "700px"/></h1><br/>

* A1<br/>
`mpg %>%`<br/>
`ilter(manufacturer == "audi") %>%`<br/>
`arrange(desc(hwy)) %>%`<br/>
`head(5)`<br/>
+) 높은순 = 내림차순
### :blue_heart: 파생변수 생성
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/407.PNG" width = "700px"/></h1><br/>

* A1<br/>
`mpg_new <- mpg %>% mutate(total = hwy + cty)`
* A2<br/>
`mpg_new <- mpg_total %>% mutate(total_mean = total/2)`
* A3<br/>
`mpg_new %>% arrange(desc(total_mean)) %>% head(3)`
* A4<br/>
`mpg %>%`<br/>
  `   mutate(total = hwy + cty, total_mean = total/2) %>%`<br/>
  `   arrange(desc(total_mean)) %>%` <br/>
  `   head(3)`

### :purple_heart: 집단 별 데이터 요약 문제
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/409.PNG" width = "700px"/></h1><br/>

* A1<br/>
`mpg %>% group_by(class) %>% summarise(mean_cty = mean(cty))`
	* class별로 분리해서 cty 평균을 구한다 
* A2<br/>
`mpg %>% group_by(class) %>% summarise(mean_cty = mean(cty)) %>% arrange(desc(mean_cty))`
	* class별로 분리해서 cty 평균을 구한뒤 내림차순 한다
* A3<br/>
`mpg %>% group_by(manufacturer) %>% summarise(mean_hwy = mean(hwy)) %>% arrange(desc(mean_hwy)) %>% head(3)`
	*	제조사별로 분리해서 hwy 평균을 구하고 내림차순 한다
* A4<br/>
`mpg %>% filter(class == "compact") %>% group_by(manufacturer) %>% 
  summarise(count = n()) %>% arrange(desc(count)) `
  * class변수에서 "compact" 데이터를 추출하여 제조사별로 compact 개수를 count변수에 저장한 후 내림차순으로 나열한다.

### :heartpulse: 데이터 합치기
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/411.PNG" width = "700px"/><br/>
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/412.PNG" width = "700px"/>
</h1>

+) stringsAsFactors : Factor타입 변환 유무
* A1<br/>
`mpg_fl <- left_join(mpg, fuel, by = "fl")`
* A2<br/>
`mpg_fl %>% select(model, fl, price_fl) %>% head(5)`
