# django TIL
## polls

templete���� python�� ����� ����ϱ� ���ؼ��� { ~ } �� ���
Html������ ������ html���� �ϴ� �� ó�� < ~ >�� �̿��ؼ� ����Ѵ�.


Primary key
primary key�� ���̺��� �� colummn���� ������ �� �ִ� ���� ���Ѵ�
������ Ư���� �������� �ʰ� model�� ����� �Ǹ� autoincrement�Ǵ� integer�� ������� �ڵ����� 1�� �����ϴ� ���� id�� �Ǿ� �� colummn���� ������ �� �ְ� �ȴ�.
������ ������ �ƴϴ��� ���� ���� ���� �� ���� ���̶�� primary key�� ����� �� �մ�.
���� ��� github�� ssh keyó�� ���Ƿ� ������ string�� ��� ���� ���� ���� �� �����Ƿ� string���̶� primary key�� ����� �� �ִ�.


Redirect
Ư�� templete���� view�� �ִ� �ش� templete�� ���� �Լ��� ��ϵ� ���� �� render�� ���� Ư�� url�� ȣ���ϰ� �� url������ �� url�� �ش�Ǵ� templete�� �������� �ʰ� �ٷ� �ٸ� templete����  httpredirect�� �� �� ���� ��Ÿ���� �� url�� ���� �� �� ����
�� ��쿡 reverse() �Լ��� ���� redirect�� url�� �ּҰ��� ���� �� �ִ�
���� ��� 
	HTTPResponseRedirect(reverse('polls:results', args=(p.id,)))�� return�ϸ�
reverse�Լ��� polls:results�� p.id�� �ش��ϴ� ������ url�� ������
/polls/p.id�� �ش��ϴ� ����/results url�� return�ϰ�
HttpResponseRedirect�� �ش� url�� ���� HttpRedirect�� return�� �ش� url�� �ش��ϴ� �������� ������� �ش�.

request.POST
request.POST�� ����� ���� �����͸� ��� �ִ� ��ü�μ�, ���̽� ����ó�� Ű�� �� ���� ���� �� �ִ�.
���� ��� request.POST['choice']�� ����� ���� ��ü���� choice���� ������ Ű�� ����� �ش� choice���� �ش��ϴ� choice.id�� ��Ʈ������ �����Ѵ�.
