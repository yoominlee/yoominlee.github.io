---
layout: post
title: -----DRAFT-----ITE4052_CV > 5_Image processing
subtitle: 3D Vision
categories: ComputerVision
tags: [ComputerVision, ITE4052]
use_math: true
---


전 시간에 이미지 퀄리티를 조절하는 부분 배웠었음!

이미지 밝기 높이기 위한 세 방법과 각 방법의 trade off들!

[페이지 마지막 밝기 조절 3가지]({% post_url 2023-04-12-CV_2Camera %})

이러한 이미지의 noise와 blur enhance 어떻게 하나? → Filtering의 motivation

## Noise Reduction

어떻게 노이즈를 제거할 수 있을까?

각 이미지 u는 노이즈 없는 이미지인 v에 노이즈n을 더한 값이라고 생각

따라서 각 이미지들은

$u_1 = v + n_1$

$u_2 = v + n_2$ 이런식으로 이루어져있음

이러한 노이즈를 줄이기 위해선, 이미지 평균을 낸다!

그렇게 되면 n~N(0,$\sigma$) → n~N(0, $\sigma^2 \over 2$) 형태가 된다.

## Image Fidelity Criteria

![1][1]

PSNR ⁉️❓

추가 필요

## Linear Filterig(Convolution)

원래 픽셀 값을 linear combination (weighted sum) 해서 변경.

linear combination에 쓰이는 weight들은 kernel, mask, filter라고 함!!

- signal processing에서의 convolution과 좀 차이가 있음

딥러닝의 컨볼루션은 엄밀히 말하면 필터를 상하 좌우 뒤집어서 cross-correlation을 하는것임.

![2][2]

### Linear filters : examples

- Identical Images

0 0 0

0 1 0

0 0 0

- 좌측으로 1 shift

0 0 0

1 0 0

0 0 0

주의 할껀, 이걸 filp 한걸 연산한다!

0 0 0

0 0 1

0 0 0

위의 필터가 이미지 중앙 픽셀에 적용된다면, 중앙 픽셀에는 중앙보다 한 칸 우측의 값이 중앙에 들어오게 되는거임.

- mean filter (Blur)

1 1 1

1 1 1

1 1 1 *(1/9)

noise reduction할 때 사용   
but blurry

- Sharpening filter

![3][3]

원본 이미지에,   
identity에 magnitude 곱한 것에서, blur 한 필터를 뺀다.

## Directional Smoothing

![4][4]

smoothing 하는 동안 blurring 되는 것을 막기 위해

mean filter로는 사각형 area에서 평균을 내는 것

directional smoothing은 대각선 방향

⁉️❓ 저 범위를 평균 내는 것?

효과

- still reduce the noise
- prevent blurring

노이즈 제거하면서 blurring 막고 싶을 때 사용한다. 

## Median Filtering

receptive field (= 수용영역: 출력 레이어의 뉴런 하나에 영향을 미치는 입력 뉴런들의 공간 크기)의 픽셀 중 중앙값 

<피피티랑 내 손필기 첨부>

픽셀바이 픽셀 연산 단계

1. <u>필터 상하 좌우 뒤집기</u>
2. 0을 기준으로 원본 이미지 좌측부터 범위 보기
3. 그 범위에서 중앙값 선택. 
    1. 만약 두 값이면 두개 더해서 평균
    2. 원본 이미지 범위 넘어가면 0기준인 곳의 픽셀 리턴.
4. 위 과정을 모든 픽셀에 대해(0부분과 대응) 진행

⇒ outlier 를 제거하는것!!!

하지만 이것도 너무 많이 제거 시 blur해짐. (따라서 필터 크기 정하는 것도 중요)

주의할 것은 Median filter는 linear 연산이 아님!!

$\because$ weight가 필터에 없음.

## Gaussian Filter

가우시안 필터와 평균필터 모두 blur 함.

하지만 결과 다름(아니 당연하지 곱하는 값이 다른데)

- high-frequency 요소를 지운다. = remove detail, boundary
    
    (= low pass filter)
    
- 오직 low freq 값만 남기는 것임.

