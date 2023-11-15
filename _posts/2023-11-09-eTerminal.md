---
layout: post
title: e-01 in terminal
subtitle: python
categories: python
tags: [python, code]
---

## 터미널에서 숫자 표현

[CLIP](https://github.com/openai/CLIP)의 zero-shot 코드를 돌려보면 output으로 각 class별 확률이 나온다.

CLIP



```

text = clip.tokenize(["alder flycatcher", "acorn woodpecker", "white ibis"]).to(device)

with torch.no_grad():
    image_features = model.encode_image(image)
    text_features = model.encode_text(text)
    
    logits_per_image, logits_per_text = model(image, text)
    probs = logits_per_image.softmax(dim=-1).cpu().numpy()

print("Label probs:", probs)  # prints: [[0.9927937  0.00421068 0.00299572]]


# Acorn_Woodpecker/391427.jpg   ["a diagram", "a dog", "a cat", "a bird"]
# Label probs: [[5.9159915e-04 5.8533618e-04 3.9655867e-04 9.9842656e-01]]

# Acorn_Woodpecker/391427.jpg   ["a diagram", "a dog", "a cat", "a bird", "acorn woodpecker", "alder flycatcher"]).to(device)
# Label probs: [[3.2474959e-06 3.2131163e-06 2.1768501e-06 5.4807151e-03 9.8330700e-01 1.1203607e-02]]

# Alder_Flycatcher/532326.jpg   ["a diagram", "a dog", "a cat", "a bird", "acorn woodpecker", "alder flycatcher"]).to(device)
# Label probs: [[1.0838326e-07 2.5759209e-07 2.8152965e-07 6.2112155e-04 6.8263017e-09 9.9937820e-01]]

# CLIP.png  ["a diagram", "a dog", "a cat", "a bird"]
# Label probs: [[0.9911703  0.00420373 0.00299083 0.00163516]]


# ------

# Acorn_Woodpecker/391427.jpg  ["a bird", "acorn woodpecker", "alder flycatcher"]
# Label probs: [[0.00548077 0.98331547 0.01120377]]

# Acorn_Woodpecker/391545.jpg  ["a bird", "acorn woodpecker", "alder flycatcher"]
# Label probs: [[5.4990454e-04 9.9944514e-01 4.9911046e-06]]

# Acorn_Woodpecker/391906.jpg  ["alder flycatcher", "acorn woodpecker", "white ibis"]
# Label probs: [[6.1842417e-07 9.9999785e-01 1.5640782e-06]]


#-------

# White_winged_Crossbill/243912.jpg   ["a bird", "white winged crossbill", "white ibis"]
# Label probs: [[6.8848167e-05 4.9102495e-09 9.9993110e-01]]


```


























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







