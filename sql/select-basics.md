# SELECT 기본 문법

> 테이블에서 데이터를 조회하는 가장 기본적인 SQL 문법

---

## SELECT / FROM

```sql
-- 모든 컬럼 조회
SELECT * FROM 테이블명

-- 특정 컬럼만 조회
SELECT 컬럼명 FROM 테이블명

-- 여러 컬럼 동시 조회
SELECT 컬럼명1, 컬럼명2 FROM 테이블명

-- 데이터베이스 명시
SELECT * FROM 데이터베이스명.테이블명
```

> 조회가 안 될 경우 `데이터베이스명.테이블명` 형식으로 명시해줄 것

**외우는 법**: SELECT, FROM → "**셀프**"로 기억 (데이터 뽑을 땐 셀프로)

### 대소문자 관련
- `SELECT`, `FROM` 등 키워드는 소문자로 써도 동작함
- 대문자 관습은 색상 하이라이트가 없던 시절의 흔적
- DBeaver에서 자동으로 대문자로 바꾸려면: `윈도우 > 설정 > SQL 편집기 > SQL 포맷 > Keyword case : Upper`

---

## ORDER BY

```sql
-- 오름차순 (기본값, ASC 생략 가능)
SELECT * FROM 테이블명 ORDER BY 컬럼명 ASC

-- 내림차순
SELECT * FROM 테이블명 ORDER BY 컬럼명 DESC

-- 다중 정렬 (컬럼1 기준 정렬 후, 같은 값끼리 컬럼2 기준 재정렬)
SELECT * FROM 테이블명 ORDER BY 컬럼명1 ASC, 컬럼명2 DESC

-- 컬럼 번호로 정렬 (3번째 컬럼 기준)
SELECT * FROM 테이블명 ORDER BY 3 DESC
```

| 키워드 | 정렬 방식 | 예시 |
|--------|-----------|------|
| ASC | 오름차순 | 1, 2, 3 / A, B, C |
| DESC | 내림차순 | 3, 2, 1 / C, B, A |

> `ORDER BY 컬럼번호` 방식은 편리하지만, 컬럼 순서가 바뀌면 의도와 다르게 동작할 수 있으니 주의
