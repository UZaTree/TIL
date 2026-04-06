# 자료형 & 연산

> 관련 주제: double, 나머지 연산, 조건문 최적화

---

## double - 소수점 정밀도

### 문제 (P1546)
`int` 간의 나눗셈은 소수점을 버립니다.

```java
int a = 5, b = 2;
System.out.println(a / b); // 2 (소수점 버림)
```

### 해결
연산 과정에 `double` 형이 포함되도록 합니다.

```java
double sum = 0;
for (int score : scores) {
    sum += (double) score / maxScore * 100; // 형 변환 후 나눗셈
}
double average = sum / N;
```

### 출력 주의
`System.out.println`으로 `double` 출력 시 오차가 생길 수 있습니다.  
문제 요구사항에 따라 `printf` 또는 `String.format` 사용을 고려합니다.

```java
System.out.printf("%.2f%n", average); // 소수점 2자리
System.out.println(String.format("%.2f", average));
```

---

## 나머지 연산 (%)

### 핵심
아주 큰 수의 계산에서 오버플로우를 막기 위해 중간중간 나머지를 구합니다.

```
(A + B) % C == ((A % C) + (B % C)) % C
```

```java
long result = ((a % MOD) + (b % MOD)) % MOD;
```

---

## 조건문 최적화

### 핵심
`if - else if` 구조에서 이미 상위 조건에서 걸러진 범위는 하위 조건에서 다시 검사하지 않아도 됩니다.

```java
// 비효율 (불필요한 중복 조건)
if (score >= 90) grade = "A";
else if (score >= 80 && score < 90) grade = "B"; // score < 90은 이미 보장됨

// 효율 (간결)
if (score >= 90) grade = "A";
else if (score >= 80) grade = "B";
else if (score >= 70) grade = "C";
```
