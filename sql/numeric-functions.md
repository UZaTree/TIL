# 숫자 함수 (Numeric Functions)

> 숫자 데이터에 적용하는 내장 함수 모음

---

## GREATEST / LEAST — 여러 값 중 최대/최소

```sql
SELECT GREATEST(5, 3, 2, 1, 4);  -- 5
SELECT LEAST(5, 3, 2, 1, 4);     -- 1
```

> `MAX()` / `MIN()`은 하나의 컬럼 전체 행에서 최대/최소를 구하고,
> `GREATEST()` / `LEAST()`는 하나의 행 안에서 여러 값을 비교

---

## FLOOR / CEIL — 내림 / 올림

```sql
SELECT FLOOR(10.1);  -- 10
SELECT FLOOR(10.9);  -- 10
SELECT CEIL(10.1);   -- 11
SELECT CEIL(10.9);   -- 11
```

---

## ROUND / TRUNCATE — 반올림 / 버림

```sql
-- ROUND(숫자, 자릿수)
SELECT ROUND(10.777, 2);     -- 10.78

-- TRUNCATE(숫자, 자릿수)
SELECT TRUNCATE(10.777, 2);  -- 10.77
```

> Oracle, PostgreSQL은 `TRUNCATE()` 대신 `TRUNC()` 사용

---

## POWER — 거듭제곱

```sql
SELECT POWER(4, 2);  -- 16
```

---

## ABS — 절댓값

```sql
SELECT ABS(-100);  -- 100
```
