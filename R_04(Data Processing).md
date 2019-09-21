## R_04(Data Processing)

- #### Data Preprocess

  1. ##### 조건에 맞는 데이터만 추출하기

     ```R
     # 1. 먼저 실습에 사용할 파일을 DataFrame으로 만들고 출력
     library(dplyr)
     exam <- read.csv("csv_exam.csv")
     exam
     
     #   id  class  math  english  science
     # 1  1      1    50       98       50
     # 2  2      1    60       97       60
     # 3  3      1    45       86       78
     # 4  4      1    30       98       58
     # 5  5      2    25       80       65
     # 6  6      2    50       89       98
     # ...
     ```

     ```R
     # 2. dplyr 패키지의 filter()를 이용해 1반 학생만 추출
     exam %>% filter(class == 1)
     
     # 조건은 여러 변수에 다양하게 사용 가능하다(>=, <=, !=, ==)
     # 조건을 중복적으로 사용하려면 &(and), |(or)
     
     # 목록에 해당하는 행 구하기
     exam %>% filter(class == 1 | class == 3 | class == 5)
     # 도 가능하지만
     exam %>% filter(class %in% c(1, 3, 5))
     # 또한 가능
     ```

  2. ##### 필요한 변수만 추출하기

     ```R
     # 1. select()를 이용하여 추출
     exam %>% select(math)
     
     # 동시에 여러 변수를 쉼표를 넣어 추출 가능
     exam %>% select(class, math, english)
     
     # 특정 변수를 제외하고 모두 넣기
     exam %>% select(-math)
     ```

     ```R
     # dplyr 함수 조합하기
     # 1. filter()와 select() 조합하기
     
     # class가 1인 행만 추출한 다음 english 추출
     exam %>% filter(class == 1) %>% select(english)
     ```

  3. ##### 순서대로 정렬하기
  
     ```R
     # arrange()를 이용하여 정렬
     exam %>% arrange(math)	# math 오름차순 정렬
     
     exam %>% arrange(desc(math))	# math 내림차순 정렬
     
     # 기준을 두가지로 정할수도 있음
     exam %>% arrange(class, math)	# class를 먼저 정렬하고, math를 다음 기준으로 정렬
     ```
  
  4. ##### 파생변수 추가하기
  
     ```R
     # mutate()를 사용하여 기존 데이터에 파생변수를 만들어 추가하기 가능
     
     exam %>% mutate(total = math + english + science)
     
     # 파생변수 한번에 여러개 추가하기
     exam %>% mutate(total = math + english + science,
                     mean = (math + english + science)/3)
     
     # ifelse() 활용
     exam %>% mutate(test = ifelse(science >= 60, "pass", "fail"))
     ```
  
  5. ##### 집단별로 요약하기
  
     ```R
     # 1. summarise()
     exam %>% summarise(mean_math = mean(math))	# math 평균 산출
     
     ##    mean_math
     ##  1     57.45
     
     # 2. 집단별로 요약하기
     exam %>% group_by(class) # class별로 분리
     		%>% summarise(mean_math = mean(math))
     ##  # A tibble: 5 x 2
     ##    class mean_math
     ##    <int>     <dbl>
     ##  1     1     46.25
     ##  2     2     61.25
     ##  3     3     45.00
     ##  4     4     56.75
     ##  5     5     78.00
     ```
  
  6. ##### 데이터 합치기
  
     ```R
     # 가로로 합치기
     # 중간고사 데이터 생성
     test1 <- data.frame(id = c(1, 2, 3, 4, 5),
                         midterm = c(60, 80, 70, 90, 85))
     # 기말고사 데이터 생성
     test2 <- data.frame(id = c(1, 2, 3, 4, 5),
                         final = c(70, 83, 6, 95, 80))
     
     total <- left_join(test1, test2, by = "id") # id를 기준으로 합쳐 total에 할당
     ```
  
     ```R
     # 세로로 합치기
     groupA <- data.frame(id = c(1, 2, 3, 4, 5),
                          test = c(60, 80, 70, 90, 85))
     groupB <- data.frame(id = c(6, 7, 8, 9, 10),
                         final = c(70, 83, 6, 95, 80))
     
     group_all <- bind_rows(groupA, groupB)
     ```
  
     

