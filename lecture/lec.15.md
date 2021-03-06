# [MIT - Introduction to Computer Science and Programming in Python](https://www.inflearn.com/course/mit-%EA%B3%B5%EA%B0%9C%EA%B0%95%EC%A2%8C-python/)
##  점
평면의 기하학을 하는 면위의 점을 코드로 간단히 짜고 싶다.  
점은 평면에서 x좌표와 y좌표를 갖는다.

e.g.1) 좌표
```
p1 =[1,2]
(x좌표가 1, y좌표가 2인 점 p1이라고 읽는다.)

평면에서 점을 나타낼수 있는 또 다른 방법,  **극좌표의 형태**
p2 =[2,π/2]
데카르트의 좌표 (=반지름을 갖고 x축에서 각을 잡는 것)
```
여기서 문제,  
단순 리스트만을 사용해서 두 점을 붙였다.  
이 리스트들 중 하나를 여러분에 건네 준다고 가정했을 때,  
그것이 데카르트의 형태인지, 평면의 형태인지 어떻게 알죠?  

e.g.2) 첫 번째 점과 두 번째 점을 함께 더한 세 번째 점을 출력한 코드
```
>>> import math
>>> def addPoints(p1,p2):
...     r = []
...     r.append(p1[0]+p2[0])
...     r.append(p1[1]+p2[1])
...     return r
...
>>> p = [1,2]
>>> q = [3,1]
>>> r = addPoints(p,q)
>>> print(r)
[4, 3]
```
문제 발견 : 반지름과 각도로 구성된 데카르트 좌표였다고 가정하면, 새로 출력되는 r점의 좌표는 틀리다.    

이러한 문제에 대해서 추상 데이터 타입을 만들고 객체가 무엇인지 기본적으로 알고 싶다.  
그리고 어떤 함수들이 실제로 그것에 속하는지 알고 싶다.  
그래서 클래스로 돌아와서 생각해보도록 하자.
#### 클래스
클래스는 객체의 인스턴스들을 만드는 템플릿이다.

e.g.3)
```
>>> class cartesainPoint:
...     pass
```
**pass**  
함수의 body부분이 비었다고 말하는 파이썬의 방법이다.

e.g.4)
```
>>> class cartesainPoint:
...     pass
>>> cp1 = cartesainPoint()
>>> cp2 = cartesainPoint()
>>> cp1.x = 1.0
>>> cp1.y = 2.0
>>> cp2.x = 1.0
>>> cp2.y = 3.0
```
cp1과 cp2라는 두 가지 인스턴스를 만든다.  

클래스 정의를 호출할 때, 그 인스턴스와 일치하는 메모리의 구체적인 장소를 할당한다.
그것에 이름을 줄 수 있고 그래서 cp1과 cp2는 모두 그것을 가리킨다.
그것을 가지면, 그 변수에 이름을 주는 것을 시작할 수 있다.
다시 말하면, 어떤 속성들을 줄 수 있다.

그래서 각 인스턴스는 어떤 내부적인 것을 가질 것이다.
cp1은 하나의 인스턴스를 가리킨다. 이 클래스의 특정한 버전을 가리킨다고 할 수 있다.

클래스의 정의를 부를 때, 그것은 가 버리고 메모리에서 다른 장소를 찾는다. 즉, 돌아갈 주소의 포인터값을 여러분에게 주고 그것에 이름을 cp2를 줍니다.  
e.g.5)
```
>>> class cartesainPoint:
...     pass
...
>>> cp1 = cartesainPoint()
>>> cp2 = cartesainPoint()
>>> cp1.x = 1.0
>>> cp1.y = 2.0
>>> cp2.x = 1.0
>>> cp2.y = 3.0
>>>
>>> def samePoint(p1,p2):
...     return (p1.x == p2.x) and (p1.y ==p2.y)
...
>>> def printPoint(p):
...     print("{" + str(p.x) + ',' + str(p,y) +'}')
>>> cp1
<__main__.cartesainPoint object at 0x7f3f7a1d39e8>
>>> cp1.x
1.0
>>> p1 = cartesainPoint()
>>> p1.x = 3
>>> p1.y = 4
>>> p2 = cartesainPoint()
>>> p2.x = 3
>>> p2.y =4
>>> samePoint(p1,p2)
True
>>> p1 is p2  #파이썬의 비교기
False
```
이 경우에, 얕은 동일성과 깊은 동일성을 구별하고 싶다.

