# Python-Cheat_Sheet
 Cheat sheet for Python programming

## str.format()을 이용한 문자열 포맷팅
```python
print("이름: {0}, 나이: {1}세".format("홍길동", 20))   # {}안에 인덱스에 해당하는 값 표시
print("이름: {1}, 나이: {0}세".format("홍길동", 20))


print("{0:c} => {1}".format(97, 97))                          
print("{0}, {1}, {2:x}".format("가", ord("가"), ord("가")))   # {}내에서 :뒤에 문자열 표시 유형을 지정할 수도 있음


print("{0:f} {1: .2f}, {2:06.3f}".format(3.141592, 3.141592, 3.141592))   # 위처럼 부동소수점의 소숫점 정밀도, 출력 폭 표현 가능


print("이름: {name}, 나이: {age}세".format(name="홍길동", age=20))  # 인덱스 대신 키 형태로 값을 넣을 수 있음


print("{0:<10}".format("좌측정렬"))
print("{0:>10}".format("우측정렬"))
print("{0:^10}".format("중앙정렬"))   # <, >, ^ 를 이용해 정렬 방향 설정 가능
print("{0:*^10}".format("중앙정렬"))  # 공백을 채울 문자를 지정할 수도 있음


print("{0:0.2f}".format(3.141592))
print("{0:10.2f}".format(3.141592))
print("{0:010.2f}".format(3.141592))
print("{{ {0:1f} }}".format(98.5))    # 부동소수점 표현 및 대괄포 {} 표현 방법
```
---
## 가변 매개변수
>**가변 매개변수 사용의 주의점**
>- 하나만 지정할 수 있음
>- 가장 마지막 매개변수로 지정할 것

### - 튜플 형식의 가변 매개변수
```python
def calc_sum(*params):
    total = 0
    for val in params:
        total += val
    return total

print(calc_sum(1, 2, 3))
print(calc_sum(4))
print(calc_sum(1, 3, 4, 5, 6, 7))
```
### - 딕셔너리 형식의 가변 매개변수
```python
def use_keyward_arg_unpacks(**params):
    for k in params.keys():
        print("{}: {}".format(k, params[k]))
        
use_keyward_arg_unpacks(a=1, b=2, c=3)
```
---
## 클로저
```python
def outer_func():
    id = 0
    
    def inner_func():
        nonlocal id   # 변수 id가 중첩함수인 inner_func 함수의 지역변수가 아니라는 뜻
                       # 이는 변수 id 접근 시 outer_func 함수의 스코프에서 찾게 만듦
        id += 1
        return id
    
    return inner_func

make_id = outer_func()
print("make_id() 호출의 결과: {}".format(make_id()))    # 1
print("make_id() 호출의 결과: {}".format(make_id()))    # 2
print("make_id() 호출의 결과: {}".format(make_id()))    # 3
```

---
## random 모듈
- 난수 생성 관련 모듈
```python
from random import random, uniform, randrange, choice, choices, sample, shuffle

print(random())         # 0.0 < N < 1.0 범위의 부동소수점 난수 N 반환
print(uniform(1, 10))   # 지정된 범위 내의 부동소수점 난수 N 반환
print(randrange(1, 45, 2))  # start, end, step 매개변수를 받아 정수형 난수 N 반환

print(choice([1, 2, 3, 4, 5])) # 인자로 전달된 시퀀스 객체의 항목 중 임의 항목 반환
print(choices([1, 2, 3, 4, 5], k=2)) # 인자로 전달된 시퀀스 객체의 항목 중 임의 항목 k개 반환 (복원추출)
print(sample([1, 2, 3, 4, 5], k=2)) # 인자로 전달된 시퀀스 객체의 항목 중 임의 항목 k개 반환 (비복원추출)

lst = [1, 2, 3, 4, 5]
shuffle(lst)
print(lst)
```

---
## datetime 모듈
- 날짜와 시간 정보를 확인하고 조작
```python
from datetime import datetime, timezone, timedelta

now = datetime.now()
print("{0}-{1:02}-{2:02}-{3:02}-{4:02}-{5:-02}".format(
    now.year, now.month, now.day, now.hour, now.minute, now.second))    # 2021-06-04-20-40-52

fmt = "%Y{0} %m{1} %d{2} %H{3} %M{4} %S{5}"
print(now.strftime(fmt).format(*"년월일시분초"))     # 2021년 06월 04일 20시 40분 52초
```
---
## 리스트
### 리스트 슬라이싱
```python
lst = [10, 20, 30, 40, 50]
print(lst[0], lst[1], lst[2], lst[3], lst[4])
print(lst[-1], lst[-2], lst[-3], lst[-4], lst[-5])

print(lst[2: 5])       # 슬라이싱
print(lst[2:3])        # 슬라이싱으로 요소 하나만 추출

print(lst[:])       # 슬라이싱으로 전체 리스트 반환
print(lst[::-1])    # 슬라이싱 방법 중 리스트의 순서를 뒤집는 방법

print(lst[::2])     # 전체 리스트를 인덱스 간격 2로 반환
print(lst[::-2])    # 뒤집은 리스트를 인덱스 간격 2로 반환
```

### 리스트 항목 추가
```python
lst = [10, 20, 30, 40]
lst.append(50)
print(lst)

lst = [10, 20, 30, 40]
lst.insert(0, 0)
lst.insert(-1, 50)
print(lst)

lst = [10, 20, 30, 40]
lst.extend([70, 80])    # = [10, 20, 30, 40] + [70, 80]
lst.append([90, 100])   # append는 항목의 타입 상관없이 다 가능
print(lst)
```

