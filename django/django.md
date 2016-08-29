
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
하나의 파일에서 다른 파일에 정의되어 있는 클래스나 함수를 사용하기 위해서는 import해야 사용할 수 있다?


들여쓰기
파이썬에서는 if나 for등을 사용할 때 들여쓰기로 해당 함수가 사용되는 부분을 구별한다
c나 자바에서 함수 밑에{}에 묶인부분이 해당함수가 작동하는 구간이라면 파이썬에서는
if
	~		처럼 if나 for이 나오고 한 번 들여쓰기가 되야 해당 함수가 작동하는 부분에 포함된다.


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


template
템플릿을 상속하면 템플릿 전체의 모습을 구조화할 수 있어 코드의 재사용이나 변경이 용이하고, 사이트 UI의 룩앤필을 일관되게 가져갈 수 있다.
사이트 전체적으로 조화로운 룩앤필을 위해 템플릿 상속을 3단계로 사용하는 것을 권장하고 있다.

1단계: 사이트 전체의 룩앤필을 담고 있는 base.html을 만든다
2단계: 사이트 하위의 섹션별 스타일을 담고 있는 base_news.html, base_sports.html등의 템플릿을 만든다
2단계의 템플릿들은 1단계의 템플릿을 상속받아 만든다
3단계: 개별 페이지에 대한 템플릿을 만든다. 3단계 템플릿들은 2단계 템플릿 중에서 적절한 템플릿을 상속받아 만든다
예를 들어 어떠한 뉴스를 나타내는 페이지를 만들고 싶으면 2단계의 뉴스폼의 템플릿을 상속받아 원하는 기사를 보여주도록 변경시켜 만들면 된다.

기본 형태나 폼등의 html을 만든 뒤 내용이 변경되는 부분은 block처리를 해놓는다
예를 들어 base.html의 title로 {% block title %}My site{% endblock %}형태로 만들어 놓은 뒤 base.html을 상속받아 base_news.html을 만든다고 하면
{% extends "base.html" %} - 이렇게 base.html을 상속받은 뒤
{% block title %}Today news{% endblock %}이렇게 바꿔 주면 변경하지 않은 부분은 base.html을 상속받아 그대로 나타내고 title만 변경한것처럼 Today news로 변경된다.
endblock 처리할때도 가독성을 위해서 {% endblock title %}처럼 해줄 수 있다


Form
HTTP 프로토콜 폼에서 사용할 수 있는 메소드는 GET과 POST뿐이다.
장고는 이 중에서도 폼 처리에는 POST 방식만을 사용하고 있다.
검색 폼에는 GET이 적절하지만 대부분의 경우에는 POST가 더 적절하다.

데이터가 없는 폼을 언바운드(unbound)폼이라고 하며, 언바운드 폼은 렌더링되어 사용자에게 보여질 때 폼은 비어있거나, 디폴트값으로 채워진다.
바운드폼은 제출된 데이터를 가지고 있어서 데이터의 유효성 검사를 하는데 사용된다
모든폼 클래스는 django.forms.Form의 자식 클래스로 생성된다.

폼을 처리하기 위해 뷰는 2개가 필요하다.
하나는 폼을 보여주는 뷰이고, 다른 하나는 제출된 폼을 처리하는 뷰이다.
2개의 뷰는 하나의 뷰로 통합하여 처리할 수 있는데, 장고에서는 하나의 뷰로 통합하여 폼을 처리하는 것을 권장하고 있다.
하나의 뷰에서 2가지 기능을 처리하기 위해서는 처음 사용자에게 보여주는 폼과 사용자가 데이터를 입력한 후 제출된 폼을 구분하여 처리할 수 있어야한다
장고에서는 HTTP 메소드로 2가지를 구분한다.
뷰가 GET방식으로 요청을 받은 경우에는 사용자에게 처음으로 폼을 보여주도록 처리하고, 뷰가 POST방식으로 요청을 받은 경우에는 데이터가 담긴 제출된 폼으로 간주하여 처리한다.

