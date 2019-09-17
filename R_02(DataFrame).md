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

2. #### 외부 데이터 이용하기

   ```R
   # 1. xlsx파일을 프로젝트 폴더에 저장한다
   # 2. readx1 패키지를 설치하고 로드
   
   install.packages("readx1")
   library(readx1)
   
   # 3. xlsx파일을 불러오기
   df_exam <- read_excel("파일명.xlsx")
   
   # * 프로젝트 폴더가 아닌 경로에 있는 파일을 불러오려면
   df_exam <- read_excel("c:/easy_r/excel.xlsx") # 같은 형식 /로 구분
   
   # * 만약 첫번째 행부터 자료가 시작된다면
   df_exam <- read_excel("경로", col_names = F)
   
   # * 만약 엑셀 파일에 시트가 여러개 존재한다면
   df_exam <- read_excel("경로", sheet = 1)
   ```

   ```R
   # csv파일 불러오기
   
   # xlsx 파일과는 다르게 R에 내장된 read.csv()를 이용
   df_exam <- read.csv("경로")
   
   # 문자가 들어있는 csv파일을 불러올떄는
   df_exam <- read.csv("경로", stringAsFactors = F)
   ```

3. #### DataFrame을 CSV파일, RData로 저장하기

   ```R
   # DataFrame 만들기
   df_midterm <- data.frame(english = c(90, 80, 60, 70),
                            math = c(50, 60, 100, 20),
                            class = c(1, 1, 2, 2))
   
   # CSV파일로 저장
   write.csv(df_midterm, file = "df_midterm.csv")	# 저장 파일은 프로젝트 폴더에 생성
   ```

   ```R
   # RData 파일 활용
   #  - R전용 파일로 다른 파일들에 비해 R에서 읽고 쓰는 속도가 빠르고 용량이 적다
   #  - R을 사용하지 않는 환경에서는 CSV파일로 보내주자
   
   # RData 파일로 저장
   save(df_midterm, file = "df_midterm.rda")
   
   # rm을 이용해서 DataFrame을 먼저 삭제하자
   rm(df_midterm)
   
   # load를 이용해 불러오기
   load("df_midterm.rda")
   ```