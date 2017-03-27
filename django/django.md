# django TIL

###서버

정적인 페이지와 동적인 페이지를 나누어서 제공
정적인 페이지는 웹 서버를 통해서 제공하고 동적인 페이지는 웹 서버와 별도로 웹 어플리케이션 서버를 이용해 제공한다

쟝고도 다른 웹 프레임워크들처럼 MVC 개념을 사용한다
하지만 쟝고에서는 MVC의 view가 templete이고 Controller가 view로 쓰이므로
이 이름을 따서 MTV라고 한다


###참조방식
파이썬은 객체를 equal방식으로 참조한다
예를 들어 dictionary 형태로 'drink' = water 형태로 입력하고 water변수의 현재값이 hotwater 였는데 icewater로 변경시킨 뒤 dictionary를 출력해보면 'drink' = icewater형태와 같이 출력된다.
하나의 파일에서 다른 파일에 정의되어 있는 클래스나 함수를 사용하기 위해서는 import해야 사용할 수 있다?


###들여쓰기
파이썬에서는 if나 for등을 사용할 때 들여쓰기로 해당 함수가 사용되는 부분을 구별한다
c나 자바에서 함수 밑에{}에 묶인부분이 해당함수가 작동하는 구간이라면 파이썬에서는
if:
   ~		처럼 if나 for이 나오고 한 번 들여쓰기가 되야 해당 함수가 작동하는 부분에 포함된다.


###json
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

http에 있는 내용을 가져올때는 여러가지 방법이 있다.
requests패키지를 import해 requests.get('http://~~~')도 하나의 방법이다
이 방법을 이용하면 해당 http에 있는 json내용을 가져올 수 있다.
하지만 이 방법으로 가져온 json 객체는 read함수를 가지고 있지 않아 json.loads를 통해 dictionary형태로 바꿀 수가 없다.
json.loads는 string이나 buffer의 형태를 필요로 하는데 requests.get을 이용해 가져온 json객체는 하나의 object로 인식 되어 할 수 없는것 같다.

따라서 json파일을 가져와 dictionary형태로 바꾸어 그 안의 내용을 참조하기 위해서는 다른 방법이 필요하다
이것을 해결할 방법으로는 urllib2 패키지를 import해 urlopen함수를 이용하는 방법이 있다.
먼저 url = "~"의 형태로 http주소를 string화 시켜 변수로 저장하고
page = urllib2.urlopen(url)의 형태로 원하는 http주소의 page를 가져올 수 있다.
urlopen함수는 read()를 포함하고 있다.
따라서 json.loads(page.read())를 하면 목표로 했던 json파일을 가져와 read()로 읽어 스트링화 시킨 뒤 json.loads를 통해 dictionary의 형태로 바꿀 수 있다.
dictionary화 시킨 뒤 자신이 원하는 내용을 가져다가 사용할 수 있다.
json형태에서는 dictionary처럼 검색을 할 수 없는것 같다
따라서 dictionary형태로 바꾸는것이 필요하다

 

###template
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


###Form
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


###상속
클래스를 상속할 때는 해당 클래스가 들어있는 위치를 import하고 클래스를 만들 때 클래스의 인자로 상속받을 클래스를 입력한다
예를 들어 class Myview(View) 는 View 클래스를 상속받은것이다.


###클래스형 뷰
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


###Generic view
지네릭 뷰(Generic view)는 개발과정에서 공통적으로 사용할 수 있는 기능들을 추상화하고, 이를 장고에서 미리 만들어 기본적으로 제공해주는 클래스형 뷰를 말한다.
클래스형 뷰를 만들때는 보통 이 지네릭 뷰를 상속받아서 작성한다
Template view는 해당 URL로 웹 요청이 들어오면, 단순하게 템플릿을 보여줄 때 사용한다. TemplateView를 사용할 때는 TemplateView를 상속받아 Views.py에 작성하는 방법도 있고 urls.py에서 TemplateView를 import하면 클래스형 뷰를 만들고 함수를 짤 필요도 없이 해당 템플릿으로 바로 render 시킬수도 있다.
지네릭 뷰에 대한 전체리스트 및 설명은
https://docs.djangoproject.com/en/1.7/ref/class-based-views/


###로깅
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


###HTML에서의 함수사용
HTML폼에서도 파이썬의 함수를 사용할 수 있는데 클래스 함수는 {% ~ %}의 꼴로 사용하고 객체함수는 {{ ~.~ }} 처럼 괄호2개사이안에 객체.함수의 꼴로 나타낸다
변수하나를 가져와 그 값을 사용할 때도 괄호2개를 쓰는것 같다??
|는 HTML에서 |앞에 있는 텍스트에 함수처리를 할때 사용하는것 같다
예를들어 "books:"|add:modelname|lower라고 하면
books:에 modelname이 더해지고 그 modelname을 소문자처리하라고 써있으므로
books:소문자인modelname의 꼴이 될 것이다.