### 리스트 for 문
- **enumerate()** 함수를 이용하면 각 항목의 인덱스도 같이 출력 가능

```python
lst = list(range(0, 11, 2))

for i, item in enumerate(lst):
    print("{}: {}".format(i, item))
 ```

### 리스트 내포 (comprehension)
```python
array = [[[c for c in range(3)] 
          for y in range(3)] 
         for x in range(3)]
```
---
## 딕셔너리
### 딕셔너리 value 기준 정렬
```python
data_dict = {
    "홍길동" : 20,
    "이순신" : 45,
    "강감찬" : 35
}

data_list = sorted(data_dict.items(), key=lambda items: items[1], reverse=True)
print(data_list)
# [('이순신', 45), ('강감찬', 35), ('홍길동', 20)]
```
---
## 문자열
### 문자열 출현 횟수 확인
>**str.count()**
>- 해당 문자열에서 입력 문자열이 출현한 횟수 반환
```python
data_str = "Have a nice day!"

print(data_str)
input_str = input("위에서 찾고자 하는 문자열을 입력하세요: ")

print("{}는 {}번 나타납니다.".format(input_str, data_str.count(input_str)))
```

### 문자열 탐색
- **str.find()** : 문자열의 처음부터 탐색 시작. 찾으면 시작 인덱스 반환, 못 찾으면 -1  반환
- **str.rfind()** : 문자열의 끝부터 탐색 시작. 찾으면 시작 인덱스 반환, 못 찾으면 -1 반환
- **str.index()** : 입력 문자열이 처음 나타난 인덱스 반환, 못 찾으면 ValueError 발생

### 문자열 삽입
>**str.join()**
>- 해당 문자열을 입력 문자열 사이사이에 삽입한 문자열 반환
```python
data_str = "가나다라마바사아자차카타파하"
comma_space = ", "
print(comma_space.join(data_str))
```
### 문자열 제거
- **str.lstrip()** : 인자로 전달된 문자열을 왼쪽에서 제거
- **str.rstrip()** : 인자로 전달된 문자열을 오른쪽에서 제거
- **str.strip()** : 인자로 전달된 문자열을 양쪽에서 제거
```python
data_str = "__ ?0 Py thon _$@#   "
print(data_str.lstrip(" 0?_#@$"))
print(data_str.rstrip(" 0?_#@$"))
print(data_str.strip(" 0?_#@$"))
```
### 문자열 교체
> **str.replace()**
>- replace(찾을 문자열, 교체 문자열, 횟수)
>- 찾을 문자열과 교체 문자열을 인자로 사용해 교체
```python
data_str = "10....20....30....40....50"
print(data_str.replace("....", "\t"))
print(data_str.replace("....", "\t", 2))
print(data_str.replace("....", "",))
```
### 문자열 자르기
>**str.split()**
>- 인자로 전달된 문자열을 기준으로 나누는 리스트 객체 생성
```python
data_str = "10, 20, 30, 40, 50"
data_str = data_str.replace(" ", "")
data_list = data_str.split(",")
print(data_list)
```
### 문자열 구성 확인
- **str.isdigit()** : 숫자로만 구성된 문자열인지 True/False 반환
- **str.isalpha()** : 알파벳으로만 구성된 문자열인지 True/False 반환
- **str.isalnum()** : 숫자, 알파벳으로만 구성된 문자열인지 True/False 반환

---
## 클래스
### 데커레이터를 이용한 인스턴스 변수의 getter, setter 구현
### 클래스 변수를 이용한 인스턴스 counting
### 클래스 메서드 @classmethod
### 비교연산자 오버로딩
### str 메서드
```python
class Person:
    count = 0    # 클래스 변수 선언
    
    def __init__(self, name, age):
        self.__name = name
        self.__age = age
        Person.count += 1
        print("객체 '{}'가 생성되었습니다.".format(self.__name))
    
    def __del__(self):
        print("객체 '{}'가 제거되었습니다.".format(self.__name))
        
    def to_str(self):
        return "{}\t{}".format(self.__name, self.__age)
    
    @property
    def name(self):
        return self.__name   # 클래스의 변수처럼 사용 가능. __name 필드값을 반환하는 getter 메서드 역할
    
    @property
    def age(self):
        return self.__age   # 클래스의 변수처럼 사용 가능. __age 필드값을 반환하는 getter 메서드 역할
    
    @age.setter
    def age(self, age):    # 변수처럼 사용 가능, __name 필드값을 반환하는 setter 메서드 역할
        if age < 0:
            raise TypeError("나이는 0 이상의 값만 허용합니다.")
        self.__age = age
    
    @classmethod
    def get_info(cls):
        return "현재 Person 클래스의 인스턴스는 총 {}개 입니다.".format(cls.count)
    
    def __gt__(self, other):  # greater than로 비교 연산자 '>' 에 해당
        return self.__age > other.__age
    
    def __ge__(self, other):  # greater and equal로 비교 연산자 '>=' 에 해당
        return self.__age >= other.__age
    
    def __lt__(self, other):  # lower로 비교 연산자 '<' 에 해당
        return self.__age < other.__age
    
    def __le__(self, other):  # lower and equal로 비교 연산자 '<= 에 해당
        return self.__age <= other.__age
    
    def __eq__(self, other):  # equal로 비교 연산자 '==' 에 해당
        return self.__age == other.__age
    
    def __ne__(self, other):  # not equal로 비교 연산자 '!=' 에 해당
        return self.__age != other.__age
    
    def __str__(self):
        return "{}\t{}".format(self.__name, self.__age)

members = [
    Person("홍길동", 20),
    Person("이순신", 45),
    Person("강감찬", 35),
]
```


