## R_05(Data Refinement)

1. ##### 결측치 정제하기

   ```R
   # 결측치 찾기
   # 1. 먼저 결측치가 포함된 DataFrame 생성
   df <- data.frame(sex = c("M", "F", NA, "M", "F"),
                    score = c(5, 4, 3, 4, NA))
   
   # 2. 결측치 확인
   is.na(df)
   
   ##       sex score
   ## [1,] FALSE FALSE
   ## [2,] FALSE FALSE
   ## [3,]  TRUE FALSE
   ## [4,] FALSE FALSE
   ## [5,] FALSE  TRUE
   
   # 3. 결측치가 총 몇개 있는지 출력
   table(is.na(df))
   
   ## FALSE  TRUE 
   ##    8     2 
   
   # 각 변수의 결측치가 몇개씩 있는지 확인
   table(is.na(df$sex))
   table(is.na(df$score))
   
   # * 결측치가 포함된 데이터를 함수에 적용하면 연산되지 않음
   ```

   ```R
   # 결측치 제거하기
   # 1. 결측치 있는 행 제거
   library(dplyr)
   df %>% filter(is.na(score))	# score가 NA인 데이터만 출력
   
   ##   sex  score
   ## 1   F     NA
   
   # 2. 결측치를 제외한 행 추출
   df %>% filter(!is.na(score))
   
   ##   sex score
   ## 1   M     5
   ## 2   F     4
   ## 3 <NA>    3
   ## 4   M     4
   
   # 3. 여러 변수 동시에 결측치 없는 데이터 추출
   df_nomiss <- df %>% filter(!is.na(score) & !is.na(sex))
   df_nomiss
   
   ##   sex score
   ## 1   M     5
   ## 2   F     4
   ## 3   M     4
   
   # * 결측치가 하나라도 있으면 제거
   df_nomiss2 <- na.omit(df)
   
   # 이렇게 한번에 결측치를 제거하는 방법이 편하긴 하지만,
   # 데이터 북석에 필요한 행들끼리 상관분석이 가능할때에도 행이 제거될 가능성이 존재해 비추천
   ```
   
   ```R
   # 평균값으로 결측치 대체하기
   mean(exam$math, na.rm = T)	# 결측치 제외하고 math 평균 산출
   
   exam$math <- ifelse(is.na(exam$math), 55, exam$math) # math가 NA면 55로 대체
   ```
   
   