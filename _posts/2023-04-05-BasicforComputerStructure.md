---
layout: post
title: ITE2031_컴퓨터구조론 기초
subtitle: 혼자 공부하는 컴퓨터 구조+운영체제
categories: 컴퓨터구조론
tags: [컴퓨터구조론, ITE2031]
---

## Chap1-2

컴퓨터의 두뇌인 CPU 내부에 ALU, 레지스터, 제어장치 있음.

ALU(Arithmetic Logic Unit)는 쉽게 말해 계산기.

레지스터는 CPU내부의 작은 임시저장장치

제어장치는 control signal이라는 전기신호 보내고 명령어 해석(추후 자세히. 현재는 CPU가 메모리에 저장된 값 읽고 싶을 땐 메모리 향해 ‘메모리 읽기’ 라는 제어신호 보낸다)

## Chap 2

### 정보단위

0과 1을 나타내는 가장 작은 정보단위 = 비트 bit

n비트는 2^n가지 정보 표현 가능

여덟개의 비트를 묶은 단위 = 바이트 byte

1바이트 1000개를 묶으면 = 1 킬로바이트 KB(kilobyte)

1000킬로바이트 = 1메가바이트

1000메가바이트 = 1기가바이트

1000기가바이트 = 1테라바이트

#### 워드

: CPU가 한번에 처리할 수 있는 데이터의 크기

CPU가 한번에 16비트를 처리할 수있다면 1워드는 16비트, 한번에 32비트 처리할 수 있다면 1워드는 32비트…

현대 컴퓨터의 워드 크기는 대부분 32비트 또는 64비트

## Chap 4-1 ALU와 제어장치

![1][1]  

### ALU

**ALU**는 레지스터를 통해 **피연산자**를 받아들이고, 제어장치로부터 수행할 연산을 알려주는 **제어신호**를 받아들인다.

제어장치와 레지스터로부터 받아들인 피연산자와 제어신호로 산술연산, 논리연산 등 다양한 연산 수행. 

결괏값은 레지스터에 저장. (CPU가 메모리에 접근하는 속도는 레지스터보다 훨씬 느림)

![2][2]  

ALU가 계산 결과와 더불어 내보내는 또 다른 정보에는 ‘**플래그**’가 있음

연산결과에 대한 추가 정보를 내보내야 할 때가 있음. 연산결과가 연산결과를 담을 레지스터보다 클 때 ‘결괏값이 너무 크다(오버플로우)’ 라는 추가정보를 내보낸다.

이러한 플래그는 CPU가 프로그램 실행 도중 반드시 기억해야 하는 일종의 참고정보

![3][3]  

(제어장치는 skip)

## Chap 5-3 CISC와 RISC

각기 다른 성격의 CPU의 언어인 **ISA**(Instruction set)를 기반으로 설계된 **CISC, RISC**

### CISC

complex instruction set computer의 약자 = ‘복잡한 명령어 집합을 활용하는 컴퓨터’를 의미

다양하고 강력한 기능의 명령어 집합을 활용하기 때문에 명령어의 형태와 크기가 다양한 **가변 길이 명령어**를 활용

다양하고 강력한 명령어를 활용한다는 말은 상대적으로 적은 수의 명령어로도 프로그램을 실행할 수 있다는 것을 의미.

프로그램을 실행하는 명령어 수가 적다는 것은 ‘컴파일된 프로그램의 크기가 작다’는 것을 의미. 같은 소스코드를 컴파일해도 CPU마다 생성되는 실행파일의 크기가 다를 수 있다는 것.

이런 장점으로 메모리 최대한 아끼며 개발해야 했던 시절에 인기 많았음

하지만, 활용하는 명령어 워낙 복잡하고 다양한 기능 제공해서 명령어의 크기와 실행 되기까지의 시간이 일정하지 않음. 

그리고 복잡한 명령어 때문에 명령어 하나를 실행하는 데에 여러 클럭 주기를 필요로 함. 이는 명령어 파이프라인 구현하는데 큰 걸림돌.(이상적인 명령어는 가급적 1클럭으로 소요시간 동일 해야 함) 이것이 현대 CPU에서 아주 치명적 약점.(명령어 파이프라인은 현대 CPU에서 높은 성능 위한 핵심기술)

## RISC

CISC로 하단 교훈 얻음

1. 빠른 처리를 위해 명령어 파이프라인 십분활용하고자, 명령어 길이와 수행시간이 짧고 규격화 되어있어야 한다
2. 자주 쓰이는 명령어만 많이 사용된다. 복잡한 기능을 지원하는 명령어 추가보다 ‘자주쓰이는 기본적인 명령어를 작고 빠르게 만드는 것’이 중요

