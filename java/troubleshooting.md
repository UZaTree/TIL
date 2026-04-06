# 주의사항 (Troubleshooting)

> 자주 하는 실수와 해결법 모음

---

## BufferedWriter.write(int) 주의

### 문제
정수형 `int`를 그대로 넣으면 숫자가 아닌 **ASCII 코드의 문자**가 출력됩니다.

```java
BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
bw.write(65); // "65"가 아닌 "A" 출력 (ASCII 65 = 'A')
```

### 해결
```java
bw.write(String.valueOf(65)); // "65" 출력
// 또는 StringBuilder 사용 권장
sb.append(65);
```

---

## throws IOException 누락

### 문제
`BufferedReader` 사용 시 컴파일 에러 발생

### 해결
```java
public static void main(String[] args) throws IOException { // 필수
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
}
```

---

## Integer.parseInt() 파싱 에러

### 문제
문자열에 공백이나 숫자가 아닌 문자가 섞여 있으면 `NumberFormatException` 발생

```java
Integer.parseInt("12 "); // 공백 포함 → 에러
```

### 해결
`StringTokenizer` 또는 `trim()`으로 미리 정제합니다.

```java
Integer.parseInt(br.readLine().trim());
// 또는
StringTokenizer st = new StringTokenizer(br.readLine());
int n = Integer.parseInt(st.nextToken());
```

---

## ArrayIndexOutOfBoundsException

### 문제
`N+1` 크기의 배열을 만들지 않았는데 인덱스 `N`에 접근할 때 발생

```java
int[] arr = new int[N];
arr[N] = 1; // 에러! 유효 인덱스는 0 ~ N-1
```

### 해결
문제 번호를 인덱스로 그대로 쓰고 싶다면 크기를 `N+1`로 선언합니다.

```java
int[] arr = new int[N + 1]; // 인덱스 1 ~ N 사용 가능
```