(smoothing 빼고 디테일만 남은 것은 high-pass filter)

## Sharpen Filter

<< 수식! 필기와 피피티 첨부 >>

## Edge Enhancement

(이름은 기억할 필요 없지만,) Prewitt과 Sobel필터로 edge detection.

pixel의 gradient를 계산해서 edge를 얻는 필터이다!

(compute gradient of pixels to detect edge)

## Point Operations

각 픽셀에 대해 point operation,

<< 피피티 #40 >>

- Contrast Stretching
    - linear filter 아님
- Clipping
    - 일정 구간의 수치는 0으로, 일정 수치 이상은 255로 바꿔주는 것.
- Thresholding
    - clipping의 스페셜 케이스.
    - a보다 크면 max 255값, a보다 작으면 0 값.
- Gamma correction
    - <#43 첨부>
    - contrast value 조정하는데 유용.
    - 감마 값이 1보다 작으면 전체적으로 밝아지고, 어두운 부분의 대비가 커짐
        
        (어두운 픽셀 부분의 기울기 급격) overall bright, high contrast on dark region
        
    - 감마 값이 1보다 크면 전체적으로 어두워지고, 밝은 부분의 대비가 커짐
        
        (밝은 부분의 기울기가 급격) overall dark, high contrast in bright region.
        
- Histogram Equalization ⭐
    - 히스토그램 : 이미지의 밝기 레벨에 따른 frequency of occurrence
    - 목표는 히스토그램을 uniform 한 분포로 만드는 것.
    - << 증명 부분 >>
    - ⁉️❓ 다시 보기!!! 증명 부분 찾아보기,,

---


[1]: /assets/images/post_img/2023-04-18-CV_5ImageProcessing/1.png
[2]: /assets/images/post_img/2023-04-18-CV_5ImageProcessing/2.png
[3]: /assets/images/post_img/2023-04-18-CV_5ImageProcessing/3.png
[4]: /assets/images/post_img/2023-04-18-CV_5ImageProcessing/4.png



[5]: /assets/images/post_img/2023-04-18-CV_5ImageProcessing/5.jpg
[6]: /assets/images/post_img/2023-04-18-CV_5ImageProcessing/6.jpg
[7]: /assets/images/post_img/2023-04-18-CV_5ImageProcessing/7.jpg


[8]: /assets/images/post_img/2023-04-09-CV_43Dpart/8.jpg
[9]: /assets/images/post_img/2023-04-09-CV_43Dpart/9.jpg
[10]: /assets/images/post_img/2023-04-09-CV_43Dpart/10.jpg
[11]: /assets/images/post_img/2023-04-09-CV_43Dpart/11.jpg
[12]: /assets/images/post_img/2023-04-09-CV_43Dpart/12.jpg
[13]: /assets/images/post_img/2023-04-09-CV_43Dpart/13.jpg
[14]: /assets/images/post_img/2023-04-09-CV_43Dpart/14.jpg
[15]: /assets/images/post_img/2023-04-09-CV_43Dpart/15.jpg
[16]: /assets/images/post_img/2023-04-09-CV_43Dpart/16.jpg
[17]: /assets/images/post_img/2023-04-09-CV_43Dpart/17.jpg


[18]: /assets/images/post_img/2023-04-09-CV_43Dpart/18.jpg
[19]: /assets/images/post_img/2023-04-09-CV_43Dpart/19.jpg

[20]: /assets/images/post_img/2023-04-09-CV_43Dpart/20.jpg
[21]: /assets/images/post_img/2023-04-09-CV_43Dpart/21.jpg

[22]: /assets/images/post_img/2023-04-09-CV_43Dpart/22.jpg
[23]: /assets/images/post_img/2023-04-09-CV_43Dpart/23.jpg

[24]: /assets/images/post_img/2023-04-09-CV_43Dpart/24.jpg
[25]: /assets/images/post_img/2023-04-09-CV_43Dpart/25.jpg

[26]: /assets/images/post_img/2023-04-09-CV_43Dpart/26.jpg
[27]: /assets/images/post_img/2023-04-09-CV_43Dpart/27.jpg

출처 : 2023-1 ITE4052 수업  






