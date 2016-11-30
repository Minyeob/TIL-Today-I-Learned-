#웹시스템설계

## Mean stack을 이용한 웹 개발

Mean은 요즘 웹 개발에 이용되는 방법 중 가장 큰 성장세를 보여주고 있는 방법이다.
Mean은
MongoDB의 M,
Express의 E,
angularJS의 A,
NodeJS N의 앞글자를 따서 만든 말이다
이 중 AngularJS와 NodeJS는 javascript 기반으로 만들어졌는데 AngularJS는 프론트엔드 개발, NodeJS는 백엔드 개발에 이용된다.
javascript언어 하나로 프론트,백엔드 모두 개발이 가능하기 때문에 비교적 배우기 쉽다는장점이 있다.
하지만 이 부분은 단점이 될 수도 있는데 쟝고나 레일즈같은 다른 백엔드 개발에 사용되는 언어들은 프론트 엔드로 html이나 css등을 공통으로 사용하기 때문에 백엔드 개발에 이용되는 언어가 바뀌더라도 앞에 프론트엔드 개발을 시켜놓은 부분은 기능만 맞게 구현시키면 바로 사용이 가능하다.
하지만 mean stack은 같은 언어로 개발되있기 때문에 프론트와 백엔드가 서로 연결되어있고 영향을 미칠 수 밖에 없다.


##자바스크립트
자바스크립트는 Prototype-based inheritance mechanism을 가지고 있다
두 개의 객체가 같은 프로토타입 개체를 가진다면 두 객체는 같은 클래스에 있다고 말할 수 있다.

closure는 함수 내부의 함수를 만들어 함수를 만들어 내부의 함수를 동작시켜 외부함수의 변수에 접근하는 함수를 말한다
외부함수내에 변수를 만든 뒤 내부에 그 변수를 사용하는 함수를 만들면 내부함수에는 바로 접근할 수 없고
외부함수를 동작시킬때만 외부함수의 변수를 이용해 동작되는 내부함수가 동작된다.

closure는 다음과 같은 경우에 사용된다.
1. 라이브러리에서 private이나, 나의 변수를 보호하고 싶을 때
2. self-defining function의 경우 static으로 변수를 이용하고 싶을 떄
3. 처음에 초기화 시켰던 값을 계속 유지하고 싶을 때
4. callback 함수에 추가로 데이터를 넘겨주고 싶을 때

외부함수 내의 변수는 내부변수이므로 외부에서 변경하거나 참조할 수 없으며 외부함수를 호출, 내부함수를 동작시킬때만 외부함수의 변수를 출력하거나 변경시키거나 할 수 있다.
그 외부함수의 선언은 우리가 일반적으로 사용하는 형태로 선언되어야만 지속해서 사용할 수 있다.
함수를 통해서 호출하는 경우 함수가 한 번 사용되고 나면 변수를 다시 참조할 수 없는것 같다.
예를 들어
   var img = document.createElement("IMG");
처럼 선언되면 img가 한 번 사용된뒤 재 사용할 수 없다.
create로 변수를 만들었는데 그 create된 변수가 이미 append되어 없어졌으므로 재사용이 안된다는 생각이 든다.

값으로 함수를 입력하기 위해서는 함수만 return 해야한다.
예를 들어 emit라는 함수를 값으로 입력하기 위해서는 emit만 값으로 입력해야하지, emit()로 하면 안된다.
emit()는 emit함수가 실행 된 결과값을 입력하는 것이다.

