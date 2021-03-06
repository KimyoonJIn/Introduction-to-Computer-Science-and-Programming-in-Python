# [MIT - Introduction to Computer Science and Programming in Python](https://www.inflearn.com/course/mit-%EA%B3%B5%EA%B0%9C%EA%B0%95%EC%A2%8C-python/)

## 리스트
e.g.1) append
```
>>> Ivys  = ['Yale',-1,'Princeton']
>>> Ivys[3] = -15
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: list assignment index out of range
>>> Ivys[1] = -15
>>> Ivys
['Yale', -15, 'Princeton']
```
e.g.2) 같은 객체를 가르킨다는 예시
```
>>> L1 =[1,2,3]
>>> L2 = L1
>>> L2
[1, 2, 3]
>>> L1[0] =4
>>> L1
[4, 2, 3]
>>> L2
[4, 2, 3]
>>> L1=[]
>>> L1
[]
>>> L2
[4, 2, 3]
```
## Dictionary
- 가변성
- 정렬되지않는다
- 빠르다
- 모든 요소를 {key : value} 형식으로 나타낸다.
  - key를 인덱스들처럼 사용된다.
- 일정시간에 키를 검색하도록 허용하는 Hashing이라는 기술을 사용한다.
- 어떤 값을 찾기 위해서 리스트에선 각 요소를 하나씩 모두 보아야한다. 리스트의 길이가 길수록 시간이 오래 걸린다는 특징이 있다. 하지만 dict인 경우 그에는 상관없이 순간적으로 key와 연결된 value를 검색할 수 있기에 강력하다.

e.g.1)  
```
>>> def showDicts():
...     EtoF = {'one' :'un', 'soccer' :'football', 'never':'jamais'}
...     print(EtoF['soccer'])
...     print(EtoF[0])
...     print(EtoF)
...
>>> showDicts()
football
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 4, in showDicts
KeyError: 0
```
e.g.2)
```
>>> def showDicts():
...     NtoS = {1 :'one', 2 :'two', 'one':1,'two':2}
...     print(NtoS)
...     print(NtoS.keys())
...     print(NtoS.keys)
...
>>> showDicts()
{1: 'one', 2: 'two', 'one': 1, 'two': 2}
dict_keys([1, 2, 'one', 'two'])
<built-in method keys of dict object at 0x0000014CF38D4318>
```


## 의사코드 - 단계의 설명
함수의 관점에서 코드의 구조를 만들고 코드를 조직하는데 도움을 주기 위해, 전체 코드의 단계들을 설명하는 의사코드를 설정  
e.g.1) 직각 삼각형의 빗변의 길이 계산
```
의사코드 - 단계의 설명
1. input  : 실수로써 기본적인 값 입력
2. 높이 :  실수형 입력
3. 제곱근 찾기
  - 빗변에 실수로 저장
4. 출력 : 빗변의 길이
```
의사코드를 사용하고 코드를 짬으로써, 사용자에게 보여지는 것이 무엇이고 실제 내부에서 돌아가는 computation이 무엇인지 분리해서 볼 수 있다. 그럼으로 사용자와 실행자 사이의 분리를 구축한다는 생각을 할 수 있다. 이것이 함수를 생성하고 싶은 이유들 중 하나이다.

교수님의 메시지
- 의사코드 사용하는 습관을 갖고 단계들이 무엇인지 적어라

## 효율성

#### 효율적인 실행을 생산하는 방법을 고안
 - 효율성은 알고리즘 선택에 대한 것이다
 - 어떤 효울성의 알고리즘을 클래스로 만드는 것을 돕고 싶다.

알고리즘의 효율성을 측정하고 싶은 것 두 가지
1. 공간 : 컴퓨터 메모리 - 계산을 하기 위해 얼마만큼의 메모리를 사용하는가
2. 시간  - 알고리즘을 수행하는데 시간이 얼만큼 걸리는가


#### 입력 사이즈의 함수로써 필요한 기본적인 단계의 수는 무엇입니까?
1. 구체적으로 입력의 관점에서 수행할 것
  - 입력사이즈는 무엇으로 할까: 리스트, 튜플 등
2. 기본적인 단계가 무엇인가
3. 랜덤 접근 모델
  1. 어떤 데이터를 메모리의 어떤 위치로 가져와서, 일정한 시간에 어떤 명령을 할 수 있다는 가정
  2. 기본적인 초기 요소들은 일정한 시간 갖는다는 가정
4. 가능성
  -  최고의 경우 - 최소의 것(min)
  -  최악의 경우 - 최대의 것(max)
  -  예측된 경우 - 평균(mean)

결과적으로 우리는 **최악의 경우** 로 초점을 맞출 것이다.