#### 얕은 동일성
두 번째 예시("p1 is p2")

주어진 두 점이 정확히 같은 지시대상을 가리키고 있는 지 묻는 코드이다.
클래스 정의를 호출 했을 때 그것이 인스턴스를 만든다고 말했었다. 그것은 메모리의 어떤 장소의 포인터인데 그 주위의 어떤 지역적인 정보를 갖는다.
이 두 점들이 정확히 메모리에서 같은 곳,즉 같은 인스턴스를 가리키는 지를 묻는다.

#### 깊은 동일성
포인터의 경우에 있어서 동일성을 원한다.  
e.g.6)
```
>>> p1 = p2
>>> p1 is p2
True
```
답은 TRUE이다. 왜냐하면 지금 저 두 점들은 메모리에서 정확히 같은 곳을 가리키고 있기 때문이다.

### 데카르트 점
e.g.7) 데카르트의 점을 가지고 있고 이 점들로 polar 점 만들기
```
>>> import math
>>> class polarPoint():
...     pass
...
>>> pp1 = polarPoint()
>>> pp2 = polarPoint()
>>> pp1.radius = 1.0
>>> pp1.angle = 0
>>> pp2.radius = 2.0
>>> pp2.angle = math.pi /4.0
>>>
>>> class cPoint:
...     def __init__(self,x,y):
...             self.x= x
...             self.y =y
...
>>> pp1 is pp2
False
>>> samePoint(pp1,pp2)
Traceback (most recent call last):
  File "<stdin>", __line 1, in <module>
  File "<stdin>", line 2, in samePoint
AttributeError: 'polarPoint' object has no attribute 'x'
```
x와 y값을 비교하기를 원했지만 에러가 났다. 왜냐하면 반지름과 각도를 다루는 메소드를 가지고 않고 있기 때문이다.    
여기서 해결방법은 polar 버전의 점들을 비교하기 위한 다른 함수와 같이 같은 점을 위한 또 다른 함수를 쓰는 것이다.  
하지만 여기서 정작 하고 싶은 것은 여러 정보를 생산해 내는 다른 방법들을 지원하는 점의 표현을 갖는 것이다. 그리고 그것이 같은 점인지 아닌 지를 다루기 위한 메소드 또는 함수인 것이다.  
지금 이 아이디어를 클래스에 적용해보고 일반화해보자.  
e.g.8)
```
>>> class Cpoint:
...     def __init(self,x,y):
...             self.x = x
...             self.y = y
...             self.radius = math.sqrt(self.x*self.x + self.y+self.y)
...             self.angle = math.atan2(self.y,self.x)
...     def cartesain(self):
...             return (self.x, self.y)
...     def polar(self):
...             return (self.radius, self.angle)
...     def __str__(self): # 값을 str로 전환
...             return "(" + str(self.x) + "," + str(self.y) + ')'
...     def __cmp__(self,other): #값을 비교
...             return (self.x> other.x) and (self.y > other.y)
...
```

### self
e.g.9) self는 왜 안 적나요?
```
>>> p = Cpoint(1,2)
```
init은 3가지 인자를 가지지만 입력은 2개만 했다. 왜 그래도 에러 없이 실행이 되는걸까 라는 의문이 들었을 것이다.
이것은 객체지향 코드이다. 그리고 self라고 불리는 이상한 외부 변수가 있다.

