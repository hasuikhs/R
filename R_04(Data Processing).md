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
     # 1. select()를 이요하여 추출
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

     

