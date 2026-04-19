# 집계 함수 (Aggregate Functions)

> 컬럼의 통계값을 구할 때 사용 — 필터링 후 사용 가능

---

## 기본 집계 함수

| 함수 | 설명 |
|------|------|
| `MAX(컬럼명)` | 최댓값 |
| `MIN(컬럼명)` | 최솟값 |
| `AVG(컬럼명)` | 평균 |
| `SUM(컬럼명)` | 합계 |
| `COUNT(컬럼명)` | 행 개수 — `COUNT(*)`도 결과 동일 |

```sql
SELECT MAX(사용금액) FROM card;
SELECT MIN(사용금액) FROM card;
SELECT AVG(연체횟수) FROM card;
SELECT SUM(사용금액) FROM card;
SELECT COUNT(사용금액) FROM card;
```

---

## AS — 컬럼명 별칭

집계 함수 사용 시 결과 컬럼명이 `MAX(사용금액)` 형태로 출력됨. `AS`로 원하는 이름으로 변경 가능

```sql
SELECT MAX(사용금액) AS 최대사용금액 FROM card;
```

> AS 뒤 별칭은 실제 컬럼명과 겹치지 않게 작명할 것. 나중에 서브쿼리 등에서 AS가 필수인 경우가 생기므로 사용법 익혀둘 것

---

## DISTINCT — 중복 제거

```sql
-- 중복 제거 후 출력
SELECT DISTINCT 연체횟수 FROM card;

-- 중복 제거 후 통계
SELECT AVG(DISTINCT 연체횟수) FROM card;
```

---

## 응용 — WHERE와 함께 사용

특정 그룹을 필터링한 뒤 통계를 내는 것이 전체 통계보다 의미 있는 경우가 많음

```sql
-- 고객등급이 vip인 사람의 평균 사용금액
SELECT AVG(사용금액) FROM card
WHERE 고객등급 = 'vip';
```

---

## 참고 — MAX/MIN 대신 LIMIT 쓰는 경우

인덱스가 있는 경우 `ORDER BY + LIMIT`이 더 빠를 수 있음. 상황에 따라 테스트 후 선택

```sql
-- 최댓값 조회 (두 방법 결과 동일)
SELECT MAX(사용금액) FROM card;
SELECT * FROM card ORDER BY 사용금액 DESC LIMIT 1;
```

> Oracle은 `LIMIT` 대신 `FETCH FIRST 1 ROWS ONLY` 사용
