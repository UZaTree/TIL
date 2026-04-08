# 제어문 (Control Flow)

> 관련 주제: switch, while, break

---

## switch 문

### 기본 문법
```java
int num = 2;

switch (num) {
    case 1:
        System.out.println("1입니다");
        break;
    case 2:
        System.out.println("2입니다");
        break;
    default:
        System.out.println("해당 없음");
        break;
}
```

### case에 넣을 수 있는 것
**컴파일 시점에 확정된 상수만 가능**

```java
case 1:           // 정수 ✅
case 'A':         // char ✅
case "hello":     // String ✅
case 10 + 5:      // 상수 연산 ✅

case n:           // 변수 ❌
case n > 0:       // 조건식 ❌
case Math.random(): // 런타임 값 ❌
```

### 사용 가능한 타입
```java
// 가능
int, char, String, enum

// 불가능
double, long
```

### fall-through (break 생략)
```java
switch (num) {
    case 1:
    case 2:
        System.out.println("1 또는 2"); // case 1, 2 둘 다 여기로
        break;
}
```
`break` 없으면 다음 `case`로 흘러내림 → **fall-through**

### Java 14+ 신문법 (switch expression)
```java
String result = switch (num) {
    case 1 -> "하나";
    case 2 -> "둘";
    default -> "기타";
};
```
> 백준은 Java 11 기준이라 못 쓰는 경우 있음

### if문과 비교
| | switch | if-else if |
|--|--|--|
| 적합한 경우 | 특정 값으로 분기 | 범위, 복합 조건 분기 |
| 가독성 | 값이 많을 때 좋음 | 범위 조건에 좋음 |

---

## while(true) + break

### 언제 쓰는가
종료 조건이 입력값에 달려있을 때 오히려 더 명확합니다.

```java
// 억지스러운 while 조건
while (a != 0 || b != 0) { // 초기값 설정 꼼수 필요

// 의도가 명확한 while(true)
while (true) {
    String[] tokens = br.readLine().split(" ");
    a = Integer.parseInt(tokens[0]);
    b = Integer.parseInt(tokens[1]);
    if (a == 0 && b == 0) break;
}
```

### 상황별 선택 기준
| 상황 | 추천 |
|--|--|
| 종료 조건이 명확한 경우 | `while(조건)` |
| 종료 조건이 입력값에 달린 경우 | `while(true)` + `break` |
| 실무 서버/백그라운드 | `while(true)` 지양 |

> 실무에서 지양하는 이유는 서버/백그라운드에서 CPU를 무한으로 잡아먹는 버그 위험 때문.  
> 백준에서는 종료 조건이 명확하므로 적절히 사용 가능.
