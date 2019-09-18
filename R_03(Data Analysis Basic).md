## R_03(Data Analysis Basic)

1. #### Data 살펴보기

   |   함수    |          기능           |
   | :-------: | :---------------------: |
   |  head()   |   데이터 앞부분 출력    |
   |  tail()   |   데이터 뒷부분 출력    |
   |  View()   | 뷰어 창에서 데이터 확인 |
   |   dim()   |    데이터 차원 출력     |
   |   str()   |    데이터 속성 출력     |
   | summary() |    요약 통계량 출력     |

   ```R
   # 앞의 부분에서 했던 파일 불러오기
   exam <- read.csv("csv_exam.csv")
   
   # 1. head(), tail() - 데이터 앞부분, 뒷부분 확인하기
   head(exam)	# 기본적으로 6행 출력
   head(exam, 숫자)	# 앞에서부터 숫자만큼 출력
   
   # 2. View() - 뷰어 창에서 데이터 확인
   # 엑셀과 유사한 창에 보여줌
   View(exam)
   
   # 3. dim() - 데이터의 행, 열을 보여줌
   dim(exam)
   
   ## [1] 20 5
   
   # 4. str() - 속성 파악하기
   str(exam)	# 데이터 속성 확인
    
   ## 'data.frame' : 2 0 obs. of 5 variables:
   ##  $ id		:  1 2 3 4 5 6 7 8 9 10 ...
   ##  $ class		:  1 1 1 1 2 2 2 2 3 3 ...
   ##  $ math		:  50 60 45 30 25 50 80 90 20 50 ...
   ##  ...
   
   # 5. summary() - 요약 통계량 산출하기
   summary(exam)
   
   ## 각 데이터 속성 별로 Min, 1사분위수, Median, Mean, 3사분위수, Max 출력 
   ```

2. #### 변수명 바꾸기

   - 변수명이 난해하여 이해하기 힘들때는 이해하기 쉬운 변수명으로 변경하자

   ```R
   # dplyr 패키지의 rename()을 이용
   install.packages("dplyr")
   library(dplyr)
   
   # 데이터를 변형하는 작업을 할때에는 복사본을 만들어서 하는 것이 좋다
   df_new <- df_raw
   df_new
   
   ##   var1 var2
   ## 1    1    2
   ## 2    2    3
   ## 3    1    2
   
   df_new <- rename(df_new, v2 = var2)  # var2를 v2로 수정
   df_new
   
   ##   var1   v2
   ## 1    1    2
   ## 2    2    3
   ## 3    1    2
   ```

3. #### 파생변수 만들기

   - 변수를 조합하거나 함수를 조합해 평균 등의 새로운 열을 넣는 것

   ```R
   df <- data.frame(var1 = c(4, 3, 8),
                    var2 = c(2, 6, 1))
   df
   
   ##   var1 var2
   ## 1    4    2
   ## 2    3    6
   ## 3    8    1
   
   df$var_sum <- df$var1 + df$var2
   df
   
   ##   var1 var2 var_sum
   ## 1    4    2		 6
   ## 2    3    6       9
   ## 3    8    1       9
   ```

   ```R
   mpg <- as.data.frame(ggplot2::mpg)
   mpg
   
   mpg$total <- (mpg$cty + mpg$hwy)/2
   head(mpg)
   
   summary(mpg$total)
   
   ##   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
   ##  10.50   15.50   20.50   20.15   23.50   39.50 
   hist(mpg$total)	# total 변수에 대한 히스토그램 생성
   
   # 조건문을 활용한 파생변수 만들기(중첩 조건도 가능)
   mpg$test <- ifelse(mpg$total >= 20, "pass", "fail")
   head(mpg)
   
   ##  manufacturer model displ year cyl      trans drv cty hwy fl   class total test
   ## 1         audi    a4   1.8 1999   4   auto(l5)   f  18  29  p compact  23.5 pass
   ## 2         audi    a4   1.8 1999   4 manual(m5)   f  21  29  p compact  25.0 pass
   ## 3         audi    a4   2.0 2008   4 manual(m6)   f  20  31  p compact  25.5 pass
   ## 4         audi    a4   2.0 2008   4   auto(av)   f  21  30  p compact  25.5 pass
   ## 5         audi    a4   2.8 1999   6   auto(l5)   f  16  26  p compact  21.0 pass
   ## 6         audi    a4   2.8 1999   6 manual(m5)   f  18  26  p compact  22.0 pass
   
   # 빈도표로 판정 보기
   table(mpg$test)
   
   ## fail pass 
   ##  106  128 
   ```

   