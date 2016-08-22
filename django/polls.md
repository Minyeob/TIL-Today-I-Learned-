# django TIL
## polls

templete에서 python의 기능을 사용하기 위해서는 { ~ } 를 사용
Html문법은 기존에 html에서 하던 것 처럼 < ~ >를 이용해서 기록한다.
파이썬의 py페이지 안에서 테이블내의 개체의 column값을 사용하기 위해서는 question_id처럼 _로 사용한다
객체의 함수를 사용할 때만 question.objects.all()형태로 . 을 이용한다


Primary key
primary key는 테이블에서 각 colummn들을 구별할 수 있는 값을 말한다
생성을 특별히 지정하지 않고 model을 만들게 되면 autoincrement되는 integer로 만들어져 자동으로 1씩 증가하는 정수 id가 되어 각 colummn들을 구별할 수 있게 된다.
하지만 정수가 아니더라도 같은 값을 가질 수 없는 값이라면 primary key로 사용할 수 잇다.
에를 들어 github의 ssh key처럼 임의로 생성된 string일 경우 같은 값을 가질 수 없으므로 string값이라도 primary key로 사용할 수 있다.


Redirect
특정 templete에서 view에 있는 해당 templete에 대한 함수에 기록된 내용 중 render를 통해 특정 url을 호출하고 그 url에서는 그 url에 해당되는 templete을 보여주지 않고 바로 다른 templete으로  httpredirect를 할 때 새로 나타내야 할 url의 값을 알 수 없다
이 경우에 reverse() 함수를 통해 redirect할 url의 주소값을 얻을 수 있다
예를 들어 
	HTTPResponseRedirect(reverse('polls:results', args=(p.id,)))을 return하면
reverse함수가 polls:results와 p.id에 해당하는 숫자의 url을 추출해
/polls/p.id에 해당하는 숫자/results url을 return하고
HttpResponseRedirect는 해당 url에 대해 HttpRedirect를 return해 해당 url에 해당하는 페이지로 연결시켜 준다.

request.POST
request.POST는 제출된 폼의 데이터를 담고 있는 객체로서, 파이썬 사전처럼 키로 그 값을 구할 수 있다.
예를 들어 request.POST['choice']는 제출된 폼의 객체에서 choice값을 추출해 키로 사용해 해당 choice값에 해당하는 choice.id를 스트링으로 리턴한다.


Admin
관리지 페이지인 admin페이지에서 어떤 화면이 보여질지는 admin.py를 변경하므로 결정할 수 있다.
어떤 항목들이 보여지는 지를 나타내는 field나 그 field들이 어떤 제목아래 뭉쳐서 어떤것들이 보여질지 정하는 fieldset 그리고 선택한 객체외에 추가로 어떤 항목이 보여질지 정하는 inlines등은 [ ] 괄호를 이용해 무엇이 보여질지를 정한다
처음에 admin페이지에서 관리할 db 테이블을 선택했을 때 그 테이블의 대표항목으로 UI 화면에 어떤 내용들이 나타내질지는 list_display = ( , )를 통해 나타낼 수 있다.
list_filter 속성을 추가하면 UI화면에 필터 사이드 바를 붙일 수 있다. ex)list_filter = ('pub_date')라고 하면 pub_date기준의 필터 사이드바가 생성된다.
search_fields = ['~']는 해당 field기준으로 검색을 할 수 있는 검색창을 만들어준다
어떤 값이 대표로 나타내질지를 정하는 list_display를 제외하고 나머지는 다 [ ]괄호를 통해 값을 입력한다.


Shell
django에서는 terminal에서 python manage.py shell명령어를 통해 파이썬 쉘을 실행시킬 수 있다.
파이썬 쉘을 통해 데이터를 관리하는것이 가능한다.
언더바 2개(__)를 사용하여 객체 간의 관계를 표현할 수 있다.
예를 들어
current_year = timezone.now().year 
Question.objects.get(Pub_date__year=current_year) 라고 한다면
pub_date의 year가 올해인 모든 Question objects들을 구할 수 있다.


Template
템플릿에서는 변수,필터,태그 등 여러가지 기능을 사용할 수 있다.
그 중 템플릿 변수를 사용하거나 필터를 이용할때는 {{ ~~ }} 형태로 괄호 2개사이에 입력한다.
템플릿 태그는 {% tag %}형태를 가진다.
많이 사용하는 태그로는 {% for %}, {% if %}등이 있다.
if 태그는 {% if athlate_list|length > 1 %} 처럼 태그 안에 필터와 연산자를 사용할 수 있다.
url 태그는 {% url 'namespace:view-name' arg1 arg2 %} 형태로 사용한다
namespace는 urls.py에서 include를 통해 입력했던 namespace, view네임은 새롭게 연결할 url의 주소 값 - view내에서의 함수 이름, arg1 agr2등은 새로 나타낼 url주소의 template을 컨트롤 할 view의 함수에서 사용하는 인자(=변수)를 나타낸다 


