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
   
   # * 결측치가 표함된 데이터를 함수에 적용하면 연산되지 않음
   ```

   