###Url
template에서 {% url %}을 통하여 링크를 걸 때 'books:index'처럼 템플릿폴더:템플릿이름
이러한 형식으로 url을 걸 때 urls.py에서 name으로 지정했던 템플릿의 이름과 url의 주소 값으로 준 템플릿이름과 일치해야 한다
urls에 url의 name으로 주지않은 이름을 템플릿이름으로 입력했다면 제대로 링크가 되지 않으면서 오류가 발생한다.
예를 들어 위에 처럼 books:index 로 url을 걸었다면 template의 books폴더 안에 해당 파일이 있어야 하고 urls에 해당 url을 가르키고 있는 name이 있어야 한다
url을 이용할 때 '~'처럼 ''안에 경로를 입력하고 나서 추가로 입력하는 것은 url로 연결할 때 urls에서 해당 url에 대해서 변수를 담고 있다면 그 변수를 입력해주는것이다.
예를 들어 {% url 'books:book_detail' book.id %} 처럼 url 함수를 처리할때 template밑에 books폴더에 있는 book_detail템플릿에 book.id 주소, 즉 book_detail/book.id 로 연결시켜주는 것이다.



###변수
Model에 지정한 클래스 안에 입력된 변수를 사용하기 위해서는 스펠링이 정확해야 한다.
s를 더 쓴다거나 빼먹는다거나 해서 모델에서는 Book 클래스 밑에 authors라고 지정해놓고 template이나 view에서 Book.author라고 쓴다면 모델에 지정된 변수가 아니기 때문에 제대로 나타나지 않는다


###Template의 URL
Template을  참조할 URL을 지정할 때는 setting.py에서 중간에 TEMPLATES로 묶여있는 부분에 DIRS가 있는데 그 DIRS를 자신이 template을 먼저 참조 할 폴더를 지정해주면 템플릿을 찾을 때 항상 그 주소를 먼저 참조하게 된다.
이 폴더안에 있는 템플릿은 "base.html"처럼 경로 없이 바로 사용 할 수 있다.
해당 디렉토리가 아닌 다른 템플릿에 링크를 걸거나 템플릿을 상속하기 위해서는 
/polls/{{question.id}}/ 처럼 하드 코딩을 해야한다 


###단축키
ctrl + A 를 하면 해당 문서의 전체블록이 선택된다
한번에 모든 문장을 Tab한다거나 지우고 싶을 때 편하게 사용할 수 있다


###dictionary
dictionary형태에서 자신이 원하는 값을 찾기 위해서는 ["~"]를 이용한다
예를 들어 dictionary형태로 저장된 Kim이라는 사람의 데이터가 있다고 하자.
이사람의 출신 초등학교를 알기 위해서는
Kim["school"]["elementary"] 의 형태로 값을 받아오면 된다



###Model
models.py에 모델의필드들을 정하고 생성할 때 맞는 필드를 주고 ()을 같이 넣어줘야 admin에서 데이터를 생성할 수 있다.
예를 들어 pub_date = models.datetimefield 처럼 ()없이 만든다면 admin에서 해당 값이 보이지 않는다. 따라서 쟝고내에서 값을 만들어줘야 한다.
모델을 다 만들고 admin.py에도 해당 모델을 register해줘야 admin 페이지에서 모델을 확인하고 수정할 수 있다.


###추상 클래스
추상 클래스를 만들기 위해서는 흔히 만들듯이 일반적인 클래스를 만들고 그 안에 내부 클래스로 
	class Meta:
        abstract = True
를 포함한다면 추상클래스가 된다
이 추상클래스는 상속을 위한 부모클래스로 사용이 되고 실제 데이터베이스 테이블을 가지지 않고 정보만을 가지고 있는 추상클래스가 된다.


###모델 초기값
데이터베이스 모델을 설정하고 특정 값을 초기값으로 주기 위해서는 field(default=~)처럼 default값을 줘서 초기값을 설정해줘야 한다
이렇게 하지 않고 name=""처럼 하면 제대로 설정되지 않는것 같다
그리고 field의 옵션을 입력할때 editable=false로 설정하면 지정해놓은 초기값을 변경시킬 수 없다.


