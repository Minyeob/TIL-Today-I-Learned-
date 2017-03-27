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


###C나 C++의 Sort, 람다함수, 객체함수

####Sort
기본적으로 제공하는 Sort 함수는 Sort 되는 조건을 지정해 Sort 해줄 수 있다.
default로 조건이 오름차순으로 되있으며 조건을 바꿔서 Sort 되는 방법을 다르게 해줄 수 있다.
예를 들어
    
    bool cmp(int a,int b) {return a<b;}
    
    sort(a.begin(), a.end(), cmp)     
처럼 sort 함수에 조건을 우리가 만든 조건을 넣어서 sort함수를 사용하면 
Sort가 기본인 sort를 할 때 앞 뒤 비교할 때 a<b 이면 true 를 return 하고, 아니면 false를 return 해 비교 되는 조건을 주는것이다.
 
    
####람다함수
overhead가 가장 적게 사용하기 위해서는 람다함수를 사용할 수 있는데
    
    sort(a.begin(), a.end(), 
    [](const point& a, const point& b)
    {
        return a.x > b.x
    }
    
처럼 주면 재사용이 되지 않는 해당 부분에서만 사용되는 이름없는 람다함수를 넣어주는것이다.
해당 조건에만 마지막 조건으로 입력되있는 함수를 사용해 비교조건을 이용하고 다른 부분에서는 다시 가져다가 사용할 수는 없다.
람다함수를 사용하면 overhead가 가장적게 일어난다.
저기서 파라미터로 const point& a 의 형태로 되어 있는데 이건 포인터로 해당 함수를 가르켜 다시 참조하는것이 아니라 해당 변수가 선언된 부분을 직접 가르켜
직접 참조하는것이다. 시스템 프로그래밍에서 배우는 immediate addressing을 생각하면 된다.


####객체함수
각 객체를 선언할 때 객체안에 그 객체의 이름으로 사용할 수 있는 함수를 선언 해줄 수도 있다.
C++에서는 struct가 객체의 클래스로 사용 되는데 그 안에 inline operator()를 선언해 해당 객체의 이름으로 함수를 사용할 수 있다.

    template<typename T>
    struct less
    {
        int 
        inline bool operator()(const T& a, const T& b)
        {
            retirn a > b;
        }
    }
    
처럼 struct 안에 operator() 를 이용해 함수를 선언해주면 함수를 less() 처럼 사용할 수 있다.
template로 type을 저렇게 선언해주면 데이터타입으로 어떤것이 들어와도 비교할 수 있다.
예를 들어 위의 코드처럼 template으로 T를 선언해주고 a앞에 T라고 데이터타입이 있으면 어떠한 데이터 타입이 들어올 수 있고
어떠한 타입의 값이든 입력 받아 값을 비교해서 결과를 bool 값으로 return 해준다.


###그래프 & 트리
그래프는 배열이나 리스트로 나타낼 수 있다.
C++에서는 리스트 대신에 vector를 사용하는데 그 이유는 리스트의 값들은 메모리 내에서 연속된 주소를 가지지 않아서 캐쉬의 hit ratio(적중률)이 떨어져 속도가 더 느리다.
벡터는 메모리 내에서 연속된 주소를 가지므로 더 높은 hit ratio를 가지므로 속도가 더 빠르므로 보통 벡터를 사용한다.


### &
함수의 파라미터로 자신이 원하는 주소의 값을 넘겨 해당 주소에 있는 값을 계산하고 싶다면 해당 주소와 해당 주소에 있는 값을 모두 넘겨야 한다
이럴 때 파라미터로 &을 포함해서 넘기면 해당 주소에 있는 값을 파라미터로 넘기고 결과로 그 주소에 있는 값을 변경할 수 있다.

    void swap(profile& first, profile& second)
    {
        profile temp;
        temp = first;
        first = second;
        second = temp;
    }
이런식으로 &을 포함해서 값을 넘기면 해당 주소에 대한 해당 값이 파라미터로 넘어가 값이 변경될 수 있다.