###반복문
자바스크립트는 다른 언어들처럼 while,for,for in 등의 반복문을 가진다.
while 반복문은 다른 언어와 같은데 파라미터로 들어간 조건이 유효할때까지 계속 반복된다.
while(1)이면 무한반복 되는것이다.
일반적인 for문은 c언어에서 사용하는것과 같이 for(i=0;i<10;i++)처럼 시작조건,완료조건,변화문 의 형태로 구성된다.
for in은 for(i in array)의 형태로 사용된다.

    for(i in array)
    {
        console.log(array[i]
    }
처럼 사용된다.
파이썬이나 자바에서 사용하는것처럼 i 가 array라는 배열의 각 value에 해당하는것이 아니라 array라는 배열의 index 값으로 i가 사용된다.
일반적인 for문과 비슷한데 반복문의 횟수를 정해줄 필요 없이 for 문을 사용하면 된다라고 생각하면 된다.
파이썬이나 자바의 for in 처럼 사용되는것은 array.foreach 가 있다.
    
    docs.forEach(function (doc) {
        print=print+JSON.stringify(doc);
      })
여기서는 docs라는 배열의 각 원소값이 doc이 되어 함수안의 코드를 실행한다.
javascript에서는 for in 보다 for each를 사용하는것이 좋을것 같다.


###배열
자바스크립트에는 배열이 c언어나 자바처럼 일반적으로 만들어서 배열에 대한 주소에 저장하거나 특정 주소에 들어있는
배열값을 가져와 참조할 수 있다.
자바스크립트에서는 배열에 push와 pop도 기본적으로 함수로 들어가있는데 이를 통해 배열을 stack처럼 사용할 수도 있다.
자바스크립트에서는 new Array()처럼 함수를 통해 배열 생성도 가능하고 특이하게 함수의 길이도 생성후에도 바꿀수 있다.
c언어나 java에서는 최초에 배열의 크기를 정하고 만들면 배열의 크기를 변화시킬 수 없는데 여기서는 배열의 길이도 나중에
array.length = 100; 이런식으로 다시 지정해 줄 수 있다.
그리곡 배열에 일반적인 캐릭터나 숫자등은 a[0]=a[1]처럼 내용을 바꿔줄 수 있지만 객체는 단순히 = 로 내용을 바꿀 수 없다.
array에 있는 copy함수를 통해 내용을 복사할 수도 있고 
slice를 통해서도 깊은 복사가 가능하다.
slice 메소드의 매개변수는 숫자를 매개변수로 받고 그 매개변수를 index로 인식하여 해당 index 부터의 값들을 copy하여 array를 새로운 객체로 return한다.
보통은 array.slice(start index, end index)를 이용하여 원하는 array만 얻고자할 때 쓰이는 메소드인데 이를 이용하면 아주 쉽게 깊은 복사(deep copy)를 할 수 있다.

    var arrayOriginal = new Array();
    arrayOriginal.push("a");
    arrayOriginal.push("b");
    arrayOriginal.push("c");
    var arrayClone = arrayOriginal.slice(0);
    arrayOriginal.push("d");
    arrayClone.unshift("d");
    // arrayOriginal => a, b, c, d
    // arrayClone => d, a, b, c

위 코드를 보면 slice(0)을 통해 시작부터 복사해서 배열자체를 그대로 copy해서 arrayclone으로 복사한것을 볼 수 있다.
slice(start index)형태로 end index를 주지 않으면 start index부터 뒤 내용을 전부 잘라서 가져온다.



##Node JS
Node JS에서는 다른 언어들처럼 여러가지 기능을 가지고 있는 라이브러리 패키지를 가지고 있는데 이를 모듈이라고 한다.
node js의 여러가지 모듈들과 패키지를 가진 온라인 저장소를 NPM이라고 하는데 NPM은 저장소의 패키지와 모듈을 설치할 수 있는 명령어를 제공한다.
파이썬의 pip와 비슷한 역활을 하는것 같다.

###이벤트처리
single thread기반의 node js는 event와 callback을 통해 동시성을 지원한다
'events' 모듈의 EventEmitter는 event를 발생시키고 이에 대한 처리 콜백 함수를 정의할 수 있는 오브젝트이다.
EventEmitter를 사용하기 위해서는 events 모듈을 먼저 불러오고 그 뒤 모듈에 있는 EventEmitter 객체를 만들어야 한다.
node js에서는 모듈도 변수로 가져와 그 변수의 하위에 있는 객체를 만들어야 한다.
예를 들어
    
    var events = require("events");
    var EventEmitter = new events.EventEmitter();

처럼 만들어줘야 EventEmitter라는 변수에 events모듈에 있는 EventEmitter 객체가 만들어진다.
그 뒤 이벤트를 생성할 때는 EventEmitter.emit('이벤트이름') 형태로 emit함수를 통해 이벤트를 생성할 수 있다.
그리고 해당 이름으로 만들어진 이벤트를 처리하기 위해서는 on이나 addlistener함수를 통해 이벤트를 처리하는 함수를 연결해줘야 한다.
EventEmitter.on('odd', odd_handler) 처럼 만든다면 'odd'라는 이름의 이벤트의 처리함수로 odd_handler라는 함수를 연결시켜주는것이다.
그 다음 event를 처리하는 odd_handler 함수가 odd_handler() 형태로 파라미터를 받지 않고 이벤트 처리를 한다면 관계없지만
odd_handler(name)처럼 파라미터를 넘겨받는 함수라면 이벤트를 발생시킬 때 파라미터를 넘겨줘야 한다.
emit함수를 쓸 때 변수를 넘겨주기 위해서는 EventEmitter.emit('이벤트이름', name) 처럼 이벤트이름 뒤 콤마로 파라미터를 넘길 수 있다.
이렇게 emit함수를 설정해준다면 함수를 처리하는 함수로 name이라는 변수가 파라미터로 넘어가게 된다.
그러면 이벤트를 처리해주는 함수에서는 이 파라미터를 이용해 사용할 수 있다.

각 함수는 자신에게 입력되있는 return값만 return할 뿐, 내부에 함수가 또 구현되있더라도 내부에서 그 함수를 실행하지 않으면 내부함수에
적힌 return값은 return 하지 않는다.
함수를 선언한뒤 this.~로 하지 않고 그냥 내부함수로 만들면 큰 함수 내부에서 내부함수는 사용할 수 있지만 외부에서는
함수에 대해 객체를 만들어도 사용할 수 없다. 큰 함수 내부에서 변수를 조작하는데 사용될 뿐이다.
반면에 큰 함수 내부에서 

    function calc(){
        var num=0;
        this.plus = function { num=num+1;}
    }

이렇게 this.plus 처럼 this.~ 꼴로 정의하면 외부에서도 객체를 만들어서 해당함수에 직접 접근할 수있다.
예를 들어

    var a = new calc;
    a.plus;
    console.log(a.num);
    
처럼 입력하면 function calc 안에 plus에 정의했던 함수가 동작해 num이 +1되어 콘솔에도 1이 출력된다.
this.~ 꼴은 객체를 통해 외부에서 내부의 값을 변경시킬 수 있을 뿐 아니라 내부 함수 내에 return을 설정해놓았다면
외부에서 해당 내부함수의 return값까지 바로 받아서 사용할 수 있다.
이렇게 되면 객체를 만들고 그 객체에 대해 함수를 사용하고 변수를 사용할 수 있으므로 자바에서 클래스의 객체를 만들어
객체마다 연산을 하고 값을 이용하는 것과 비슷하다. 큰 함수가 하나의 클래스가 되고 그 함수의 객체를 만들어 사용할 수 있는것이다.
객체를 여러개 만들어 연산을 하면 각 객체마다 다른 값을 가지고 각각 따로 사용된다.
this를 이용하지 않고도 내부에 함수를 만들어 객체를 만든 뒤 사용하기 위해서는 return으로 a:b처럼 key:value의 관계를 return할 때
b로 function을 사용하면 큰 함수를 실행하면 객체가 생성되는데 그 객체에서 함수로 사용이 가능하다.
b에 변수를 설정하면 해당 변수에 대한 사용도 객체를 통해 역시 가능하다.
대신 함수의 return 값으로 그 밑의 함수를 return하는것과 마찬가지라서 기존 큰 함수에서 정의되었던 변수나 this.~ 꼴의 함수들은
함수의 return값으로 나온 객체에서 직접 사용할 수 없고 그 객체에서는 return값에 설정되있는 함수나 변수만 사용가능해서 return에 있는
함수들이 큰 함수내의 함수를 실행하거나 변수를 return하는 형식으로 기존 입력값을 이용해야 한다.

이런식으로 구현하거나 특정 이벤트나 동작마다 내부함수가 동작하여 외부함수의 변수를 변경시키거나 return할 수 있게해서
외부함수의 내부변수를 직접 변경하거나 가져다가 사용할 수는 없지만 외부함수 내부의 내부함수를 통해 변수를 사용하고 변경하고 return할 수 있게
만들면 그 내부변수는 직접 조작할 수 없고 내부함수에 의해서만 참조되고 변경되므로 보호가 가능하다.
이런식으로 구현된 함수를 closure를 사용한 함수라고 할 수 있다.


###서버,클라이언트 통신
node.js에서는 모듈을 통해 직접 서버를 열고 클라이언트도 연결시켜 서로 통신이 가능하게 만들 수 있다.
간단하게 http 모듈이나 net 모듈을 require해서 서버와 클라이언트 구축이 가능하다.
서버쪽에서는 create server를 통해 server를 만들고 파라미터로 클라이언트가 연결되었을때의 반응하는 함수를 구현한다.
파라미터로 들어간 함수의 내용은 client가 connect 되었을 때 자동으로 실행된다.
    
    var server = net.createServer(function (client) {
    var id='client'+number;
    client.write('Welcome! You are '+id);
    console.log('client'+ number+ ' is connected');
    client.id=id;
    socketlist[number] = client;
    number++;
처럼 코드를 짜면 client가 연결되었을때 함수에 적힌 내용들이 자동으로 실행되게 된다.
위의 내용은 server쪽의 내용이고 client쪽도 connect 함수를 통해 연결하면 함수에 기록한 내용들이 기본적으로 실행된다.

    var client = net.connect({port:8080, host:'localhost'}, function (data){
    console.log('client is connected to '+ client.remoteAddress+ ':'+ client.remotePort);
    });
처럼 만들면 해당 port와 host를 통해 server에 연결되고 함수에 적힌 console.log를 실행하게 된다.
클라이언트를 서버에 연결시키면 connect를 준 옆에 변수가 생성이되고 서버쪽에도 server를 만들고 그에 대한 return으로
입력한 함수의 파라미터로 입력해놓은 객체가 생성이 된다.
위에 코드처럼 되있으면 server에 client variable이 생성되고 서버쪽에도 함수의 파라미터인 client 객체가 만들어진다.
서로 다른 객체가 되므로 각 client를 구별 가능하다.
서버쪽에 client를 받아 connect 될 때 구현되는 부분에 변수를 설정한다면 해당 변수들은 각각의 socket 객체마다 변수를 가지므로
각 객체마다 구분되게 사용이 가능하다.
예를 들어 위에서는 client가 연결될 때 서버에서 생성되는 client 객체는 var id를 가지는데 이 id 변수는 연결이 되는 client마다
만들어진 객체들을 통해 연결이 가능하고 여기서 server와 client를 연결하고 있는 각각 생성된 client들을 socket이라고 한다.
이 socket을 이용해 event를 발생시키고 그에 대한 처리를 하면서 통신을 하는것이다.
예를 들어 client.write를 통해 client쪽 socket에서 data를 보내면 server는 해당 data를 받고
서버쪽에서 client.on('data', ~) 를 통해 client.write로 보낸 data를 'data' 이벤트로 받아 처리를 한다.
소켓의 이벤트는 8개 정도가 있는데
https://nodejs.org/dist/latest-v4.x/docs/api/net.html#net_class_net_socket 의 공식문서를 통해 확인하면 된다.
client를 여러개 만들어 각각 server에 연결시키면 서버에서는 각 소켓에 대한 서버쪽 소켓이 생기고 위의 코드대로면
각 client에서 연결할 때마다 각각의 client 객체를 서버에서도 만든다.
socket을 통해서는 각 server와 client가 1:1로 연결을 하며 클라이언트 소켓에서 다른 클라이언트나 서버쪽에서 여러 클라이언트로
통신을 하기 위해서는 클라이언트가 연결할 때 서버쪽에서 생성되는 소켓을 배열이나 리스트 등에 저장해놓고 server쪽에서
각 클라이언트에 통신을 해줘야 한다.
client -> server -> 다른 client 형태로 서버를 통해 여러 client와 동시에 통신이 가능하다.

    
###키보드 입력값 받기
키보드 입력에 대한 내용도 이벤트로 받아 처리가 가능하다.

    process.stdin.on('data', function (chunk) {
    if(chunk.toString()=='/exit\n'){
        client.write('exit');
        console.log('Socket connection is disconnected');
        client.end();
    }

    else
    {
        client.write(chunk.toString());
    }
    });

위 처럼 키보드를 입력하면 process.stdin에 'data'이벤트를 발생하고 이에 대한 이벤트를 받아 처리 하면 키보드로 받은 값을 활용할 수 있다.
코드를 보면 chunk가 있는데 키보드로 입력받은 내용은 chunk로 저장되고 chunk.tostring()을 통해 입력받은 값을 문자열 형태로 저장해
활용하거나 출력할 수 있다.
다른 언어에 scan한 내용을 변수에 저장하는것처럼 node에서도 키보드로 입력하면 process.stdin의 data 이벤트를 발생시키고
그 이벤트에서 chunk라는 변수에 입력한 내용이 저장한다고 생각하면 된다.


###폼처리
폼 method를 get으로 주면 그걸 처리하는 컨트롤러 쪽에서는 query라는 이름으로 참조하고 post로 보내면 body라는 방식으로 참조한다.
for(method='GET', action='')안에 input(id='test', name='ttt)라고 하면 그걸 처리하기 위해서는 app.query.ttt 형식으로
qpp.method에 해당하는 처리 방법,input name 의 형식으로 받을 수 있다.
javascript에서는 form에 입력된 값을 받아 올 때 name으로 각 값을 구별한다.
name이 제출 되는 값들의 key값의 역활을 한다.
input이 어떤 폼 아래에 기록되어 action과 method를 확인해 어디로 가고 어떻게 보내지는지 확인해야 하고
각 input 값들이 어떤 name을 가지고 있어 그 값을 어떻게 받아와야 할지 확인하는것은 중요하다
input이 비어있을 때 작성버튼을 누르면 제출되지 않고 해당 칸을 작성하라고 알려주기 위해서는 옵션으로 required를 써주면 된다.
예를 들어 input에 action과 method를 줄 때 그 옆에 required를 같이 써주면 해당 칸이 비어있는 상태로 제출을 시도하면 alert를 해준다.


###jade
jade는 javascript에서 사용하는 view 표현 방법 중 하나이다.
모든 값들은 TAB으로 구별되고 괄호같은건 사용하지 않는다.
앞의 값의 탭한 뒤 값이 해당 값의 value가 되어 사용된다.
예를 들어 h1    kim 이라고 하면 html의 <h1>kim</h1>과 같다. 괄호 대신 TAB으로 구별하는 것이다.
엔터 후에 밑 줄의 값도 TAB을 이용해 명령어의 뒤에 있다면 위의 명령어를 받는다

     div#userinput
        form(action='/remove', method='post')
            p
                input#input_1(type='text', name='input_1', placeholder="지우거나 바꾸고 싶은 텍스트를 입력하세요" )
            p
                input#input_2(type="text" placeholder="바꿀 텍스트를 입력하세요" name="input_2")
            br
            textarea(id="text_space" placeholder="전체 텍스트를 입력하세요" name='text_space')
            p
                input#submit(type='submit' value='Submit')
                
위 처럼 되어 있으면 userinput이라는 div 밑에 밑에 내용들이 포함되어 있고 각 p 밑에 밑줄의 내용들이 >p> 내용 </p> 형태로 포함되어 있다.
그리고 input#input_1 처럼 값에 대한 클래스를 <h1 class=''> 처럼 글로 쓸 필요없이 #을 통해 바로 주거나 id도 .을 통해 p.name 의 형태로 바로 줄 수 있다.

자바스크립트에서 넘겨준 변수를 사용하기 위해서는 jade에서 p=variable 처럼 html 태그에 그 태그안에 입력될 내용을 가진 변수를 입력하면 된다.
위의 경우 <p>variable의 값</p> 의 html 내용과 같은 내용이 된다.
그리고 일반 text를 입력하다가 변수의 내용을 중간에 넣기 위해서는 p    안녕하세요 #{variable}처럼 #{}안에 변수를 입력해주면 해당내용이 출력된다.
그리고 html 태그가 포함된 값을 html에서 사용하는것 처럼 내용만 가져다가 사용하기 위해서는 !=을 이용하면 된다.
jade에서 html태그가 포함된 html내용을 가져다 사용하기 위해 != 을 이용하는데 !=을 이용하면 <>태그들이 text가 되지 않고 해당 html 태그에 맞게 사용된다.


###문자열
javascript에서는 문자열 처리를 String object에 대해 지원하는 여러가지 함수를 통해 처리할 수 있다.
그 중 많은 수의 함수들은 인자(parameter)로 Regexp를 받는데 Regexp는 정규표현식이다.
js에서는 new Regexp(문자열, attribute)의 형태로 정규표현식을 만들 수 있는데 문자열은 정규표현식으로 바꿀 문자열, 뒤의 attribute는
해당 정규표현식이 전역에 걸쳐 영향을 미칠지, 대,소문자를 구별할 지 않을지, 여러 줄 매치 등을 의미하는데 많이 사용할 수 있는 전역 선언은 'g'를 이용해 선언한다.
str.replace(new Regexp('abcd', 'g'),'')의 형태로 문자열 함수가 사용될 때 정규식이 정규식이 사용되는 대상의 전역에서 사용된다는 의미로
여기서는 str 문자열 전체에 정규표현식이 replace의 상대로 사용된다는 의미이다.


###jquery
jQuery(제이쿼리)는 브라우저 호환성이 있는 HTML 속 자바스크립트 라이브러리이며 클라이언트 사이드 스크립트 언어를 단순화 할 수 있도록 설계되었다
사용자에게 보이는 화면에서 발생하는 입력이나 이벤트에 대해 javascript를 이용해 처리할 수 있도록 html 안에서 작성해줄 수 있다.
jade안에서 사용하기 위해서는 body 안에서 script. 을 적고 그 안에 코드를 작성해서 사용할 수 있다.
명심해야 할점은 script 뒤에 .이 꼭 붙어야 한다.


###AWS에서 node 동작시키기
aws 계정과 인스턴스를 만들고 해당 인스턴스에 접속이 가능하다면 위에 node로 코딩해서 웹 서버를 만들 수 있다.
sudo apt-get install nodejs를 통해 node를 설치하면 노드가 사용 가능하고 똑같이 install 명령어로 npm을 설치한다면 마찬가지로 npm이 사용가능하다.
http 서버를 만들어 사용할 것이 아니라 express를 이용하려면 express도 설치해야 한다.
express는 npm을 통해 설치가 가능하므로  sudo npm install -g express 명령어를 통해 설치할 수 있다.
express를 설치했다면 express -e 명령어로 기본 express 프로젝트를 시작할 수 있다.
그리고 sudo npm install 을 입력한다면 기본적으로 package.json 에 입력되어있는 node module 파일들을 설치해
node 프로젝트를 시작할 수 있도록 한다.
그리고 사용하기 위해서는 app.js 로 들어가 app.set을 통해 http server나 port를 연결해 외부에서 접속이 가능하도록 해야한다.
그리고 project 폴더로 들어가 npm start를 실행하면 node 를 실행해 브라우저를 통해 접속이 가능하다.
컴퓨터를 켜놓지 않고도 aws에서 항상 해당 node project가 실행되기 위해서는
nohup npm start 명령어로 nohup 을 포함해서 실행하면 aws 내에서 항상 백그라운드로 node가 실행되
컴퓨터를 켜지 않아도 해당 ip에 대해 접속이 가능하다.


###Session
node js에서 session은 'express-session' 모듈을 load함으로써 다룰 수 있다.
session을 만들기 위해서는 반드시

    app.use(session({
      secret: 'keyboard cat',
      cookie: {
        maxAge: 1000 * 60 * 60 * 24 * 7
      },
      store: store,
      resave: false,
      saveUninitialized: true
    }));
    
처럼 session에 secret값을 넣어줘야 한다. store는 저장될 공간이고 resave는 session이 modify 되지 않아도 다시 저장한다는 의미이고
saveUninitialized 는 session이 만들어진뒤, modify되지 않아도 자동으로 저장된다는 의미이다. 
이런건 모두 optional 하지만 secret은 session id를 암호화하는데 사용한다. secret에는 문장 또는 문장으로 이루어진 배열을 사용하는데
이 문장이 해쉬 함수를 통해 암호화되어 id가 되고 해당 id를 해쉬 함수를 통해 다시 해석했을때 해당 secret과 같다면 같은 session임을 알 수 있다.
위의 설정은 반드시 routing 설정을 하기 전에 해줘야 한다. 즉 app.js 에서 해당 주소에 대한 control을 하기 전에 반드시 미리 처리를 해야 session에 대해 사용할 수 있다.
session은 json object로 되어 있다.



###JSON
JSON 형태의 데이터는 JSON.stringify(json data)의 형태로 문자열로 바꿀 수 있다.
data 라는 이름의 json object가 있다고 하면 JSON.stringify(data)를 통해 json object를 json 문자열로 바꾸는것이다.
json 문자열은 파이썬의 dictionary형태와 같다고 보면 된다.
json의 원하는 키에 대해서만 변환시키기 위해서는 stringify의 두 번째 파라미터인 replacer 함수를 사용해 원하는 옵션을 줘서 바꿀수도 있다.

    function replacer(key, value) {
      if (typeof value === "string") {
        return undefined;
      }
      return value;
    }
    
    var foo = {foundation: "Mozilla", model: "box", week: 45, transport: "car", month: 7};
    var jsonString = JSON.stringify(foo, replacer);    
처럼 한다면 jsonString의 값으로는 {"week":45,"month":7} 가 된다.
replace함수에서 value가 string type이면 undefined를 return 하도록 했고 undefined를 return 하면 null 값이 되어 변환되지 않는다.

    JSON.stringify(foo, ['week', 'month']);  
    // '{"week":45,"month":7}', only keep "week" and "month" properties
처럼 배열을 이용해 원하는 key값만 간단히 문자열화 시킬 수도 있다.
위처럼 하면 foo라는 json 파일에서 week라는 key값과 month라는 key의 key와 value만 문자열화 된다.

JSON.parse 를 이용하면 json 문자열을 다시 object로 만들 수 있다.
Json object에서 자신이 찾는 key에 대한 value를 구하기 위해서는 json object.key 값의 형태로 foo.foundation 처럼 사용하면 foo 라는 json object의
foundation key값에 해당하는 value를 구할 수 있다.
문자열로 변환시키면 원하는 값에 대해 찾을 수 없고 오브젝트 상태일때만 원하는 key값에 대한 정보만을 찾을 수 있다.
console.log로 console창에는 object의 값도 볼 수 있지만 html에는 object의 값은 나타낼 수 없고 문자열로 바꿔서 출력해줘야 한다.


###Assert
Assert는 유닛 테스트를 위해서 Node.js에서 사용할 수 있는 테스트 모듈이다. 별도의 설치없이도 import하면 바로 사용할 수 있다.
var assert = require('assert'); 처럼 import 해서 assertion을 이용하면 된다.
assert()는 인자로 넘어온 값이 true랑 같은 지 비교한 후, 같지 않으면 에러를 발생시킨다.
assert.ok()는 assert()와 똑같이 사용된다.
assert.iferror는 반대로 인자로 넘어온 값이 false랑 같은 지 비교 후, 넘어온 값이 true 라면 error를 발생시킨다.
equal()과 notEqual()은 인자를 두 개 넘겨서 비교할 수 있는 메소드이다.
assert.equal(a,b) , assert.notequal(a,b) 처럼 사용되는데 equal은 a==b를 해서 a와 b가 같은지 비교 해, 같지 않으면 에러를 발생시킨다.
notequal은 a!=b 를 해서 같지 않은 지 비교해, 같다면 에러를 발생시킨다.
==나 != 를 이용해 비교하므로 강제형변환을 사용하므로 정확한 결과가 나오지 않을 수도 있다.
strictEqual()과 notStrictEqual()은 Identity 연산자로 비교한다.
equal()이나 notequal()이랑 사용방법은 똑같이 assert.strictequal(a,b) 나 assert.strictnotequal(a,b)를 사용하는데
=== 나 !== 을 이용하므로 조금 더 명확한 비교가 가능하다.


###==와 ===의 차이
그동안 다른 언어에서 비교를 할 때 ==를 사용했다.
javascript에서도 마찬가지로 ==를 사용하는데 javascript에서 ==를 사용하면 연산이 되기 전에 피연산자들을 먼저 비교할 수 있는 형태로 변환시키고 비교한다.
    
    254 == '254'                // return true
    true == 1                   // return true
    undefined == null           // return true
    'abc' == new String('abc')  // return true
    null == false               // return false
    'true' == true              // return false
    true == 2                   // return false
따라서 다음과 같은 결과를 출력한다.
true가 나와서는 안되는 값들도 true가 나오는것이다. 정확한 비교가 안 될때도 있다.
하지만 ===와 !==는 Identity 연산자이다. 이 녀석은 ==와는 반대로 형변환을 하지 않고 연산한다.

    254 === '254'               // return false
    true === 1                  // return false
    undefined === null          // return false
    'abc' === new String('abc') // return false
따라서 다음과 같은 결과를 출력한다.
javascript에서 좀 더 정확한 비교를 하기 위해서는 ===나 !==를 사용하는것이 좋겠다.


###MongoDB
MongoDB는 no sql database로 node js 에서 데이터베이스로 가장 일반적으로 사용된다.
각 데이터에 대해 key:value 의 json 형태로 document로 db에 저장된다.
document 는 여러 데이터를 저장한 일종의 하나의 tuple 이라고 보면 된다.
$in 을 이용하면 앞의 key 값의 value로 [] array 안에 포함된 어떠한 값이라도 매칭되는 document를 find 한다

    db.bios.find(
       {
          _id: { $in: [ 5,  ObjectId("507c35dd8fada716c89d0013") ] }
       }
    )
예를 들어 위 같은 코드가 있으면 db의 bios라는 collection 에서 _id가 5이거나 위의 object id 인 모든 document를 찾는다.