그렇다면 self란 무엇인가?
위키피디아는 self가 통합된 것의 개념이라는 것을 알려준다.
그것은 특유한 의식의 원천이다.더욱이, 이 self는 그들이 생각 되어 지는 것의 각각의 생각 그리고 행동을 위한 대리인의 책임이 있다. 그것은 그러므로 시간 내내 견디는 물질이다.
따라서, 다른 시간에서의 생각과 그리고 행동은 같은 self와 관련된다.

이 때, self의 의미 중 중요한 요소가 숨겨져 있다.
인스턴스르 만들 때, 인스턴스를 특징화 하는 것에 접근할 수 있어야 하는 것이다.
여기서 인스턴스를 특징 짓는 것은 무엇이 계속 되는 지를 구체화하는 내부의 인자들이다.

파이썬의 객체 지향 시스템의 내부에서 무슨 일이 일어나는 지는 다음과 같다.

init을 부를 때, 그것은 인스턴스를 만들 것이다. 특히, 그것은 self를 그 인스턴스를 언급하기 위해 사용될 것이다. 다르게 말하면 클래스 함수를 가지고 있을 때, 그것의 내부에 이 모든 내부적인 정의들을 가지고 있다.  
클래스의 정의를 호출할 때, 그것은 init을 호출한다. init은 그 인스턴스에 대한 포인터를 만들어낸다.self를 인스턴스의 포인터로 전해주면서 init. 즉, 포인터는 그것이 메모리에 있는 그 부분에 접근했다고 말한다.  
그리고 이제 위에서 본 코드의 self.x와 같이 그 메모리 내부에 x를 위해 전해 지는 값으로 정의한다. self.x는 구조 내부에, 변수이름 x를 만들고 연관된 값을 만든다. self가 항상 특정한 인스턴스를 가리킨다는 것이다.
관습에 의해 첫 번째 인자는 항상 **self** 입니다. 왜냐하면 그것은 **인스턴스의 포인터** 여야하기 떄문이다.

e.g.10)
```
>>> p
<__main__.Cpoint object at 0x7f3f7a1e16d8>
```
p는 Cpoiunt로부터 생긴 인스턴스이다.
p는 일종의 cartesain point이다. 메모리 위치가 있음을 확인할 수 있다.

e.g.11) 메소드 cartesain
```
>>> p.cartesain()
(1, 2)
```
클래스의 함수를 정의한 것들 중 하나는 내부의 메소드였다. 그 메소드는 이름을 가지고 있다.
우리는 클래스들이 메소드들을 가지길 원한다. 그렇게 되면 특정한 인스턴스의 값에 접근할 수 있다.  
위 예제에서 p.Cartesain은 일종의 데이터의 접근자라고 할 수 있다.

우리는 직접적으로 인자들의 값을 바꿀 수 있다.
이것은 데이터 은닉이다.
#### 데이터 은닉
데이터 은닉에 대해서 기본적으로 다음과 같이 생각한다.
우리는 값들을 정의된 메소스들을 통해 오직 인스턴스 값에 접근할 수 있다.이것은 매우 편리하다. 왜냐하면 이것은 모듈방식, 캡슐화를 주기 때문이다.   
그것이 기본적으로 말하는 것은 점을 만들 때, 값들에 접근할 수 있는 유일한 방법은 정의된 메소드들 중 하나를 사용하는 것이다. 이 경우에 이것과 부합한 것이 Cartesain이라고 할수 있다.
데이터 은닉을 말하는 또 다른 방법은, 그렇게 하지 마라.
들어가서 직접적인 접근을 사용함으로써, 값들을 바꾸지 마라.
오직 접근자, 값을 바꿔주는 기능을 하는 메소드들을 통해서 하라.  

값을 바꾸는 가장 좋은 위생적인 방법은, 직접 들어가서 그것을 바꾸지 않고 미리 정의된 메소드를 통해 값을 바꾸는 것이다.
미리 정의된 메소드를 통하지 않고서는 값을 읽어서도 안된다.

##### 연산자 오버로딩
__cmp__ 와 같은 역할을 하는 ,비교를 하는 기본적인 또는 일반적인 방법인 __eq__ 를 생성했을 때, 이 둘은 같은 것일까?  