###모델 상속
모델을 상속할 때 특정필드를 가져다가 그대로 상속해서 내용만 변경해서 사용하는것은불가능하다.
init함수를 subclass에 정의해 해당 모델을 불러올 때 해당 필드에 대한 값을 변경하도록 하거나 _meta.get_field등을 통해 초기값을 변경할 수 밖에 없다.
init함수를 통해 변경하기 위해서는
 def __init__(self, *args, **kwargs):
        super(CurrencyEUR, self).__init__(*args, **kwargs)
        nation = models.CharField(max_length=3, default='EUR')
        nation.contribute_to_class(self, 'nation')
처럼 init함수를 통해 부모클래스의 init를 상속받아 내용을 변경시키고 밑에 field의 contribute_to_class를 통해 class에 입력되는 값을 바꾸면 된다.
이런식으로 하면 처음 만들때 init함수를 통해 값이 입력되기는 하지만 default로 초기값을 주는것처럼 아예 데이터베이스 초기부터 값이 설정되있지는 않은것같다.
데이터베이스를 애초에 설계할때 subclass마다 값이 다른 부분은 부모클래스에 만들지 말고 각 자식클래스마다 값을 입력해 만드는것이 더 좋은것 같다.



###Object Type
django에서 특정 model에서 자신이 원하는 객체를 구해야 하는 경우가 많은데 이럴 때
a.objects.filter(pk=1)이나  b.objects.get(pk=2)처럼 filter나 get을 이용해 특정 조건을 만족하는 객체를 구할 수 있다.
하지만 이 두 경우의 경우에 다른 점이 존재하는데 결과값의 type이 서로 다르다.
filter를 이용해 구할 경우 type을 확인해보면 queryset으로 나오고 get으로 구한다면 자신이 구하려고 했던 모델이 type으로 나온다.
자신이 의도했던 모델이였던 경우 모델을 설계할때 지정했던 변수나 함수를 사용가능하지만 queryset은 단순히 database의 queryset이므로 이러한 것들을 사용할 수 없다.


###데이터 비교
데이터를 비교할 때 데이터의 종류가 같지 않으면 비교를 할 수 없다.
예를 들어 Model에 pub_date라는 필드가 있고 이 필드의 타입을 datetime field로 설정한 뒤
이 필드를 datetime.date.today()와 비교 하면 해당 데이터에 오늘 날짜를 가지고 있었다고 하더라도
모델에 있는 pub_time field는 datetime type으로 날짜와 시간을 모두 가지고 있으므로 datetime.date.today()와 데이터 타입이 다르므로
같을 수 없다.
따라서 둘을 비교하면 무조건 다르다는 결과만 출력하므로 서로 같은지 확인하기 위해서는
두 데이터 타입이 같은 상태에서 비교해야 두 데이터가 같은지 비교 가능하다.


###여러개의 데이터를 가지는 자료형비교
여러개의 데이터를 가지고있는 자료형으로 list, tuple, dictionary 등이 있다.
list는 a = [] 의 형태로 []괄호로 이루어져있고 tuple은 b = (2, 3)처럼 ()괄호안에 여러개의 데이터가 담겨있다.
dictionary는 key와 value로 이루어져있는데 c={ 'int':1 } 처럼 {}괄호로 이루어져있고 안에 hash처럼 key와 해당하는 value로 이루어져있어
찾을때 c['int']처럼 key값을 통해 검색을 하면 해당 key에 해당하는 value를 구할 수 있다.


###쟝고 Form 클래스
쟝고에서는 html에서 form을 컨트롤할 필요없이 Formview클래스와 forms.Form클래스를 상속해 쟝고내에서 폼을 만들고 컨트롤 가능하다
템플릿에서 form을 만들어서 그 폼 데이터를 받아서 view에서 처리할 필요없이 view에서 Formview를 상속받고 화면에 보여질 template_name과
성공했을때 보여질 success_url, 그리고 template서 form처리를 안하는 대신 화면에 보여줄 form_class를 입력해주면 폼 처리가 된 template이 화면에 보여진다.
쟝고에서 폼을 만들때는 from django import forms를 해서 forms를 상속한 forms.py를 만들고 forms.Form을 상속한 class를 만든 뒤 그 클래스내에서
forms.IntegerField나 forms.ChoiceField같이 forms 내에 있는 필드를 이용 해 폼 처리를 하고 싶은 내용을 만들고 화면에 보여줄 template에 {{form.as_p}}처리만 해주면
템플릿파일에 forms.py에서 만들었던 form이 처리되어 화면에 출력된다
submit 버튼을 눌러 form을 제출했을 때 어떻게 처리 될지를 컨트롤 하기 위해서는 forms.py에서 forms.Form을 상속받은 class내에 def submitted(self, request): 형태로
submitted 함수를 만들어 내용을 입력해주면 form이 제출되었을 때 어떻게 컨트롤 할지 정할수 있다.
제출된 폼 데이터를 받아 새로운 url로 연결할 때는 reverse를 이용해야 한다.
연결할 url의 url주소는 모르지만 url name을 알고 있으므로 이 url name을 reverse함수를 이용하면 원하는 url로 연결할 수 있다.
reverse('index')처럼 reverse(url주소)로 연결해줘야 제출된 폼이 올바르게 새로운 url로 연결되어 새로운 url화면을 보여줄수 있다.
reverse가 오류가 발생할때가 있는데 이 때는 reverse_lazy(url주소)로 입력해주면 문제가 해결되서 url로 연결된다.
reverse_lazy를 사용하는 경우는 다음과 같은데
1. providing a reversed URL as the url attribute of a generic class-based view
2. providing a reversed URL to a decorator (such as the login_url argument for the django.contrib.auth.decorators.permission_required() decorator).
3. providing a reversed URL as a default value for a parameter in a function’s signature.
여기서는 Formview를 이용하여 Form을 작성했으므로 1번에 해당한다.
Formview는 generic class-based view이므로 여기서는 reverse_lazy를 통해 새로운 url로 연결해야 한다.

