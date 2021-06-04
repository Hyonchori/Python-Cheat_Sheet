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
