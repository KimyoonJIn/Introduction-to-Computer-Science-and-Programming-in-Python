## 클래스의 핵심
클래스
- 추상 데이터 타입을 위한 템플릿이다
- 데이터와 메소드들을 함께 모으려는 방법 (모듈 방식의 개념)

데이터 은닉 : 메소드를 통해서만 그 부분에 접근할 수 있다.
- 파이썬은 이것을 강화 하지 않았다.

클래스는 인스턴스를 만드는데 사용된다. 인스턴스 내부에 속성들의 집합을 가진다.

## 상속
우리는 다른 클래스로부터 구체화된 클래스들을 가질 수 있다.
e.g.1) Person class
```
>>> class Person(object):
...     def __init__(self, family_name, first_name):
...             self.family_name = family_name
...             self.first_name = first_name
...     def familyName(self):
...             return self.family_name
...     def firstName(self):
...             return self.first_name
...     def __cmp__(self,other):
...             return cmp((self.family_name, self.first_name), (other.family_name, other.first_name))
...     def __str__(self):
...             return ('<Person : %s %s>' & (self.first_name, self.family_name))
...     def say(self, toWhom, something):
...             return ( self.first_name + ' ' +self.family_name + ' says to ' + toWhom.firstName() + ' '+ toWhom.familyName() +': ' +something)
...     def sing(self, toWhom, something): #또 다른 메소드를 사용하는 메소드의 예
...             return self.say(toWhom, something + 'tra la la')
...
>>> per = Person('foobar', 'frank')
>>> per.firstName()
'frank'
>>> per.say(per,'why are you not in class.')
'frank foobar says to frank foobar: why are you not in class.'
```
e.g.2) Person으로부터 상속받은 MIT Person class code
```
>>> class MITPerson(Person):
...     nextIdNum = 0 #지역변수
...     def __init__(self,familyName, firstName):
...             Person.__init__(self,familyName,firstName)
...             self.idNum = MITPerson.nextIdNum
...             MITPerson.nextIdNum += 1
...     def getIdNum(self):
...             return self.idNum
...     def __str__(self):
...             return '<MIT Person : %s %s>' % (self.first_name, self.family_name)
...     def __cmp__(self,other):
...             return cmp(self.idNum, other.idNum)
...
>>> p1 = MITPerson('Sam','Smith')
>>> p2 = MITPerson('Foobar','Jane')
>>> print(p1.getIdNum())
0
>>> print(p2.getIdNum())
1
```
이 때,
Superclass - Person
Subclass - MITPerson이다.
#Shadowing

e.g.3) 섀도잉
```
>>> class UG(MITPerson):
...     def __init__(self,familyName,firstName):
...             MITPerson.__init__(self, familyName, firstName)
...             self.year =None
...     def setYear(self, year):
...             if year >5 : raise OverflowError('Too many')
...             self.year = year
...     def getYear(self):
...             return self.year
...     def say(self,toWhom,something): #MITPerson -> Person
...             return MITPerson.say(self,toWhom,'Excuse me, but ' + something)
...
>>> me = Person('Grimson','Eric')
>>> ug = UG('Doe', 'Jane')
>>> ug.familyName()
'Doe'
>>> ug.say(per,'I really like 6.00')
'Jane Doe says to frank foobar: Excuse me, but I really like 6.00'
```
say함수의 say 메소드는 UG도 아닌, MITPerson도 아닌, Person 클래스로부터 왔다.
MITPerson이 say를 가지고 있지 않기 때문에 가지고 싶은 메소드를 찾을 때까지 person으로 가는 것이다.
이것이 섀도잉의 예이다.

여기서 종종 섀도잉은 **오버라이딩** 이라고 불린다.