위의 원칙 하에 등장한 것이 RISC(Reduced Instruction Set Computer)

- 이름처럼 CISC에 비해 명령어의 종류가 적다
- CISC와 달리 짧고 규격화된 명령어
- 되도록 1클럭 내외로 실행되는 명령어 지향

즉, RISC는 고정 길이 명령어를 활용.

(단순하고 적은 수의 고정길이 명령어 집합 사용)

명령어가 규격화 되어있고, 하나의 명령어가 1 클럭 내외로 실행되기 때문에 RISC 명령어 집합은 명령어 파이프라인에 최적화 되어있음.

RISC는 메모리에 직접 접근하는 명령어를 load, store 두개로 제한할 만큼 메모리 접근을 단순화 하고 최소화를 추구. 그렇기 떼문에 CISC보다 주소지정방식의 종류가 적은 경우가 많음.

(이런 점에서 RISC를 load-store구조라고 부르기도 함)

RISC는 메모리 접근을 단순화, 최소화 하는 대신 레지스터 적극 활용.

따라서 CISC보다 레지스터를 이용하는 연산이 많고, 일반적인 경우보다 범용 레지스터 개수도 더 많음.

다만 사용가능한 명령어의 개수가 CISC보다 적기 때문에 RISC는 CISC보다 많은 명령으로 프로그램을 작동시킴.

![4][4]  

정리\)
- ISA: CPU의 언어이자 하드웨어가 소프트웨어를 어떻게 이해할지에 대한 약속
- CISC: 복잡하고 다양한 종류의 가변 길이 명령어 집합을 활용한다
- RISC: 단순하고 적은 종류의 고정 길이 명령어 집합을 활용한다

---

### **MIPS 명령어 모음**

**< 논리,연산 >**

**add** (add)  :                add $s1 $s2 $s3  ->    $s1 = $s2 + $s3             -    더한다.

**sub** (subtract)  :           sub $s1 $s2 $s3  ->    $s1 = $s2 - $s3        -    뺀다.

**addi** (add immediate)  : addi $s1 $s2 10  ->    $s1 = $s2 + 10      -  상수를 더할때 주로 쓴다.

**lw** (load word)  :          lw $s1, 20($s2)  ->      $s1 = Memory[$s2+20]   - 메모리에서 레지스터로 load한다.

**sw** (store word) :         sw $s1, 20($s2)  ->      Memory[$s2+20]           - 레지스터에서 메모리로 store한다.

**and** (and) :                and $s1, $s2, $s3 ->     $s1 = $s2 & $s3            - s2와 s3의 and 값을 s1에 저장한다.

**or** (or) :                     or $s1, $s2, $s3 ->       $s1 = $s2 \| $s3            - s2와 s3의 or 값을 s1에 저장한다.

**sll** (shift left logical) :    sll $s1, $s2, 10  ->       $s1 = $s2 <<10           - s1 은 s2을 10만큼 좌비트이동 한것이다.

**srl** (shift right logical) :  srl $s1, $s2, 10  ->       $s1 = $s2 >>10           - s1 은 s2을 10만큼 좌비트이동 한것이다.

**< 조건 >**

**beq** (branch on equal) :       beq $s1, $s2, 25 ->     if($s1 == $s2) go to PC+4+100  - s1=s2 면 25로 이동한다.

**bne** (branch on  not equal) : beq $s1, $s2, 25 ->     if($s1 != $s2) go to PC+4+100   - s1!=s2 면 25로 이동한다.

**slt** (set on less than) :          slt $s1, $s2, $s3  ->    if($s2 < $s3) $s1 =1 else $s1 = 0 - s1<s2 만족하면 1 아니면 0

**j** (jump) :                          j  2500              ->    go to 10000                           - 목표 주소로 점프한다.

**jr** (jump register)                jr  $ra               ->    go to $ra                               - For switch, procedure return

**jal** (jump and link)              jal 2500             ->    $ra = PC + 4 ; go to 10000       - resgister 로 점프하여 링크


---

[출처1 ](http://www.yes24.com/Product/Goods/111378840) 혼자 공부하는 컴퓨터 구조+운영체제

[출처2 ](https://programming119.tistory.com/41) https://programming119.tistory.com/41




[1]: https://github.com/yoominlee/img/blob/main/2023-04-05-BasicforComputerStructures/1.jpg?raw=true
[2]: https://github.com/yoominlee/img/blob/main/2023-04-05-BasicforComputerStructure/2.jpg?raw=true
[3]: https://github.com/yoominlee/img/blob/main/2023-04-05-BasicforComputerStructure/3.jpg?raw=true
[4]: https://github.com/yoominlee/img/blob/main/2023-04-05-BasicforComputerStructure/4.jpg?raw=true



