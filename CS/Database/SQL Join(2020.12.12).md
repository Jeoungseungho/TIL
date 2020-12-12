# SQL Join(2020.12.12)

## Join? 
조인이란 두개 이상의 테이블이나 **데이터버이스를 연결하여 데이터를 검색하는 방법**이다. 자신이 검색하고 싶은 칼럼이 다른 테이블에 있을 경우 주로 사용 하며 여러개의 테이블을 마치 하나의 테이블인 것처럼 활용하는 방법이다. 보통 Primary key 혹은 Foreign Key로 두 테이블을 연결한다. 테이블을 연결하려면 적어도 하나의 칼럼은 서로 공유되고 있어야 한다. 

## JOIN의 종류 

```sql
문법
SELECT
테이블별칭.조회할컬럼,
테이블별칭.조회할컬럼
FROM 기준테이블 별칭
INNER JOIN 조인테이블 별칭 ON 기준테이블별칭.기준키 = 조인테이블별칭.기준키 ...
```

### 1) INNER JOIN
<img width="515" alt="스크린샷 2020-12-12 오후 8 18 49" src="https://user-images.githubusercontent.com/44199159/101982442-476dec00-3cb7-11eb-858e-b959b737ad0c.png">

- 쉽게 말해 교집합이라고 생각하면 된다. 
- 기준 테이블과 Join한 테이블의 **중복된 값**을 보여준다.
- 결과값은 A의 테이블과 B의 테이블이 모두 가지고 있는 데이터만 검색된다. 

```sql
SELECT
A.NAME, 
B.AGE
FROM EX_TABLE A
INNER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```

### 2) LEFT OUTER JOIN 

<img width="488" alt="스크린샷 2020-12-12 오후 8 31 44" src="https://user-images.githubusercontent.com/44199159/101982680-11316c00-3cb9-11eb-8d29-43de9c062581.png">

- **기존 테이블의 값 + 테이블과 기준 테이블의 중복된 값**을 보여준다. 
- 왼쪽 테이블을 기준으로 Join을 하겠다고 생각하면 된다. 
- 결과값은 A 테이블의 모든 값과 A 테이블과 B 테이블의 중복되는 값이 검색된다. 

```sql
SELECT
A.NAME,
B.AGE
FROM EX_TABLE A
LEFT OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP

```

### 3) RIGHT OUTER JOIN
![스크린샷 2020-12-12 오후 8 38 56](https://user-images.githubusercontent.com/44199159/101982847-14792780-3cba-11eb-80b9-cbd1263b432b.png)

- LEFT OUTER JOIN의 반대이다. 
- 오른쪽 테이블을 기준으로 JOIN을 하겠다고 생각하면 된다. 
- 결과값은 B 테이블의 모든 데이터와 A 테이블과 B 테이블에서 중복되는 값이 검색된다. 

```sql
SELECT
A.NAME,
B.AGE
FROM EX_TABLE A
RIGHT OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP

```

### 4) FULL OUTER JOIN 
<img width="514" alt="스크린샷 2020-12-12 오후 8 46 57" src="https://user-images.githubusercontent.com/44199159/101983005-30c99400-3cbb-11eb-9c04-386293b8d297.png">

- 쉽게 말해 **합집합이다.**
- A 테이블이 가지고 있는 데이터, B 테이블이 가지고 있는 데이터 모두 검색된다. 
- 사실상, 기즌 테이블의 의미가 없다. 

```sql
SELECT
A.NAME,
B.AGE
FROM EX_TABLE A
FULL OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```
### 5) CROSS JOIN
<img width="459" alt="스크린샷 2020-12-12 오후 8 50 48" src="https://user-images.githubusercontent.com/44199159/101983072-bb11f800-3cbb-11eb-8adc-cb6b0312629b.png">

- **모든 경우의 수를 전부 표현해 주는 방식**이다. 
- 기준 테이블이 A일 경우, A의 데이터 한 ROW를 B 테이블의 전체와 조인하는 방식이다. 
- 결과값은 N*M이다.
- 위의 경우 A 테이블에 데이터가 3개 B 테이블에 데이터가 4개가 있으므로 총 12개가 검색된다. 

```sql
--첫 번째 방식--
SELECT
A.NAME,
B.AGE
FROM EX_TABLE A
CROSS JOIN JOIN_TABLE B

--두 번째 방식--
SELECT
A.NAME,
B.AGE
FROM EX_TABLE A, JOIN_TABLE B
```
### 6) SELF JOIN
![스크린샷 2020-12-12 오후 9 03 43](https://user-images.githubusercontent.com/44199159/101983297-899a2c00-3cbd-11eb-96e1-e010fd4b2a75.png)

- 자기 자신과 자기 자신을 조인한다는 의미이다.
- 하나의 테이블을 여러번 복사해서 조인한다고 생각하면 된다.
- 자신이 가지고 있는 칼럼을 다양하게 변형시켜 활용할 경우에 자주 사용한다. 

```sql
SELECT
A.NAME,
B.AGE
FROM EX_TABLE A, EX_TABLE B
```