장고의 폼 클래스는 모든 필드에 대해 유효성 검사 루틴을 실행시키는 is_valid() 메소드를 가지고 있다. 
사용자로부터 이름을 입력받아 저장하기 위한 폼을 만든다고 할 때 django.forms를 상속받아 NameForm이라는 클래스를 새로 만들고 뷰에서 폼을 제어해야 하므로 뷰에 Nameform을 제어하는 함수를 만들고 그 함수내에서 request.method == 'POST'인지 request.method == 'GET' 이냐에 따라서 구분하여 
request가 POST이면 데이터가 이미 담겨있으므로 form = NameForm(request.POST) 처럼 form에 request를 인자로 담아 데이터가 담긴 폼을 만든 뒤 is_valid()를 통해 유효성 검사를 하고 유효하다면 자신이 의도한대로 처리를 한 뒤 새로운 URL로 리다이렉션 시켜준다
request.method == 'GET'이라면 빈 폼을 사용자에게 render 시켜주면 된다.


상속
클래스를 상속할 때는 해당 클래스가 들어있는 위치를 import하고 클래스를 만들 때 클래스의 인자로 상속받을 클래스를 입력한다
예를 들어 class Myview(View) 는 View 클래스를 상속받은것이다.


클래스형 뷰
뷰를 작성하는 방법은 이제까지 써 온 함수를 이용한 방식 말고 클래스형 뷰를 이용하여서도 만들 수 있다.
프로젝트가 복잡해질수록 클래스형 뷰가 더 좋다.
작성은 이제까지와 마찬가지록 views.py에 작성하면 된다
클래스형 뷰를 작성하기 위해 views.py에 from django.views.generic import view를 하면 된다.
클래스형 뷰를 이용할 때는 urls.py에서 해당 url에 대해 컨트롤 할 view를 지정해 줄 때 as_view() 함수를 이용한다.
예를 들어 index클래스에 작성을 했다면 index url에 대한 view를 index.as_view()함수로 지정해주면 된다.
as_view() 메소드는 클래스의 인스턴스를 생성하고, 그 인스턴스의 dispatch() 메소드를 호출한다.  dispatch()메소드는 요청을 검사해서 GET,POST등의 어떤 HTTP 메소드로 요청되었는지를 알아낸 다음, 인스턴스 내에서 해당 이름을 갖는 메소드로 요청을 중계해준다.
as_view() 함수와 dispatch() 함수는 View클래스안에 정의되어 있고 클래스형 뷰를 만들때는 View 클래스를 상속받아 만드므로 해당 함수가 제공된다
클래스형 함수는 GET이나 POST등의 서로 다른 request를 처리할 때 if를 사용하지 않고 method의 이름으로 구별하므로 코드의 가독성이 좋다.
그리고 다중상속등의 객체 지향 기술이 가능하므로 코드의 재사용성이나 개발 생산성을 획기적으로 올려준다.


Generic view
지네릭 뷰(Generic view)는 개발과정에서 공통적으로 사용할 수 있는 기능들을 추상화하고, 이를 장고에서 미리 만들어 기본적으로 제공해주는 클래스형 뷰를 말한다.
클래스형 뷰를 만들때는 보통 이 지네릭 뷰를 상속받아서 작성한다
Template view는 해당 URL로 웹 요청이 들어오면, 단순하게 템플릿을 보여줄 때 사용한다. TemplateView를 사용할 때는 TemplateView를 상속받아 Views.py에 작성하는 방법도 있고 urls.py에서 TemplateView를 import하면 클래스형 뷰를 만들고 함수를 짤 필요도 없이 해당 템플릿으로 바로 render 시킬수도 있다.
지네릭 뷰에 대한 전체리스트 및 설명은
https://docs.djangoproject.com/en/1.7/ref/class-based-views/


로깅
로거(logger)는 로깅 시스템의 시작점으로, 로그 메시지를 처리하기 위해 메시지를 담아두는 저장소라고 할 수 있다.
로거는 로그 레벨을 가지고, 로그 레벨은 로그 메시지의 중요도에 따라 자신이 어느 레벨 이상의 메시지를 처리할지에 대한 기준이 된다.
로거에 저장되는 메시지를  로그 레코드라고 한다 
로그 레코드의 레벨과 로거의 레벨을 비교해 로그 레코드의 레벨이 로거의 레벨보다 낮으면 해당 레코드는 무시된다.

