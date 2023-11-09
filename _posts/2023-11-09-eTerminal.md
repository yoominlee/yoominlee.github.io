---
layout: post
title: e-01 in terminal
subtitle: python
categories: python
tags: [python, code]
---

## 파이썬 f-string 포멧팅






























%연산자나 함수가 아니라 새로본 포멧팅 방식

### 사용 예시
<pre>
<code>
epoch = 0
loss = 1
print(f"Loss after epoch {epoch}: {loss}")
</code>
</pre>
위와 같이 작성하면 
Loss after epoch 0: 0.70199928 -> 이런 형태로 나온다.

> 딥러닝 수업에서 100 epoch 마다 weight나 bias, loss등을 출력하는데 깔끔하게 쓰기 좋았다.

### 다른 효과
#### 변수명 간단히 쓰기

아래와 같이 중괄호 안에 변수와 =을 붙이면,
{bugs=}를 쓰면 출력 시 입력한 것과 그 값이 옆에 나온다.

<pre>
<code>
>>> print(f'Debugging {bugs=} {count=} {area=}')
Debugging bugs='roaches' count=13 area='living room'
</code>
</pre>


#### 딕셔너리 넘겨서 키로 값 접근하기
포맷할 변수 위치에 이름으로 지정할 수 있음
[] 대괄호 사용
<pre>
<code>
>>> table = {'Sjoerd': 4127, 'Jack': 4098, 'Dcab': 8637678}
>>> print('Jack: {0[Jack]:d}; Sjoerd: {0[Sjoerd]:d}; '
          'Dcab: {0[Dcab]:d}'.format(table))

Jack: 4098; Sjoerd: 4127; Dcab: 8637678
</code>
</pre>



#### 정렬
':' 뒤에 정수를 전달하면 해당 필드의 최소 문자 폭이 된다. 
<pre>
<code>
>>> table = {'Sjoerd': 4127, 'Jack': 4098, 'Dcab': 7678}
>>> for name, phone in table.items():
        print(f'{name:10} ==> {phone:10d}')

Sjoerd     ==>       4127
Jack       ==>       4098
Dcab       ==>       7678
</code>
</pre>

:> : 오른쪽 정렬   
:< : 왼쪽 정렬   
:^ : 가운데 정렬   
:*> : 오른쪽 정렬 후 *로 채움   
:*< : 왼쪽 정렬 후 *로 채움   
:*^ : 가운데 정렬 후 *로 채움   

[출처1 ](https://docs.python.org/ko/3/tutorial/inputoutput.html) https://docs.python.org/ko/3/tutorial/inputoutput.html







