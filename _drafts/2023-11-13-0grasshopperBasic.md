---
layout: post
title: Grasshopper(Rhino6) basic
subtitle: Design with grasshopper
categories: GenerativeDesign
tags: [rhino, 3D, grasshopper]
---

## Basic in Grasshopper


### Extensions

보통 [food4rhino](https://www.food4rhino.com/en)에서 extension압축파일을 받는 경우가 많다. 
 
이때 압축파일의 설치 방법이 나와 있는 텍스트 파일 등에서 ```압축폴더에서 특정 폴더를 'User Object Folder'로 복사해라```와 같은 내용이 있기도 하다. 

<br>   

참고) extension중 wasp의 설치 가이드의 일부:   
```
- Copy the folder "wasp" in the Grasshopper Libraries folder (File -> Special Folder -> Components)
- Copy the CONTENT of the UserObjects folder into Grasshopper user objects folder (File -> Special folders -> User Objects)
...
```

위에서 말하는 디렉토리를 찾아 헤맸었는데, 그럴 필요가 없다.  

우선 라이노를 켜고, grasshopper에 들어가면,   
```File > Special Folders``` 를 선택 후 설치파일에서 요구한 이름을 클릭하면, 요구했던 이름의 디렉토리가 파일탐색기로 열린다. 이 위치에 다운받은 폴더를 복사하기만 하면 완료. 

![1][1]



### 기본적 용어
기본 화면의 상단 바의 다양한 구성요소들을 Component라고 하고, 이런 component들을 아래의 Canvas라고 하는 공간에 드래그 해 주면 된다.

- Component
- Canvas

### 원하는 component 검색
Canvas를 더블클릭하면 검색어를 입력할 수 있는 사각형이 나온다.

![2][2]

### Component 

각각의 component들은 하나의 함수라고 생각하면 이해가 잘 되는 것 같다. 함수처럼 각각의 형태에 맞는 다양한 파라미터들을 input으로 넣어주고 다양한 return값인 output도 존재한다.

이때의 input과 output은 다 선으로 연결해준다. 

#### Example

![3][3]

- Line SDL   
canvas를 더블클릭 후 'line'을 검색하면 정말 다양한 line들이 있다.    
Rhino에서 그린 line을 담는 변수 역할을 하는 Line,   
시작점(A)과 끝점(B)을 input으로 넣는 Line,   
시작점(S)과 방향(D), 길이(L)를 input으로 넣는 Line SDL.   
위 두개는 input형태는 다양하지만, output은 line segment로 동일하다. 

    추가적으로 LineDimension(LineDim)과 같이 line, text, size를 input으로 가지고 이에 대한 dimension을 표현하는 component도 있다.

    - input:
        - Start(S): line start point (default: empty)
        - Direction(D): Line tangent(direction) (default=(0,0,1))
        - Length(L): Line length (default=1)

    - output: 
        - Line segment

- Sphere(Sph)
    - input: 
        - Base(B): Base plane (default=World XY)
        - Radius(R): Sphere radius (default=1)
    - output:
        - Sphere(S): input에 맞는 형태의 sphere

- Sphere 4Pt (Sph4Pt)
    - input: 
        - Point 1(P1): First point
        - Point 2(P2): Second point (P1과 겹치면 안됨)
        - Point 3(P3): Third point (P1, P2와 겹치면 안됨)
        - Point 4(P4): Fourth point (P1, P2, P3과 겹치면 안됨)
    - output:
        - Center(C): sphere의 center point
        - Radius(R): sphere의 radius number
        - Sphere(S): P1~P4에 fit한 sphere


위 예시들과 같이 다양한 함수형태의 component 존재.

component 생성 후 마우스 hover시 component 및 파라미터들에 대해서도 간략한 설명이 나온다. 





---

[1]: /assets/images/post_img/2023-11-13-0grasshopperBasic/1.png
[2]: /assets/images/post_img/2023-11-13-0grasshopperBasic/2.png
[3]: /assets/images/post_img/2023-11-13-0grasshopperBasic/3.png
[4]: /assets/images/post_img/2023-11-13-0grasshopperBasic/4.png
[5]: /assets/images/post_img/2023-11-13-0grasshopperBasic/5.png
[6]: /assets/images/post_img/2023-11-13-0grasshopperBasic/6.png
[7]: /assets/images/post_img/2023-11-13-0grasshopperBasic/7.png
[8]: /assets/images/post_img/2023-11-13-0grasshopperBasic/8.png




