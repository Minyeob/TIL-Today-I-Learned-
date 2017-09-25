# Machine Learning

## TensorFlow
텐서플로(TensorFlow)는 구글 제품에 사용되는 머신러닝(기계학습)을 위한 오픈소스 소프트웨어 라이브러리이다.
파이썬에서는 Package의 형태로 제공되므로 설치하여 편하게 사용할 수 있다.

### Linear Regression
변수들의 식으로 결과를 예측하기 위해 사용되는 방법 중 가장 많이 사용되고 간단한 방법
실제 결과값이 y이고 결과를 예측하기 위한 회귀식이 h(x)=wx+b라면 Linear regression은
cost=1/m(h(x)-y)^2 의 형태로 계산할 수 있는 cost를 최소화시킬 수 있는 Weight인 w를
찾아 결과와 가장 비슷한 값을 예측하는 식을 구하는 방법으로 진행된다.

#### Multi-variable Linear Regression
Tensorflow에서는 직접 계산식을 만들어 과정을 진행할 수 있고 변수가 많은 회귀식의
경우에는 행렬의 곱을 통해 표현하여 간단하게 나타낸다.
즉 변수가 n개라서 h(x)=w1x1 + w2x2 + .... + wnxn의 형태로 굉장히 복잡한 식이라도 
h(x)=xw라고 표현하고 w와 x를 각각 행렬의 형태로 표현하여 계산할 수 있다.
행렬의 곱 형태로 나타낼 때는 h(x)=xw 의 형태로 표현한다면 행렬의 곱만으로도 표현이 가능하므로
xw 의 형태로 많이 표현한다.
Tensorflow에서 식으로 나타낼 때는
  
    hypothesis=tf.matmul(X,W)+b
처럼 matmul을 이용해 matrix multiplication 임을 알려준다.
Placeholder를 통해 machine learning에 사용될 변수를 할당할 때 shape를 통해 instance가 몇개이고
변수의 종류가 몇 개인지 정해준다.

    X=tf.placeholder(tf.float32, shape=[None, 3])
의 형태로 X에 대해 설정해준다면 X는 32비트 float 변수이고 X의 가지수는 3가지 종류이고
학습에 사용될 횟수인 instance의 수는 정하지 않는 것을 의미한다.
None을 이용하면 값으로 이용될 때 배열의 크기만큼 알아서 실행된다.

    W=tf.Variable(tf.random_normal[3,1], name='weight')
처럼 변수 선언을 해 줄때는 3x1 형태의 배열을 말한다.
즉 3개의 변수가 계산을 통해 1개의 변수처럼 사용될 것을 말한다.

##### 학습데이터가 매우 커 여러 개의 파일로 존재하는 경우
tensorflow에서는 데이터가 매우 커 하나의 파일이 아닌 여러 파일로 나눠서 값이 입력되어
있는 경우 Queue를 이용하여 읽고 처리할 수 있다.