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
