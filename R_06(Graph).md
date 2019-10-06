## R_06(Graph)

1. #### 산점도(Scatter Plot)

   - Data를 x축과 y축에 점으로 표현한 그래프
   - 산점도는 나이와 소득처럼 연속 값으로 된 두 변수의 관계를 표현할 때 사용

   ```R
   # 산점도 만들기
   
   library(ggplot2)
   
   # mpg data를 load, x축은 displ, y축은 hwy로 지정해 배경 생성 : 데이터, 축
   ggplot(data = mpg, aes(x = displ, y = hwy))
   
   # 산점도에 점을 그리는 함수 geom_point() : 그래프 종류
   ggplot(data = mpg, aes(x = displ, y = hwy)) + geom_point()
   
   # x축 범위를 지정하는 함수 xlim(x, y), y축 범위를 지정하는 함수 ylim(x, y) : 세부 설정
   # x축을 x~y까지로 지정 y 포함 
   ggplot(data = mpg, aes(x = displ, y = hwy)) + geom_point() + xlim(3, 6)
   ```

2. #### 막대 그래프(Bar Graph)

   - Data의 크기를 막대의 길이로 표현한 그래프
   - 집단 간 차이를 표현할 떄 주로 사용

   ```R
   # 평균표 만들기
   
   library(dplyr)
   
   df_mpg <- mpg %>% group_by(drv) %>% summarise(mean_hwy = mean(hwy))
   
   df_mpg
   
   ##  A tibble: 3 x 2
   #   drv   mean_hwy
   #   <chr>    <dbl>
   # 1 4         19.2
   # 2 f         28.2
   # 3 r         21 
   ```

   ```R
   # 평균 막대 그래프 생성하기 geom_col()
   ggplot(data = df_mpg, aes(x = drv, y = mean_hwy)) + geom_col()
   
   # 크기 순으로 정렬 reorder(축 명, 기준)
   ggplot(data = df_mpg, aes(x = reorder(drv, -mean_hwy), y = mean_hwy)) + geom_col() 
   ```

   ```R
   # 빈도 막대 그래프 생성하기 geom_bar()
   ggplot(data = mpg, aes(x = drv)) + geom_bar()
   ```

   * geom_col() vs geom_bar()

     ```
     요약표를 이용하는지 원자료를 이용하는지에 따라 그래프를 만드는 절차와 함수가 다르므로 유의 바람
     ```

3. #### 선 그래프(Line Graph)

   - 시간에 따라 달라지는 데이터를 표현한 그래프

   ```R
   # 시계열 그래프 만들기 geom_line()
   ggplot(data = economics, aes(x = date, y = unemploy)) + geom_line()
   ```

4. #### 상자 그림(Box Plot)

   - Data의 분포를 직사각형 상자 모양으로 표현한 그래프

   ```R
   # 상자 그림 만들기 geom_boxplot()
   ggplot(data = mpg, aes(x = drv, y = hwy)) + geom_boxplot()
   ```

   |    상자 그림     |      값       |             설명              |
   | :--------------: | :-----------: | :---------------------------: |
   | 상자 아래 세로선 |   아랫수염    |  하위 0~25% 내에 해당하는 값  |
   |    상자 밑면     | 1사분위수(1Q) |       하위 25% 위치 값        |
   | 상자 내 굵은 선  | 2사분위수(2Q) |   하위 50% 위치 값(중앙값)    |
   |    상자 윗면     | 3사분위수(3Q) |       하위 75% 위치 값        |
   |  상자 위 세로선  |    윗수염     | 하위 75~100% 내에 해당하는 값 |
   | 상자 밖 점 표식  |    극단치     | Q1, Q3 밖 1.5 IQR을 벗어난 값 |

   - 1.5 IQR : 사분위 범위(Q1~Q3 간 거리)의 1.5배