html이 아닌 쟝고의 forms를 통해 form을 만들고 컨트롤 할지라도 행동을 취하기 위해서는 template안에 action을 입력해줘야 한다.
action을 제대로 입력해주지 않으면 뒤에 method나 유저로부터 form을 입력받아 data를 처리하는등의 행위도 제대로 동작하지 않는다.
반대로 action을 처리해주면 form내의 submitted를 따로 설정하지 않아도 form으로 입력받은 data가 자동으로 action으로 연결된 url로 전달되고
입력받은 데이터를 가지고 자신이 원하는 처리를 하면 된다.
쟝고에서 만든 폼을 이용해서 데이터를 받은 뒤 사용하기 위해서는 http를 이용해서 하듯이 단순히 request.POST를 이용해서 데이터를 받는것이 아니라
form을 처리 할 클래스로 가져온뒤 cleaned_data를 이용해 데이터를 받아와야 한다.
예를 들어

    def post(self, request):
        form = InputValueForm(request.POST)
        if form.is_valid():
            used_amount = form.cleaned_data['used_amount_field']
            selected_currency = form.cleaned_data['select_currency_field']
    
이와같이 자신이 사용했던 폼을 request해서 class내에 변수로 가져온 뒤 폼의 유효성을 확인하고
폼이 유효하다면 form.cleaned_data['필드변수이름']을 통해 자신이 입력받을 필드의 데이터를 가져올 수 있다.


###다른 클래스에 정의된 내용 이용하기
클래스내에 function이나 variable을 정의해놓고 다른 클래스내에서 가져다가 사용하기 위해서는
자바에서 클래스 객체를 만들고 그 안의 내용을 호출하듯이 파이썬에서도 클래스를 이용해 객체를 만들고 그 안의 내용을 사용해야 한다.
객체를 만들지 않고는 그 클래스 안의 내용을 참조할 수 없다.
예를들어 base라는 class내의 function find를 사용하기 위해서는
    a = base().find()   와 같이 사용해야 한다.
단순히 클래스 내부의 내용을 참조하겠다고 a=base.find()처럼 function call을 하면 base객체가 만들어지지 않았으므로 클래스 내부의 내용을
사용할 수 없다.


###쟝고에서 한글 사용하기
파이썬은 기본적으로 ASCII 인코딩을 사용한다
ASCII로는 한글을 표현할 수 없기 때문에 다른 인코딩 방식을 사용해야 한다.
Linux 환경에서 한글은 utf-8로 인코딩 되있다.
쟝고에서 utf-8로 된 글자를 사용하기 위해서는 해당 문자가 사용되는 파이썬 문서 가장 위에
    # -*- coding: utf-8 -*-  라고
글자를 입력하면 해당 파일이 utf-8로 코딩되있음을 컴퓨터가 인식해 utf-8문자를 사용할 수 있다.

   
###파이썬3에서의 url open과 json load
파이썬3에서는 모듈이나 함수등의 사용등이 바뀌었는데 urlopen도 바뀌었다.
2에서는 해당 url의 자료를 받아오는 urlopen이나 url을 parsing 하는데 사용하는등의 함수가 모두 urllib2 모듈에 존재했는데
파이썬3에서는 세분화되어서 url을 받아오는 urlopen은 urllib.request, urlparse는 urllib.parse등에 나누어서 저장되어있다.
url에서 data를 받아오기 위해서는 urllib.request를 import하고 urllib.request.urlopen()을 통해 자료를 받아올 url에서 자료를 받고
받아온자료를 read()하는것까지는 이전과 같다. 

