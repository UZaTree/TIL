# 자료형 & 연산

> 관련 주제: double, 나머지 연산, 조건문 최적화, 제곱, 진법 변환

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

### double → int 변환
```java
double d = 8.9;
int n = (int) d;             // 8 → 소수점 버림 (반올림 아님)
int n = (int) Math.round(d); // 9 → 반올림
```

### 출력 주의
`System.out.println`으로 `double` 출력 시 오차가 생길 수 있습니다.  
문제 요구사항에 따라 `printf` 또는 `String.format` 사용을 고려합니다.

```java
System.out.printf("%.2f%n", average); // 소수점 2자리
System.out.println(String.format("%.2f", average));
```

---

## int vs long

| | int | long |
|--|--|--|
| 범위 | 약 -21억 ~ 21억 | 약 -922경 ~ 922경 |
| 사용 | 일반적인 경우 | 21억 넘을 것 같을 때 |

**long을 써야 하는 경우**
- 입력값이 10억 이상
- "결과가 매우 클 수 있다"
- 팩토리얼, 피보나치 등 누적 곱셈
- 두 수의 곱을 구하는 경우

```java
int a = 1_000_000_000;
int b = 1_000_000_000;
System.out.println(a + b);  // -294967296 → 오버플로우!

long a = 1_000_000_000L;
long b = 1_000_000_000L;
System.out.println(a + b);  // 2000000000 → 정상
```

> 헷갈리면 그냥 `long` 써도 백준에서 문제 없음

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

## 제곱 (Math.pow)

Java에서 `^`는 제곱이 아닌 **XOR 비트 연산자**입니다.

```java
Math.pow(2, 3);                    // 2의 3승 = 8.0 (double 반환)
int result = (int) Math.pow(2, 3); // 8 (int로 형변환 필요)
Math.sqrt(16);                     // 4.0 (제곱근)
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

---

## 진법 변환

### N진법 → 10진법 (P2745)
```java
String N = st.nextToken();
int B = Integer.parseInt(st.nextToken());
String reverse = new StringBuilder(N).reverse().toString();
double sum = 0;

for (int i = 0; i < reverse.length(); i++) {
    char c = reverse.charAt(i);
    if (Character.isDigit(c)) {
        sum += (c - '0') * Math.pow(B, i);
    } else {
        sum += (c - 55) * Math.pow(B, i); // A=65, 65-55=10
    }
}
System.out.println((int) sum);
```

### 10진법 → N진법 (P11005)
```java
while (quotient > 0) {
    int remainder = quotient % B;
    if (remainder >= 10) {
        sb.append((char) (remainder + 55)); // 10→A, 11→B ...
    } else {
        sb.append(remainder);
    }
    quotient /= B;
}
System.out.println(sb.reverse().toString());
```

> 알파벳 변환 공식: `char - 55` (A=65, 65-55=10) / `remainder + 55`