핸들러는 로거에 있는 메시지에 무슨 작업을 할 지 정하는 엔진이다.
핸들러도 로그 레벨을 가지고 핸들러의 레벨보다 로그 레코드의 레벨이 낮다면 로그 레코드는 무시 된다.
로거는 핸들러를 여러개 가질 수 있고 각 핸들러는 서로 다른 로그 레벨을 가질 수 있다.
핸들러를 여러개 사용해 메시지의 중요도에 따라 다른 방식의 로그 처리가 가능합니다.

로그 레코드가 로거에서 핸들러로 넘겨질 때, 필터를 사용해서 로그 레코드에 추가적인 제어를 할 수 있다.
일반적으로 로그레벨에 따라 로그 레코드가 처리 되는데 필터를 이용하면 이에 추가하여 로그 레코드의 처리 기준을 추가 할 수 있다.
예를 들어, 에러 이상의 로그 레코드 중에서도 특정 소스로 부터 오는 로그 레코드만 처리한다는등의 제어를 할 수 있다.


HTML에서의 함수사용
HTML폼에서도 파이썬의 함수를 사용할 수 있는데 클래스 함수는 {% ~ %}의 꼴로 사용하고 객체함수는 {{ ~.~ }} 처럼 괄호2개사이안에 객체.함수의 꼴로 나타낸다
변수하나를 가져와 그 값을 사용할 때도 괄호2개를 쓰는것 같다??
|는 HTML에서 |앞에 있는 텍스트에 함수처리를 할때 사용하는것 같다
예를들어 "books:"|add:modelname|lower라고 하면
books:에 modelname이 더해지고 그 modelname을 소문자처리하라고 써있으므로
books:소문자인modelname의 꼴이 될 것이다.


Url
template에서 {% url %}을 통하여 링크를 걸 때 'books:index'처럼 템플릿폴더:템플릿이름
이러한 형식으로 url을 걸 때 urls.py에서 name으로 지정했던 템플릿의 이름과 url의 주소 값으로 준 템플릿이름과 일치해야 한다
urls에 url의 name으로 주지않은 이름을 템플릿이름으로 입력했다면 제대로 링크가 되지 않으면서 오류가 발생한다.
예를 들어 위에 처럼 books:index 로 url을 걸었다면 template의 books폴더 안에 해당 파일이 있어야 하고 urls에 해당 url을 가르키고 있는 name이 있어야 한다
url을 이용할 때 '~'처럼 ''안에 경로를 입력하고 나서 추가로 입력하는 것은 url로 연결할 때 urls에서 해당 url에 대해서 변수를 담고 있다면 그 변수를 입력해주는것이다.
예를 들어 {% url 'books:book_detail' book.id %} 처럼 url 함수를 처리할때 template밑에 books폴더에 있는 book_detail템플릿에 book.id 주소, 즉 book_detail/book.id 로 연결시켜주는 것이다.



변수
Model에 지정한 클래스 안에 입력된 변수를 사용하기 위해서는 스펠링이 정확해야 한다.
s를 더 쓴다거나 빼먹는다거나 해서 모델에서는 Book 클래스 밑에 authors라고 지정해놓고 template이나 view에서 Book.author라고 쓴다면 모델에 지정된 변수가 아니기 때문에 제대로 나타나지 않는다


Template의 URL
Template을  참조할 URL을 지정할 때는 setting.py에서 중간에 TEMPLATES로 묶여있는 부분에 DIRS가 있는데 그 DIRS를 자신이 template을 먼저 참조 할 폴더를 지정해주면 템플릿을 찾을 때 항상 그 주소를 먼저 참조하게 된다.
이 폴더안에 있는 템플릿은 "base.html"처럼 경로 없이 바로 사용 할 수 있다.
해당 디렉토리가 아닌 다른 템플릿에 링크를 걸거나 템플릿을 상속하기 위해서는 
/polls/{{question.id}}/ 처럼 하드 코딩을 해야한다 


단축키
ctrl + A 를 하면 해당 문서의 전체블록이 선택된다
한번에 모든 문장을 Tab한다거나 지우고 싶을 때 편하게 사용할 수 있다