연산자 오버로딩을 가짐으로써, 사용하고 싶은 모든 객체들의 하나의 일반적이나 인터페이스를 사용할 수 있다.
어떻게 어떤 메소드들이 클래스와 연관되었는지 알 수 있을까?  
e.g.12)
```
>>> dir(p)
['__class__', '__cmp__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', 'angle', 'cartesain', 'polar', 'radius', 'x', 'y']

```
p와 연관된 메소드들을 리스트 형태로 돌려준다. 종종 이것들을 fields라고 부른다.
그래서 인스턴스 내부에, 인스턴스와 연관되어 있어서, 우리는 메소드들과 fields를 갖는다. 메소드와 fields를 모두 인스턴스의 속성들이라고 부른다.

e.g.13) 숫자 1과 문자 1과 연관된 모든 메소드들의 비교
```
>>> dir(1)
['__abs__', '__add__', '__and__', '__bool__', '__ceil__', '__class__', '__delattr__', '__dir__', '__divmod__', '__doc__', '__eq__', '__float__', '__floor__', '__floordiv__', '__format__', '__ge__', '__getattribute__', '__getnewargs__', '__gt__', '__hash__', '__index__', '__init__', '__init_subclass__', '__int__', '__invert__', '__le__', '__lshift__', '__lt__', '__mod__', '__mul__', '__ne__', '__neg__', '__new__', '__or__', '__pos__', '__pow__', '__radd__', '__rand__', '__rdivmod__', '__reduce__', '__reduce_ex__', '__repr__', '__rfloordiv__', '__rlshift__', '__rmod__', '__rmul__', '__ror__', '__round__', '__rpow__', '__rrshift__', '__rshift__', '__rsub__', '__rtruediv__', '__rxor__', '__setattr__', '__sizeof__', '__str__', '__sub__', '__subclasshook__', '__truediv__', '__trunc__', '__xor__', 'bit_length', 'conjugate', 'denominator', 'from_bytes', 'imag', 'numerator', 'real', 'to_bytes']
>>> dir('1')
['__add__', '__class__', '__contains__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__getnewargs__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__mod__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__rmod__', '__rmul__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', 'capitalize', 'casefold', 'center', 'count', 'encode', 'endswith', 'expandtabs', 'find', 'format', 'format_map', 'index', 'isalnum', 'isalpha', 'isdecimal', 'isdigit', 'isidentifier', 'islower', 'isnumeric', 'isprintable', 'isspace', 'istitle', 'isupper', 'join', 'ljust', 'lower', 'lstrip', 'maketrans', 'partition', 'replace', 'rfind', 'rindex', 'rjust', 'rpartition', 'rsplit', 'rstrip', 'split', 'splitlines', 'startswith', 'strip', 'swapcase', 'title', 'translate', 'upper', 'zfill']
```
위 예시에서 두 개의 메소드들이 같지않다는 것을 알 수 있다.
이것은 사용가능한 어떤 메소드들이 있는지 확인하기 위해 가장 편한 방법이다.


## 선분
평면의 기하학에서 하는 쉬운 방법은 선분을 만드는 것이다. 선분은 시작점과 끝점을 가진다.

e.g.14) 선분의 길이를 구하는 클래스
```
>>> class Segment:
...     def __init__(self,start,end):
...             self.start = start
...             self.end = end
...     def length(self):
...             return math.sqrt(((self.start.x - self.end.x) * (self.start.x - self.end.x)) + ((self.start.y - self.end.y) *(self.start.y - self.end.y)))
...
>>> p1 = cPoint(3.0, 4.0)
>>> p2 = cPoint(5.0, 7.0)
>>> s1 = Segment(p1,p2)
>>> print(s1.length())
3.605551275463989
```

교수님의 메세지
 - 오직 메소드를 통해서 변수들에 접근한다. 그런 점에서 선분 클래스 예시는 직접적으로 x값을 다루기 때문에 좋은 코드가 아니라는 걸 말하고 싶다.
