#객체지향 프로그래밍

Decorator
데코레이터는 같은 클래스나 인터페이스를 상속하는 객체들이 공통으로 행하는 행동이 있다면 그 객체들의 원래클래스들을 각각 상속해서 새로운 클래스를 만들 필요없이 하나의 데코레이터 내에서 원래의 슈퍼클래스나 인터페이스를 상속받은 어떤 객체라도 상관없이 하나의 데코레이터내에서 지정 된 함수로 처리할 수 있도록 만든 효율적인 디자인 패턴이다.
예를 들어 커피라는 슈퍼클래스가 있고 그 클래스를 상속받은 아메리카노, 카페라떼, 카페모카 등 커피 종류들이 있다고 하면 데코레이터를 사용하지 않으면 ice나 샷추가, 휘핑추가등을 해서 다른 커피를 만들기 위해 기존의 아메리카노나 카페라떼등을 상속해 또 다른 클래스를 각 커피마다 몇 개씩 만들어야 해서 비효율적이다.
하지만 데코레이터를 이용해 커피를 상속받은 샷추가라는 클라스를 만들고 함수 정의를
def 샷추가(Coffee coffee)
{
	coffee.price += 500
	coffee.shot += 1
}
이런식으로 만들어서 샷추가(coffee)를 만들면 coffee에 어떤 커피 종류가 오던 클래스를 상속해서 새로 정의할 필요 없이 샷추가를 사용한 커피에 500원을 추가하고 샷1개를 추가할 수 있어 하나의 데코레이터로 여러 클래스를 대신 할 수 있어 매우 효율적이다.
위에 샷추가 같이 하나의 클래스로 여러 클래스의 역활을 대신 할 수 있도록 만든 것을 데코레이터라고 한다.


Copy와 Equal의 차이
A라는 객체가 있고 B라는 객체가 있다고 가정하자
A.copy() = B 라고 하면 A의 현재 속성과 값을 똑같이 가지고 있는 B라는 객체를 하나 더 만드는 것이다. A와 B라는 각 객체의 이름이 각각 stack에 저장 된다고 하면 A의 속성은 메모리의 heap에 1번지라는 주소에 저장되어 있는데 copy를 했으므로 heap의 2번지에 1번지에 있는 A의 속성값을 그대로 복사해와 2번지에 똑같이 저장하는 것이다.
서로 다른 메모리 주소를 나타내므로 copy한 뒤 A의 속성 값을 변경하더라도 B는 copy받은 A의 초기값 그대로를 나타내므로 A와 B의 값은 서로 영향을 미치지 않는다

반대로 A=B 식으로 대입을 하면 A와 B의 이름은 각각 stack에 저장되는건 같지만 같다고 equal 처리를 했으므로 A의 속성을 나타내는 heap의 1번지를 B도 같이 가르키게 된다. B도 heap의 1번지를 그대로 가르키는 것이다.
이 상태에서 A의 속성 값을 변경한다면 B도 같은 위치를 가르키고 있으므로 A를 따라 똑같이 변화하게 된다.
따라서 A가 변화할 때 B도 따라서 변화한다.
이 방식이라고 반드시 나쁜것은 아니다.
예를들어 쟝고로 웹 사이트를 만들 때 인스타그램등을 예로 들면 화면에 하트를 터치하면 보이는 화면을 관리하는 view의 하트도 +1되야 하고 관리자페이지의 하트도 +1이 동시에 되야하므로 equal방식을 이용해 구현해놓았다면 하나의 액션으로 한 번에 처리할 수 있으므로 효율적이다.

함수구분
객체지향언어에서는 객체를 만들고 그 객체에서 사용이 가능한 instance method(객체함수)와 객체를 만들지 않아도 사용할 수 있는 class method로 구분이 가능하다
