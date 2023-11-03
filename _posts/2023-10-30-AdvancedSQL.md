---
layout: post
title: Advanced SQL
subtitle: ITE2038 Database Systems
categories: Database
tags: [DB, ITE2038]
use_math: true
---

Key ideas :    
Advanced SQL   
SimpleDB Overview

---


Contents:   
- Fancy SQL
- Overview of SimpleDB

## Aliases(가명) and Ambiguity(애매모호함)
: 쿼리를 명확히 적어라

```sql
SELECT name
FROM keepers JOIN keeps ON id = kid
JOIN cages on cageno= no
JOIN animals on acageno=no
WHERE species = 'bear'
```

select name 부분어느 table인지도 모를 뿐아니라 animal, keepers 둘 다에 있음   
아래처럼 수정

```sql
SELECT animals.name
FROM keepers JOIN keeps ON id = kid
JOIN cages on cageno= no
JOIN animals on acageno=no
WHERE species = 'bear'
```

### Quiz

![1][1]

## Aggregation 
각 cage의 keeper 수 찾기.   
![5][5]
![6][6]
-> keeper가 0명인 cage는?

### Left Join
T1 LEFT JOIN T2 ON pred   
위의 명령어 통해서 pred를 만족하는 T1xT2뿐 아니라 T2의 field와 만족하지 않는 T1의 모든 row도 포함. (기존 join은 두 table중 한 쪽이라도 NULL이면 출력 안했음)

> practice (예제 생각많이 해보기!)   
![2][2]   
Q1.
![3][3]
![4][4]
Q2. count
![7][7]
![8][8]
-> 원하던 결과 아님!
![9][9]
![10][10]
COUNT(*), COUNT(col) 주의!


❗COUNT(*)는 NULL을 포함한 모든 row count함!   
COUNT(col)은 col의 non-null값 있는 row만 센다.

### Self Joins
>자기자신안의 데이터를 가져다 붙이는 경우.   
그냥 join은 보통 두 table의 결합을 의미.

Q. bear과 giraffe들을 keep하는 keeper는?
![11][11]
-> 위 쿼리로는 Bear와 Giraffe 동시에 keep 하는 keeper가 나오므로 원하는 결과 얻을 수 없다.

$\therefore$ 사육사 table은 1개 이지만, 곰키우는 사육사 table과 기린 키우는 사육사 table2개로 보고, self join 진행

![12][12]
-> 이런 형태 권장 X   
실수하기 쉽고, 디버깅 하기도 어려움 +논리적 생각도 어려움.   
꽤 간단한 내용임에도 7번의 join 사용됨.

$\therefore$ advanced SQL 사용.    
(nested query)

## Nested Queries
![13][13]

각 query는 relation(table)임. 따라서 tbale을 사용할 수 있는 모든곳에서 쿼리 사용할 수 있음.

이해와 디버깅 상대적으로 쉬움.    
but, 여전히 from()내부 길면 헷갈림.  
$\therefore$ CTE등장

### Simplify with Common Table Expressions (CTEs)
CTE가 여러곳에서 참조(referenced)되어야 하는 경우, nested expression보다 CTE가 더 잘 작동함.   

CTE의 문법:
```sql
WITH 테이블 이름 AS 테이블이 만들 쿼리문
```
- CTE는 temporarily 존재하는 쿼리의 set이다. following larger 쿼리에서만 사용.
- 더 readable. 그리고 이것이 쿼리 디버그 하기 용이하게 함 $\because$ 긴쿼리를 작은 쿼리로 break down
- CTE와 view의 차이는 "duration"   
한번만 쓸꺼면 CTE (임시)   
계속 볼꺼면 VIEW로 (영구)   
-> 둘 다 테이블로 존재하는 것 아님.   
기존 테이블에 대해 쿼리 수행 후 내가 필요한 결과만 가져오기.   
![14][14]

#### Example   
Q. Giraffe를 keep하는 keeper에게 kept되는 animal들?   
![15][15]
-> 주어진 table
![16][16]
-> CTE로 작성한 query 윗부분 설명
![17][17]
-> quert 아랫부분 그래프로 설명 

최종 output은, 
```
Sally | Student
Sam | Salamander
Sally | Student
Barry | Bear
```
중복(duplicate) 된다는 문제 발생!!

![18][18]

"Distinct"로 해결
![19][19]