하지만 이 데이터가 json파일이라면 json을 python에서 사용하기 위해 파이썬2에서는 그냥 json을 import한 뒤 json.loads를 하면 되었지만 
파이썬3에서는 json파일이 str형태이어야 load할 수 있다고 나오는데 urlopen과 read를 통해 받아온 데이터는 byte형태이므로 load가 불가하다.
여기서 load를 하기 위해서는 byte파일을 decoding해서 string으로 바꾸고 load를 하면 되는데 간단히

    recived_data = json.loads(url_str.decode('utf-8'))
처럼 utf-8형식으로 decoding 한다거나 하면 json 파일을 load 할 수 있다. 


###파이썬 goto
파이썬에서는 goto, label이 없다.
실행하는 도중 밑 부분에서 특정 부분으로 다시 돌아갈 수 없다는 말이다.
조건문을 활용해 조건을 잘 설정해서 다시 위로 돌아갈 필요없게 잘 코딩해야 한다.

###try와 예외처리
파이썬에서는 자바에서처럼 try,except를 통해 오류가 날거같은 부분을 실행하고 오류가 발생할때의 예외처리가 가능하다.
try 부분에 문제가 생길것 같은 부분을 코딩하고 except 부분에 문제가 생겼을 때의 처리될 코드를 적는다.
예외가 발생하지 않고 정상적으로 실행될 부분은 else밑에 적으면 된다.
그리고 예외가 발생하던 안하던 상관없이 마지막에 실행될 부분은 finally 밑에 적어 무조건 실행될 부분을 적으면 된다.

###static file
쟝고에서는 파이썬 코드나 html 파일이외에 image 나 css, javascript 등의 파일을 처리하기 위해서 static file을 이용한다.
static file은 쟝고 서버에 해당 파일을 사용한다고 알려준뒤 static 파일을 load 하겠다고 html 내에서 선언하고 사용해야 한다.

    STATIC_ROOT = os.path.join(BASE_DIR,'staticfiles')
    STATIC_URL = '/static/'
    STATICFILES_DIRS = (
        os.path.join(BASE_DIR, 'static'),
    )
위의 형태로 settings.py 에 선언을 하면 settings.py 에 선언해줘야 할 static file 관련 선언은 다 한것이다.
static url은 웹 페이지에서 사용할 static 파일의 최상위 URL 경로이다.
상위 경로 자체는 실제 파일이나 디렉터리가 아니며, URL로만 존재하는 단위이다.
django에서 인식된 static file들은 홈페이지 메인주소/static/ ~하부경로 의 형태로 참조할 수 있다.
http://127.0.0.1:8000/static/img/city-bg.jpg 처럼 url을 입력하면 해당 경로의 static file을 열어볼 수 있다.
STATIC_URL은 정적 파일이 실제 위치한 경로를 참조하며, 이 실제 경로는 STATICFILES_DIRS 설정 항목에 지정된 경로가 아닌 STATIC_ROOT 설정 항목에 지정된 경로이다.
STATIC_ROOT는 Django 프로젝트에서 사용하는 모든 정적 파일을 한 곳에 모아넣는 경로이다. 
한 곳에 모으는 기능은 manage.py 파일의 collectstatic 명령어로 수행한다.(python manage.py collectstatic)
해당 명령어는 각 Django 앱 디렉터리에 있는 static 디렉터리와 STATICFILES_DIRS에 지정된 경로에 있는 모든 파일을 모은다.
주의할 점. STATIC_ROOT 경로는 STATICFILES_DIRS 등록된 경로와 같은 경로가 있어서는 안 된다. 남들이 잘 안 쓸만한 이상한 이름(staticfiles?)을 써야한다.
django project 내의 각 app에서 static file을 이용하기 위해서는 각 app 밑에 static 폴더를 만들어서 static file들을 저장한 뒤
collectstatic 명령어를 통해 해당 static file을 쟝고에 인식시키고

     {% load staticfiles %}
     <script src="{% static "js/jquery-1.11.3.min.js" %}"></script>
     <script src="{% static "js/bootstrap.min.js" %}"></script>             
     <script src="{% static "js/hero-slider-main.js" %}"></script>         
     <script src="{% static "js/jquery.magnific-popup.min.js" %}"></script> 
     
 처럼 html 페이지 내에서 불러서 사용하면 된다.
 
 자세한 내용은 http://blog.hannal.com/2015/04/start_with_django_webframework_06/  참조하면 된다.