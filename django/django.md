
# django TIL

����

������ �������� ������ �������� ����� ����
������ �������� �� ������ ���ؼ� �����ϰ� ������ �������� �� ������ ������ �� ���ø����̼� ������ �̿��� �����Ѵ�

���� �ٸ� �� �����ӿ�ũ��ó�� MVC ������ ����Ѵ�
������ �������� MVC�� view�� templete�̰� Controller�� view�� ���̹Ƿ�
�� �̸��� ���� MTV��� �Ѵ�


�������
���̽��� ��ü�� equal������� �����Ѵ�
���� ��� dictionary ���·� 'drink' = water ���·� �Է��ϰ� water������ ���簪�� hotwater ���µ� icewater�� �����Ų �� dictionary�� ����غ��� 'drink' = icewater���¿� ���� ��µȴ�.

json
json�� �������ӿ��� ���� ���� ���·� string:string �� ���·� key�� �׿��´� value�� ��Ī�Ǿ��ִ� �����̴�.
���� ��� "language" : "python"�� ���·� key �� value�� data�� ������ �ѱ� �� �ִ�.
���̽��� dictionary���°� jsonó�� Ű�� value�� ��Ī�Ǿ� �ִ�.
dictionary�� json���·� ���� �ٲ� �� �ִ�.

json -> dict �� ������ ���� ���� �����ϴ�
import json
json_data = '{"hello": "world", "foo": "bar"}' 
data = json.loads(json_data)

dict -> json �� ������ ����
import json
data = {'baz': 'goo', 'foo': 'bar'}
json_data = json.dumps(data)

dict -> json ���� �ٲ� http���·� response�� ���� �ִ�
import json
from django.http import HttpResponse

def fbview(request):
    data = {'foo': 'bar', 'hello': 'world'}
    return HttpResponse(json.dumps(data), content_type='application/json')

�̰Ŵ� ������ ���� �Ҷ� Ŭ���̾�Ʈ�� data�� ���� ��û�� �Ѵٸ� dictionary���·� �����Ǿ� �ִ� data�� json���·� �ٲ� http���·� response �� �� �� �ִ�.