## Recursive Queries (고급 Query #1)
- CTA를 더 어렵게 쓰면,    
어떤 동물이 아플 때, 그 사육사가 관리하는 (아플 가능성 있는) 다른 동물 구하는 등의 상황도 Recursive CTA로 어렵지 않게 구할 수 있다.
- 어떤 table을 기준으로 그 table이 계속 늘어나는 것.    
<u>새로운 table이 생기는 것 X</u>, 어떤 결과 table자체가 iteration 반복할 때 마다 커지게 되고, 언젠간 멈추게 됨.

![20][20]

- Recursive CTE: SELECT statement에서 자기자신 호출(reference itself)하여 loop 생성하는 CTE
- Recursive CTE는 hierarchical or graph based data구조에서 recursive 쿼리 수행할 수 있게 함. (예를 들어, organizational charts, family trees, transportaion networks ...)
![21][21]

### Example
![22][22]
![23][23]

### Example
- 회사 employee들의 hierarchical tree 생성해라

|id|name|department|manager_id|
|:---:|:---:|:---:|:---:|
|124|John Doe|IT|135|
|135|Jane Miller|HR|146|
|146|Sarah Smith|CEO|NULL|

위의 경우, 사람 증가시 한눈에 알기 어려움.   
$\therefore$ recursive CTE사용

```sql
WITH employee_manager_cte AS (
    SELECT id, name, department, manager_id, 1 AS level  
    FROM employees  
    WHERE manager_id IS NULL
UNION  ALL
    SELECT e.id, e.name, e.department, e.manager_id, level + 1 
    FROM employees e  
    INNER JOIN employee_manager_cte r ON e.manager_id = r.id
)
SELECT *FROM employee_manager_cte
```
Base case: 아무의 관리도 받지 않는 맨 꼭대기 사람 찾고, CEO가 관리하는 관리자 찾고, ...   
그들이 관리하는 사람 ...    
직원 바닥날 때 까지 반복. 언젠간 recursive CTE 멈출것임. ($\therefore$ stop condition 필요 X)


|id|name|department|manager_id|level|
|:---:|:---:|:---:|:---:|:---:|
|124|John Doe|IT|135|1|
|135|Jane Miller|HR|146|2|
|146|Sarah Smith|CEO|NULL|3|

❗ Recursive CTE쓸 때 항상 infinite loop 고민해보기! (멈출지 아닐지)   
항상 condition check


