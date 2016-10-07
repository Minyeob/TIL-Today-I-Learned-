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
for in은 파이썬이나 자바에서 쓰는것처럼 for object in list 의 형태로 특정 배열이나 리스트등에 있는
객체를 순서대로 모두 반복한다.

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
