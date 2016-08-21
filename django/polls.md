# django TIL
## polls

templete에서 python의 기능을 사용하기 위해서는 { ~ } 를 사용
Html문법은 기존에 html에서 하던 것 처럼 < ~ >를 이용해서 기록한다.


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
