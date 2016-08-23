
# django TIL

서버

정적인 페이지와 동적인 페이지를 나누어서 제공
정적인 페이지는 웹 서버를 통해서 제공하고 동적인 페이지는 웹 서버와 별도로 웹 어플리케이션 서버를 이용해 제공한다

쟝고도 다른 웹 프레임워크들처럼 MVC 개념을 사용한다
하지만 쟝고에서는 MVC의 view가 templete이고 Controller가 view로 쓰이므로
이 이름을 따서 MTV라고 한다


참조방식
파이썬은 객체를 equal방식으로 참조한다
예를 들어 dictionary 형태로 'drink' = water 형태로 입력하고 water변수의 현재값이 hotwater 였는데 icewater로 변경시킨 뒤 dictionary를 출력해보면 'drink' = icewater형태와 같이 출력된다.

json
json은 웹프레임에서 많이 쓰는 형태로 string:string 의 형태로 key와 그에맞는 value가 매칭되어있는 형태이다.
예를 들면 "language" : "python"의 형태로 key 와 value의 data를 간단히 넘길 수 있다.
파이썬의 dictionary형태가 json처럼 키와 value가 매칭되어 있다.
dictionary와 json형태로 서로 바꿀 수 있다.

json -> dict 는 다음과 같이 구현 가능하다
import json
json_data = '{"hello": "world", "foo": "bar"}' 
data = json.loads(json_data)

dict -> json 은 다음과 같다
import json
data = {'baz': 'goo', 'foo': 'bar'}
json_data = json.dumps(data)

dict -> json 으로 바꿔 http형태로 response할 수도 있다
import json
from django.http import HttpResponse

def fbview(request):
    data = {'foo': 'bar', 'hello': 'world'}
    return HttpResponse(json.dumps(data), content_type='application/json')

이거는 서버를 구현 할때 클라이언트가 data에 대해 요청을 한다면 dictionary형태로 구현되어 있는 data를 json형태로 바꿔 http형태로 response 해 줄 수 있다.

