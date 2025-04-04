# 2장. 테이블에서 데이터 검색

## 04강. Hello World 실행하기

### SELECT * FROM 테이블명 실행

- SQL 명령문은 스페이스로 구분하고, 마지막에 세미콜론(;)을 붙여야 실행
    
    ```sql
    SELECT * FROM 테이블명
    ```
    

### SELECT 명령 구문

- SELECT : 데이터베이스를 읽어오는 DML 명령어 == 질의, 쿼리
- SQL 명령어는 ‘구’라는 단위로 구분
    - 애스터리스트(*) : ‘모든 열’을 의미하는 메타문자
    - FROM : 처리 대상 테이블을 지정하는 명령어

### 예약어와 데이터베이스 객체명

- SELECT, FROM : 구를 결정하는 키워드, 예약어
- 데이터베이스는 같은 이름으로 다른 다른 데이터베이스 객체 생성 불가능
- 통상적으로 데이터베이스 객체명과 동일한 예약어 사용 불가능
- 예약어와 데이터베이스 객체명 대소문자 구분X

### Hello World를 실행한 결과 = 테이블

- SELECT 명령을 실행하면 ‘행(레코드)’과 ‘열(컬럼/필드)’로 구성된 표 형식의 데이터 출력
- 셀 : 테이블에서 각각의 행과 열이 만나는 부분, 하나의 데이터값 저장
- 데이터는 자료형으로 분류 가능
    - 열은 하나의 자료형만 가능
    - 수치형, 문자열형, 날짜시간형

### 값이 없는 데이터 = NULL

- NULL은 데이터가 들어있지 않은 것을 의미하는 특별한 값

---

## 05강. 테이블 구조 참조하기

### DESC 명령

- DESC 명령으로 테이블 구조 참조 가능
- `DESC 테이블명` 명령으로 테이블에 정의되어 있는 열 확인
    
    ```sql
    DESC 테이블명
    ```
    
    - Field : 열의 이름
    - Type : 해당 열의 자료형
    - Null : NULL 사용여부를 나타내는 제약사항
    - Key : 해당 열의 ‘키’ 지정 여부
    - Default : 기본값, 생략했을 경우 적용되는 값

### 자료형

- INTEGER : 정수값 저장(소수점 포함X), 수치형 자료형
- CHAR : 문자열 저장, 고정 길이 문자열 자료형
    - 열의 최대 길이 지정 필요
    - 최대 길이보다 작은 문자열 저장할 경우 공백문자로 나머지를 채워서 저장
- VARCHAR : 문자열 저장, 가변 길이 문자열 자료형
    - 열의 최대 길이 지정 필요
    - CHAR와 달리 데이터 크기에 맞춰 저장공간 크기 변경
- DATE : 날짜값 저장 자료형
- TIME : 시간 저장 자료형

---

## 06강. 검색 조건 지정하기

### SELECT 구에서 열 지정하기

- SELECT구에서 결과로 표시하고 싶은 열 지정
    
    ```sql
    SELECT 열1, 열2 ... FROM 테이블명
    ```
    

### WHERE 구에서 행 지정하기

- 구의 순서와 생략
    - WHERE구 : 행 속에서 필요한 데이터만 검색하기 위해 사용
    - SQL에서 정해진 구의 순서가 바뀌면 에러 발생
        - SELECT구 → FROM구 → WHERE구 순서
        - WHERE구 생략 가능, 생략 시 테이블 내 모든 행이 검색 대상
- WHERE구
    - WHERE구의 조건에 일치하는 행만 결과로 반환
        
        ```sql
        SELECT 열 FROM 테이블명 WHERE 조건식
        SELECT * FROM sample21 WHERE no=2;
        ```
        
        - 조건식은 열과 연산자, 상수로 구성되는 식
        - WHERE구로 행만 추출하지만 SELECT구로 열 지정 동시에 가능
- 조건식
    - 조건식은 ‘열과 연산자, 상수’로 구성
    - 조건식은 참 또는 거짓의 진리값을 반환하는 식으로 비교 연산자를 사용해 표현
        - 값이 서로 같은 경우 =
        - 값이 서로 다른 경우 <>
    - WHERE구에서 지정한 조건식에 따라 복수의 행 반환
        - 반드시 하나의 행 반환X
        - 조건식이 일치하는 행이 없는 경우 아무것도 반환X

### 문자열형의 상수

- 수치형 : 숫자 그대로 표기 (ex) no=2
- 리터럴(literal) : 자료형에 맞게 표기한 상수값
    - 문자열과 날짜시간형 모두 싱글쿼트(’ ‘)로 둘러싸 표기
    - 문자열형 (ex) name=‘박준용’
    - 날짜시간형 (ex) birthday=’2025-03-17 17:00’
        - 연월일은 하이픈(-)으로 구분
        - 시분초는 콜론(:)으로 구분

