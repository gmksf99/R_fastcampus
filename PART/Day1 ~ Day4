# Day 1~4_데이터 기본 문제
<h1 align="center">
<img src = "https://github.com/gmksf99/R_fastcampus/blob/master/.img/413.PNG" width = "700px"/></h1><br/>

* A1
* 미성년자 이므로 [전체 인구 수 - 전체 성인 수]
	* `midwest <- as.data.frame(ggplot2::midwest)`
	* `midwest_new <- midwest %>% mutate(percent_child = (poptotal - popadults)/poptotal*100)`
* A2
	* `midwest_new %>% select(county, percent_child) %>% arrange(desc(percent_child)) %>% head(5)`
* A3
	* `midwest_new <- midwest_new %>%` <br/> 
  `mutate(grade = ifelse(percent_child >= 40, "large", ifelse(percent_child >= 30, "middle", "small")))`
	* `midwest_new %>% group_by(grade) %>% summarise(count = n())`
* A4
	* `midwest_new <- midwest %>% mutate(percent_asian = popasian/poptotal*100)`
	* `midwest_new %>% select(state, county, percent_asian) %>% arrange(percent_asian) %>% head(10)`
