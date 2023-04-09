---
layout: post
title: -----DRAFT-----ITE4053_DL> 11-1 Convolution 
subtitle: 
categories: DeepLearning
tags: [DeepLearning, ITE4053]
use_math: true
---

### What is Image Filtering?

Image filtering: 

local image data로부터 새로운 값을 얻어내는 function.

굉장히 많은 방법이 있지만 심플한 것 배울것

### Linear Image Filtering

non linear 한 것도 많지만 이번 수업에선 단순한 linear 한것 볼것임

weighted sum 하는 것을 통해(가중 합) 갑을 하나 얻을 수 있음. (convolution) → 단순한 연산 

image filtering 으로 할 수 있는 것들:

- enhance image
    - 노이즈 제거, smooth, increase contrast, sharp하게, …
- Extract information from images
    - Texture, edges, distinctive points, etc.
- Detect patterns
    - Template matching

(심플 리니어 필터로도 많은 것을 할 수 있음)

### Point Spread Function (PSF)

: A linear function for the image filtering

(‘point spread’ function)

psf라는건 심플한 리니어 필터인데, 

psf를 위해서는 커널 필요하고, 커널 모양에 따라 값이 변함.

![4][4]

중앙 파란색 → 필터(= 커널)

----

~~작은 크기의 커널~~

~~커널에 하나의 값 있는 예시, 두개 있는 예시~~

—> 근데 값이 왜그렇게되지?? 연산이??

수업 끝나고 질문\)

Q. PSF의 연산

A. 가중 합과 다른 것임!!

source image에서 값이 있는 부분에만 필터 값 적용함.

이미지에서 값이 어떤 것이 되었던 간에 유무만 판단하여 적용.

그리고 소스 이미지에서 값이 있는 픽셀의 개수만큼 타겟 이미지의 갯수가 생성이 되고, 이들의 합이 output이 된다. 

#14

### Formulation

그리고 이 메카니즘을 수학적으로 표현하면, (수학적 definition)

G = H * F

![5][5]

수학적 정의만 봐서는 결과 어떻게 나올 지 모름


![6][6]

psf wiki

주어진 커널 모양으로 이미지가 퍼저나감. 그래서 이름이 ‘포인트 스프레드 커널’

### Convolution

![7][7]

실제로 두번째 줄 적용하면 컨볼루션 결과 얻을 수 있음

하지만 다른 방법으로,

H라는 이미지와 F라는 필터 있을 때

필터 뒤집고, cross correlation 구하면 컨볼루션의 결과 얻을 수 있음


### Cross-correlation

![8][8]

: Measure of similarity of two inputs(signals)

element wise로 곱한다.

### Convolution vs. Correlation

![9][9]


Convolution:   
점이 어떻게 퍼저나가는지에 대해

Correlation:  
두개의 데이터가 얼마나 비슷한지 측정하는

하지만 좌우 상하 뒤집은 커널 적용하면 컨볼루션과 같은 결과

---

Q. 결국 컨볼루션은 cross correlation을 필터 뒤집어서 하는 것..?

A. 식은 다른데 결과론적으로 봤을 때 cross correlation의 필터 뒤집어서 적용하면 컨볼루션의 결과가 된다.


[4]: /assets/images/post_img/2023-04-06-2Convolution/4.png
[5]: /assets/images/post_img/2023-04-06-2Convolution/5.png
[6]: /assets/images/post_img/2023-04-06-2Convolution/6.png
[7]: /assets/images/post_img/2023-04-06-2Convolution/7.png
[8]: /assets/images/post_img/2023-04-06-2Convolution/8.png
[9]: /assets/images/post_img/2023-04-06-2Convolution/9.png


[출처1]ITE4053 수업






