# coding_test_-
테스트 풀이 소스 업로드

### 1. BreadType객체 (팩토리 메소드구현 + 속성 출력)
```
# 추상클래스 abc(abstract base class)라는 모듈을 임포트
from abc import ABCMeta, abstractmethod

# BreadType 클래스를 추상클래스로 생성, recipe 메소드 구현
class BreadType(metaclass=ABCMeta):
    @abstractmethod
    def recipe(self):
        pass
    
# BreadType 을  상속받는 클래스는 recipe 메소드를 구현해야만 객체생성    
class Cream(BreadType):
    def recipe(self):
        print('breadType: ','cream')
        print('recipe')
        print('flour: ', 100)
        print('water: ', 100)
        print('cream: ', 200)
        
class Sugar(BreadType):
    def recipe(self):
        print('breadType: ','sugar')
        print('recipe')
        print('flour: ', 100)
        print('water: ', 50)
        print('sugar: ', 200)
        
class Butter(BreadType):
    def recipe(self):
        print('breadType: ','butter')
        print('recipe')
        print('flour: ', 100)
        print('water: ', 100)
        print('butter: ', 50)
        
# 클래스 선언 후 객체를 생성     
if __name__ == '__main__':
    cream = Cream()
    sugar = Sugar()
    butter = Butter()
    
    # BreadType 객체의 리스트를 순환하며 출력
    list = ['cream.recipe()','sugar.recipe()','butter.recipe()']        
    [eval(i) for i in list]
```
* 추상클래스 모듈을 임포트 하여 breadType 클래스를 추상클래스로 생성 후, 반복되는 recipe 메소드를 구현했습니다.
* 이때 recipe를 구현하지 않으면 에러가 나므로 꼭 구현합니다.
* 객체 리스트를 순환하며 출력하는 조건이 있었으므로 리스트를 만들어 eval() 함수를 이용하여 함수를 호출합니다.


### 2. 체이닝메소드 이용, add, substract 함수 구현(calculator)
```
class Calculator():
   
    
    def __init__(self,result):
        self.result = result
       
    def add(self,value):
        self.result += value
        return self
     
    def subtract(self,value):
        self.result -= value
        return self
        
calculator = Calculator(0)  

print(calculator.add(4).add(5).subtract(3).result)
```

* 체이닝 메소드를 이용하기 위한 calculator 클래스 생성, 여기서 함수 return에서 self.result가 아닌 self인점 주의가.


### 3. 재귀함수를 이용하여 Factorial 을 구하는 함수
```
def factorial(n):
    if n == 1:
        return 1
    return n * factorial(n - 1)

factorial(1000)
```
* 알고리즘의 기초적인 재귀함수를 이용한 팩토리얼 구하는 함수. 표현은 쉽지만 여기서 자기자신을 계속 호출하기 때문에 공간 낭비가 많아 메모리 초과 오류가 발생할 수 있습니다. 

/n /n
### 4. Factorial 함수에서 Stack Overflow 해결
```
# stack 재사용으로 overflow 방지하는 꼬리재귀 함수 사용 또는 while 루프
def factorial(number, accumulator=1):
    if number == 0:        
        return accumulator
    else:       
        return factorial(number - 1, number * accumulator)
print(factorial(1000))


# 또는 math  모듈 (팩토리얼값 구하는 함수 제공)
from math import factorial
print(factorial(1000))
```
* 메모리 초과 오류 방지를 위해 꼬리재귀 함수 또는 while 문을 쓴다. 파이썬일 경우 math의 모듈의 팩토리얼 함수를 사용하면 간편하게 구할 수 있습니다. 



### 5. 디지털 연못 물 깊이의 총합
```
import pandas as pd
import numpy as np

df = pd.read_csv('data/pond.txt', sep=' ', header=None)

data = df.values.tolist()

dx=[-1,0,1,0]
dy=[0,1,0,-1]
n= df.index.size # data 행과 열값이 같으므로.. index값으로 길이를 구한다.

# 위아래 좌우가 1일경우,
for i in range(1, n):
    for j in range(1, n):
        # i+dx[k] : 행 / j+dy[k] : 열
        if all(data[i][j] >0 and data[i+dx[k]][j+dy[k]]>=1 for k in range(4)):
            data[i][j] +=  1
            
# 위아래 좌우가 2일경우,            
for i in range(1, n):
    for j in range(1, n):             
        if all(data[i][j] >0 and data[i+dx[k]][j+dy[k]]>=2 for k in range(4)):
            data[i][j] +=  1
            
# 위아래 좌우가 3일경우,            
for i in range(1, n):
    for j in range(1, n):             
        if all(data[i][j] >0 and data[i+dx[k]][j+dy[k]]>=3 for k in range(4)):
            data[i][j] +=  1            

data
# 데이터프레임으로 변환
df2 = pd.DataFrame(data)
# 행기준으로 합계
df2[10]=df2.sum(axis=1)
df2
# 행기준 합계를 열기준으로 다시 합계
result = df2[10].sum()
print("연못 깊이의 총합은 : ", result)
```
* pond.txt 파일을 판다스 데이터프레임으로 읽어옵니다.
* 판다스 프레임을 2중리스트로 변환합니다.
* 사방의 값과 비교해야 하므로 dx=[-1,0,1,0] dy=[0,1,0,-1] 가 필요합니다.
* 사방값이 1일경우, 2일경우, 3일경우 각각 이중 for문을 돌면서 + 1 을 해줍니다. 
* 연못깊이의합을 구하기 위해 다시 for 문을 돌리는것보다 간편한 데이터 프레임의 sum 함수를 이용하기 위해
* 데이터 프레임으로 변환합니다.
* 행 기준으로 sum을 해서 새로운 데이터 열을 만든 후 
* 새로운 열의 sum 을 구하면 연못 깊이의 합계가 나옵니다.

### 총 걸린 시간은 오전 9시에 시작하여 1시 반에 끝났습니다. (4시간 반 소요)
