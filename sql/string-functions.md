# 문자 함수 (String Functions)

> 문자 컬럼 또는 문자열에 적용하는 내장 함수 모음

---

## CONCAT() — 문자 이어붙이기

```sql
-- 컬럼끼리 합치기
SELECT CONCAT(고객명, 고객등급) FROM card;

-- 컬럼 + 직접 입력한 문자 + 숫자 혼합 가능
SELECT CONCAT(고객명, ' is ', 사용금액) FROM card;
```

> PostgreSQL, Oracle 등은 `||` 기호 사용: `고객명 || ' is ' || 고객등급`
> SQL Server는 `+` 기호 사용

---

## TRIM() — 좌우 공백 제거

```sql
SELECT TRIM(컬럼명) FROM 테이블명;
```

---

## REPLACE() — 문자 치환

```sql
-- REPLACE(대상문자, 찾을문자, 바꿀문자)
SELECT REPLACE('서울에사는 서울맨', '서울', '경기');
-- 출력: '경기에사는 경기맨'
```

---

## SUBSTR() — 문자 추출

```sql
-- SUBSTR(대상문자, 시작위치, 추출할글자수)
SELECT SUBSTR('abcdef', 3, 2);
-- 출력: 'cd'
```

---

## INSERT() — 문자 교체

```sql
-- INSERT(대상문자, 시작위치, 교체할글자수, 바꿀문자)
SELECT INSERT('test@naver.com', 1, 4, 'hello');
-- 출력: 'hello@naver.com'
```

---

> `SELECT` 뒤에 컬럼명 없이 문자나 숫자만 넣어도 그대로 출력됨 — 함수 테스트할 때 유용
