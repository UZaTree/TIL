# 문자 처리 (char & String)

> 관련 주제: 아스키코드, Character 메서드, char 배열, 문자 분류

---

## 아스키코드

```
A = 65,  Z = 90
a = 97,  z = 122
0 = 48,  9 = 57
```

### Java에서 char 연산
```java
char c = 'A';
System.out.println((int) c);      // 65
System.out.println((char)(c + 1)); // B

// 대소문자 변환 (차이: 32)
char upper = 'A';
char lower = (char)(upper + 32);  // 'a'
```

---

## char vs int 출력 주의

```java
char c = 65;
System.out.println(c);  // A → char는 문자로 출력

int n = 65;
System.out.println(n);  // 65 → int는 숫자로 출력
```

### StringBuilder append 시
```java
sb.append((char) 65); // A
sb.append(65);        // 65
```

---

## String → char 변환 흐름

```
nextToken() → String → charAt(i) → char → Character.is~~()
```

```java
String token = st.nextToken();

for (int i = 0; i < token.length(); i++) {
    char c = token.charAt(i);

    if (Character.isDigit(c)) {
        // 숫자 처리
        int num = c - '0'; // 실제 숫자값으로 변환
    } else if (Character.isLetter(c)) {
        // 문자 처리
    }
}
```

> `char`로 저장된 `'1'`은 실제 숫자 `1`이 아님. 숫자로 쓰려면 `- '0'` 필요

---

## Character 주요 메서드

| 메서드 | 설명 |
|------|------|
| `Character.isDigit(c)` | 숫자인지 확인 |
| `Character.isLetter(c)` | 문자인지 확인 |
| `Character.isUpperCase(c)` | 대문자인지 확인 |
| `Character.isLowerCase(c)` | 소문자인지 확인 |

> `String` 전체에는 사용 불가, 반드시 `char`로 꺼낸 후 사용

---

## 알파벳 ↔ 숫자 변환 (진법 계산용)

```java
// 알파벳 → 숫자 (A=10, B=11 ...)
int value = c - 55; // A(65) - 55 = 10

// 숫자 → 알파벳 (10=A, 11=B ...)
char alpha = (char)(remainder + 55);
```
