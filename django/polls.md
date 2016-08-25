# django TIL
## polls

templete���� python�� ����� ����ϱ� ���ؼ��� { ~ } �� ���
Html������ ������ html���� �ϴ� �� ó�� < ~ >�� �̿��ؼ� ����Ѵ�.
���̽��� py������ �ȿ��� ���̺��� ��ü�� column���� ����ϱ� ���ؼ��� question_idó�� _�� ����Ѵ�
��ü�� �Լ��� ����� ���� question.objects.all()���·� . �� �̿��Ѵ�


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


Admin
������ �������� admin���������� � ȭ���� ���������� admin.py�� �����ϹǷ� ������ �� �ִ�.
� �׸���� �������� ���� ��Ÿ���� field�� �� field���� � ����Ʒ� ���ļ� ��͵��� �������� ���ϴ� fieldset �׸��� ������ ��ü�ܿ� �߰��� � �׸��� �������� ���ϴ� inlines���� [ ] ��ȣ�� �̿��� ������ ���������� ���Ѵ�
ó���� admin���������� ������ db ���̺��� �������� �� �� ���̺��� ��ǥ�׸����� UI ȭ�鿡 � ������� ��Ÿ�������� list_display = ( , )�� ���� ��Ÿ�� �� �ִ�.
list_filter �Ӽ��� �߰��ϸ� UIȭ�鿡 ���� ���̵� �ٸ� ���� �� �ִ�. ex)list_filter = ('pub_date')��� �ϸ� pub_date������ ���� ���̵�ٰ� �����ȴ�.
search_fields = ['~']�� �ش� field�������� �˻��� �� �� �ִ� �˻�â�� ������ش�
� ���� ��ǥ�� ��Ÿ�������� ���ϴ� list_display�� �����ϰ� �������� �� [ ]��ȣ�� ���� ���� �Է��Ѵ�.


Shell
django������ terminal���� python manage.py shell��ɾ ���� ���̽� ���� �����ų �� �ִ�.
���̽� ���� ���� �����͸� �����ϴ°��� �����Ѵ�.
����� 2��(__)�� ����Ͽ� ��ü ���� ���踦 ǥ���� �� �ִ�.
���� ���
current_year = timezone.now().year 
Question.objects.get(Pub_date__year=current_year) ��� �Ѵٸ�
pub_date�� year�� ������ ��� Question objects���� ���� �� �ִ�.


Template
���ø������� ����,����,�±� �� �������� ����� ����� �� �ִ�.
�� �� ���ø� ������ ����ϰų� ���͸� �̿��Ҷ��� {{ ~~ }} ���·� ��ȣ 2�����̿� �Է��Ѵ�.
���ø� �±״� {% tag %}���¸� ������.
���� ����ϴ� �±׷δ� {% for %}, {% if %}���� �ִ�.
if �±״� {% if athlate_list|length > 1 %} ó�� �±� �ȿ� ���Ϳ� �����ڸ� ����� �� �ִ�.
url �±״� {% url 'namespace:view-name' arg1 arg2 %} ���·� ����Ѵ�
namespace�� urls.py���� include�� ���� �Է��ߴ� namespace, view������ ���Ӱ� ������ url�� �ּ� �� - view�������� �Լ� �̸�, arg1 agr2���� ���� ��Ÿ�� url�ּ��� template�� ��Ʈ�� �� view�� �Լ����� ����ϴ� ����(=����)�� ��Ÿ���� 