## Window Functions (고급 Query #2) ⭐
> WINDOW FUNCTION 종류 (벤더별로 지원하는 함수 차이가 있음)   
1.그룹 내 순위(RANK) 관련 함수: RANK, DENSE_RANK, ROW_NUMBER   
2.그룹 내 집계(AGGREGATE) 관련 함수 : SUM, MAX, MIN, AVG, COUNT (sql server는 OVER 절의 OREDER BY 지원 X)   
3.그룹 내 행 순서 관련 함수 : FIRST_VALUE, LAST_VALUE, LAG, LEAD (오라클에서만 지원)   
4.그룹 내 비율 관련 함수 : CUME_DIST, PERCENT_RANK, NTILE, RATIO_TO_REPORT    
5.선형 분석을 포함한 통계 분석 함수   
[참조](https://moonpiechoi.tistory.com/128)

### Example
동물원의 동물 1000마리 하루에 1번씩 밥 줄 떄, 밥주는 시간에 따라 0시~다음날 0시까지 누적하면?   
-> 밥주는 시간 전부 정렬 후 누적.    
: 이런 경우 Window function으로 간단히.

![24][24]
: Window function 안쓰는경우 이런 형태

형태
```sql
SELECT x, y, ... ,window_func(params)
OVER (PARTITION BY column1 ORDER BY column2)
```
ex1. 
```sql
SELECT hour_, minute_, RANK() OVER (ORDER BY hour_, minute_) FROM times_
```

ex2.    
animal로 split 후, 각 row 별로 rank 연산

```times_(hour_ int, minute_ int, animalid int)```
```sql
SELECT animalid hour_, minute_ RANK()
OVER (PARTITION BY animal ORDER BY hour_, minute) FROM times_
```

DB 내부에 함수 관련 최적화 O $\therefore$ 최적화 O

### Other Window Functions
- ```cume_dist()``` : 누적비율 구하기(전체분포에서 나의 누적 위치)    
0과 1 사이 결과(1000마리 중 50번째라면, 50/1000인 0.05로 결과나옴)
- ```lag(value, offset)``` : 나를 기준으로 *째 앞에 있는 것 (ex. 1주일 전(7일 전) 매출과의 비교 통해 1주일간 매출 차이 얻을 수 O)
- ```sum() / count() / avg()``` : 각 파티션의 row들 연산.    
이 표현들의 경우, OVER부분에서 포함되어야 할 파티션의 subset나타내기 위해 'frame' 포함할 수 있다.(전체를 보는게 아닌 "나를 기준으로 앞에 3개까지 보겠다"등 명시 가능)


#### practice
![25][25]
![26][26]

### SoIn
```sql
SELECT date, sales, sales -lag(sales,7)
OVER (ORDER BY   date) AS difference FROM sales
```
---

## What is SimpleDB
: basic 데이터베이스 시스템

>수업 목표: 데이터베이스 시스템이 어떤 구성 요소로 이루어져 있으며, 어떤 순서로 동작하고, 데이터가 들어오면 어떻게 처리하는지 과정 이해

- SQL front-end
    - Heap files 
    - Buffer Pool 
        > 캐시. 어떤 데이터 올려둘지. miss 덜나게
    - Basic Operators 
        - Scan, Filter, JOIN, Aggregate
        > 쿼리: 순서 기술 X. 원하는 목표만 기술
    - Query optimizer 
        > DBMS가 목표 성취 위해 가장 비용 적고 빠른 방법 찾기
    - Transactions 
        > multi user
    - B-Tree Indexes 
        > 쿼리들은 순서대로 접근 X. 랜덤 access.    
        임의 데이터 썼더라도 빨리 조회 위해 indexing, hashing 잘 해둬야 함
    - Recovery 
        > 손실X, 일관성 유지.

### Module diagram
![27][27]


<요소 설명은 생략..>   
Database, Catalog, BufferPool, HeapFile(ImplementsDbFile), HeapPage(Implements Page), SeqScan(Implements DbIterator)   
-> 필기 참고..


---

## 핵심
- Window functions


---
다음시간:
- Relational database design
- Normal forms
---

[1]: /assets/images/post_img/2023-10-30-AdvancedSQL/1.png
[2]: /assets/images/post_img/2023-10-30-AdvancedSQL/2.png
[3]: /assets/images/post_img/2023-10-30-AdvancedSQL/3.png
[4]: /assets/images/post_img/2023-10-30-AdvancedSQL/4.png
[5]: /assets/images/post_img/2023-10-30-AdvancedSQL/5.png
[6]: /assets/images/post_img/2023-10-30-AdvancedSQL/6.png
[7]: /assets/images/post_img/2023-10-30-AdvancedSQL/7.png
[8]: /assets/images/post_img/2023-10-30-AdvancedSQL/8.png
[9]: /assets/images/post_img/2023-10-30-AdvancedSQL/9.png
[10]: /assets/images/post_img/2023-10-30-AdvancedSQL/10.png
[11]: /assets/images/post_img/2023-10-30-AdvancedSQL/11.png
[12]: /assets/images/post_img/2023-10-30-AdvancedSQL/12.png
[13]: /assets/images/post_img/2023-10-30-AdvancedSQL/13.png
[14]: /assets/images/post_img/2023-10-30-AdvancedSQL/14.png
[15]: /assets/images/post_img/2023-10-30-AdvancedSQL/15.png
[16]: /assets/images/post_img/2023-10-30-AdvancedSQL/16.jpg
[17]: /assets/images/post_img/2023-10-30-AdvancedSQL/17.png
[18]: /assets/images/post_img/2023-10-30-AdvancedSQL/18.png
[19]: /assets/images/post_img/2023-10-30-AdvancedSQL/19.png

[20]: /assets/images/post_img/2023-10-30-AdvancedSQL/20.jpg
[21]: /assets/images/post_img/2023-10-30-AdvancedSQL/21.jpg
[22]: /assets/images/post_img/2023-10-30-AdvancedSQL/22.png
[23]: /assets/images/post_img/2023-10-30-AdvancedSQL/23.png
[24]: /assets/images/post_img/2023-10-30-AdvancedSQL/24.png
[25]: /assets/images/post_img/2023-10-30-AdvancedSQL/25.jpg
[26]: /assets/images/post_img/2023-10-30-AdvancedSQL/26.jpg
[27]: /assets/images/post_img/2023-10-30-AdvancedSQL/27.jpg
[28]: /assets/images/post_img/2023-10-30-AdvancedSQL/28.png
[29]: /assets/images/post_img/2023-10-30-AdvancedSQL/29.png

출처 : 2023-2 ITE2038 수업  






