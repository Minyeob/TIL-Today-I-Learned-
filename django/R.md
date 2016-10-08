#R 프로그래밍

###간단한 명령어들
R에서는 변수에 data를 집어넣을 때 기본적으로 다른 프로그래밍에서 사용하는 = 이나 <-을 이용해 변수 대입을 하면된다.
예를 들어 data = 1, data <- 1 모두 가능하다.

lm은 직선식인 lenear model을 입력할때 사용하는데 lm(공식: 변수~변수, 사용될데이터 data= 데이터이름) 의 꼴로 사용하고
공식은 y~x+1처럼 y=ax+b의 꼴로나타낼때 y~ax+b의 형태로 입력하면 된다.

par는 그래프가 어떻게 보여질지 나타낸다 mfrow는 그래프가 1페이지에 a*b의 갯수가 보일것을 말한다
a=행 개수 b=열 개수 a행 b열의 갯수 행렬의 개념으로 몇행 몇열로 그래프가 표시될것인지를 나타낸다.

$는 앞의 데이터에서 뒤 데이터를 가져온다는거고 data$Time은 data에서 Time을 가져오겠다는 뜻이다.

dev.off는 그래프를 모두 지우고 그래프 옵션을 초기화 할때 이용한다.

summary는 입력한 모델의 분석 결과를 나타낸다.
summary에서 나온 결과값에서 coefficients는 계수를 나타낸다.
estimate는 추정값을 나타내고 std. error는 표준오차, t value는 해당값의 t value를 나타낸다.
intercept는 절편을 의미하므로 linear regression에서는 x절편인 알파값을 말한다
절편 밑 데이터는 x축 데이터의 계수이므로 베타를 말한다
t value와 pr은 정확히 모르겠다, 옆에 별은 추정식의 정확도에 따라 평가를 해주는데 별이높을수록 좋다
R-squared는 총변동에서 회귀모델이 설명할 수 있는 비율을 나타내고 회귀모델이 얼마나 정확한지 보여준다
R-squared가 높을수록 해당 회귀모델의 정확도가 높다고 할 수 있다.

c는값들을 vector 또는 list로 만들 때 이용한다.

abline은 지금 나타나있는 그래프에 직선을 추가할 때 사용한다.
lm으로 linear model을 입력한 내용을 abline하면 해당 model에 대한 값을 추정한 직선을 그래프에 그려준다.

plot은 그래프를 보일 때 사용하고 plot(x값, y값), plot(특정변수)등의 형태로 나타내면 된다.

confint(모델)은 모델에 대한 신뢰구간을 구할 때 사용된다.
confit(fit)처럼 하면 fit에 대해 2.5% 97.5% 신뢰구간을 나타내준다.
이것은 추정값에 대한 95% 신뢰도에 대한 신뢰구간을 나타내준다.

자료 객체들을 결합하여 데이터 프레임을 만들수 있다.
length(원소의개수)가 같은 데이터끼리 묶어 테이블을 만들 수 있다.
data.frame(name, age, sex)처럼 만들고 각 data가 length가 3으로 같다고 하면
attribute가 name,age,sex인 tuple이 3개 인 table이 만들어진다고 생각하면 된다.
sql table을 자신이 원하는 data set을 attribute로 구성해 만든다고 생각하면 된다.
위 처럼 만들면
    name    age sex
1
2
3                               인 테이블이 만들어지는것과 같다.
data.frame(~ , row.names=c("kim", "lee", "choi")) 처럼 row.name을 줌으로써 각 row(tuple)의 이름을 줄 수도 있다.

predict로는 모델에 대해 특정값을 대입했을때의 예측되는 값을 구할 수 있다.
predict(모델이름, 자신이찾을변수값, se.fit, interval, level)의 형태로 값을 예측할 수 있다.
모델이름에는 자신이 만들어놓은 모델, 예를 들어 lm으로 만든 linear model등을 넣으면 된다.
자신이 찾을 변수값에는 자신이 찾을 값의 대입값, 예를 들어 x=3 일때의 y가 구하고 싶다면 x=3을 입력하면 된다.
se.fit에는 standard error가 return된다면 그 에러에 대한 문장을 return할것인지를 나타내는데?? se.fit=TRUE라면 에러가 있을때 특정 값을 return할 것이다.
interval은 예측이 어떤 구간에 대해 예측하는것인지를 나타내는데, 신뢰구간이나 예측구간등을 의미한다. interval="prediction"이라면 예측구간에 대한 예측이 된다.
level은 신뢰도를 나타내는데 level=0.95라면 95% 신뢰도에 대한 신뢰구간을 구하는것이 된다.
