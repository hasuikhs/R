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

   