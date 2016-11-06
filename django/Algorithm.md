#Algorithm

##Algorithm 이론들과 푸는 과정에서의 C,C++ 내용들

###C++의 stack
C++에서 stack은 #include <stack>을 한다면 C++에서 제공하는 기본 stack을 사용할 수 있고
stack<int> a; 의 형태처럼 데이터 타입을 정해서 해당 stack을 선언해 해당 data type의 stack을 만들 수 있다.
stack.push(123) 처럼 parameter로 push할 데이터를 넣고 stack에 push해줄수 있으며 stack.top()은 현재 stack의 top에 있는 data를 확인할 수 있다.
top은 stack에서 data를 제거하지는 않으며 그냥 top에 있는 data가 무엇인지만 받아온다.
stack.pop()을 통해서 stack의 top에 있는 data를 제거할 수 있는데 pop의 return type은 void이므로 단순히 pop을 통해 변수에 데이터를 입력 해 줄수는 없다.
변수에 스택에서 pop한 결과를 선언하기 위해서는 int a=stack.top(); stack.pop() 처럼 top에 있는 data를 받아오고 pop을 통해 제거하는 형태로 변수에
값을 주고 pop을 통해 stack의 top에 있는 data를 제거해주면 된다.