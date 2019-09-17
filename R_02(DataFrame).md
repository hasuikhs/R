## R_02(DataFrame)

1. #### DataFrame 만들기

   ```R
   english <- c(90, 80, 60, 70)
   math <- c(50, 60, 100, 20)
   class <- c(1, 1, 2, 2)
   
   df_midterm <- data.frame(english, math)
   
   df_midterm
   
   ##   english  math  class
   ## 1     90    50      1
   ## 2     80    60      1
   ## 3     60   100      2
   ## 4     70    20      2
   ```

   - 분석하기

     ```R
     # $는 DataFrame 안에 있는 변수를 지정할 때 사용
     
     mean(df_midterm$english)	# df_midterm의 english 평균 산출
     
     ## [1] 75
     
     mean(df_midterm$math)		# df_midterm의 math 평균 산출
     
     ## [1] 57.5
     ```

   - DataFrame 한번에 만들기

     ```R
     df_midterm <- data.frame(english = c(90, 80, 60, 70),
                              math = c(50, 60, 100, 20),
                              class = c(1, 1, 2, 2))
     ```

     