### NULL값 검색

- NULL값을 검색할 때 = 연산자가 아닌 IS NULL 사용
- NULL값이 아닌 행 검색할 때 IS NOT NULL 사용

### 비교 연산자

- =, <>, >, ≥, <, ≤

---

## 07강. 조건 조합하기

- 조건식을 조합해 사용할 경우 복수의 조건을 WHERE구로 지정
- 조합할 때는 AND, OR, NOT 사용

### AND로 조합하기

- AND로 조건식을 연결하면 모든 조건을 만족하는 행 검색 가능
- AND 연산자는 논리곱을 계산하는 논리 연산자로, 교집합으로 계산
    
    ```sql
    조건식1 AND 조건식2
    SELECT * FROM sample24 WHERE a<>0 AND b<>0;
    ```
    

### OR로 조합하기

- OR로 조건식을 연결하면 어느 쪽이든 조건을 만족하는 행을 모두 검색 가능
- OR 연산자는 논리합을 계산하는 논리 연산자로, 합집합으로 계산
    
    ```sql
    조건식1 OR 조건식2
    SELECT * FROM sample24 WHERE a<>0 OR b<>0;
    ```
    

### AND와 OR를 사용할 경우 주의할 점

- AND는 OR에 비해 우선순위가 높다
- a열이 1 또는 2이고, b열이 1 또는 2인 행 검색
    
    ```sql
    SELECT * FROM sample24 WHERE a<>0 AND b<>0;
    SELECT * FROM sample24 WHERE (a=1 OR a=2) AND (b=1 OR b=2);
    ```
    
    ❌ OR 조건식은 괄호로 묶어서 지정한 습관 추천
    
    ```sql
    SELECT * FROM sample24 WHERE a=1 OR a=2 AND b=1 OR b=2;
    SELECT * FROM sample24 WHERE a=1 OR (a=2 AND b=1) OR b=2;
    ```
    

### NOT으로 조합

- NOT 연산자는 오른쪽에만 항목을 지정하는 단항 연산자
- 오른쪽에 지정한 조건식의 반대 값 반환
- a열이 0이 아니거나 b열이 0이 아닌 행을 제외한 나머지 행을 검색
    
    ```sql
    SELECT * FROM sample24 WHERE NOT(a<>0 OR b<>0);
    ```
    

---

## 08강. 패턴 매칭에 의한 검색

- LIKE 술어를 사용하면 문자열의 일부분을 비교 가능
- 특정 문자나 문자열이 포함되어 있는지를 검색 : 패턴 매칭 / 부분 검색

### LIKE로 패턴 매칭하기

- LIKE 술어를 사용하면 패턴 매칭으로 검색 가능
    
    ```sql
    열명 LIKE '패턴'
    ```
    
- 와일드카드 == 메타문자
    - 패턴 매칭 시 임의의 문자 또는 문자열에 매치하는 부분을 지정하기 위해 사용하는 특수문자
    - 메타문자로 %와 _가 있다
        - % : 임의의 문자열
        - _ : 임의의 문자 하나
    - %는 임의의 문자열과 매치하며, 빈 문자열도 매치
        
        ```sql
        SELECT * FROM sample25 WHERE text LIKE 'SQL%';  // 전방 일치
        SELECT * FROM sample25 WHERE text LIKE '%SQL%'; // 중간 일치
        SELECT * FROM sample25 WHERE text LIKE '%SQL';  // 후방 일치
        ```
        

### LIKE로 %를 검색하기

- %를 LIKE로 검색할 경우 \%로 검색
- _를 LIKE로 검색할 경우 \_로 검색

### 문자열 상수 ‘의 이스케이프

- 문자열 상수를 검색할 때 메타문자를 검색할 때와 같은 문제 발생
- 문자열 상수는 ‘문자열’과 같이 ‘로 둘러싸 표기
- 문자열 상수 안에 ‘를 포함하는 경우 ‘를 2개 연속해서 표기
    
    ```sql
    It's -> 'It''s'
    ' -> ''''
    ```
    
- 간단한 패턴 매칭은 LIKE를 사용하고, 복잡한 패턴을 매칭하는 경우 정규 표현식 사용 추천

---

## Quiz

아래 쿼리 조건에 포함되지 않는 예시는?

```sql
SELECT * FROM example
WHERE name LIKE 'i%' OR name NOT LIKE 'p%' AND name LIKE '%ing';
```

1) ing

2) ping

3) king

4) inging