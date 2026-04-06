# 입출력 (I/O)

> 관련 도구: `BufferedReader`, `StringBuilder`, `StringTokenizer`, `split()`

---

## BufferedReader

### 왜 쓰는가?
`Scanner`보다 내부 버퍼(8KB)가 커서 대량의 데이터를 읽을 때 속도가 압도적으로 빠릅니다.

### 구조
```
System.in (바이트 스트림)
  → InputStreamReader (문자 스트림)
    → BufferedReader (버퍼링)
```

### 기본 사용법
```java
import java.io.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        String s = br.readLine();           // 문자열 한 줄 읽기
        int n = Integer.parseInt(br.readLine()); // 정수 한 개 읽기
    }
}
```

> ⚠️ `throws IOException` 선언 필수

---

## StringBuilder

### 왜 쓰는가?
`String`은 불변(Immutable) 객체라 `+` 연산 시 매번 새 객체를 생성합니다.  
반복문에서 수천 번 합치면 메모리와 시간이 크게 낭비됩니다.  
`StringBuilder`는 가변(Mutable) 객체로 내부 버퍼에서 직접 수정하므로 성능이 뛰어납니다.

### 주요 메서드
```java
StringBuilder sb = new StringBuilder();

sb.append(i).append(" ");       // 끝에 추가 (반복 출력 최적화에 필수)
sb.insert(0, "[결과 리스트]\n"); // 특정 위치에 삽입
System.out.print(sb.toString()); // 최종 출력
```

---

## StringTokenizer vs split()

### 언제 무엇을 쓸까?

| | StringTokenizer | split() |
|--|--|--|
| 속도 | 빠름 | 약간 느림 |
| 가독성 | 떨어짐 | 좋음 |
| 실무 사용 | 거의 안 씀 | 자주 씀 |
| 내부 방식 | 단순 문자 비교 | 정규식 엔진 |

> 백준에서 입력값이 많고 시간 제한이 빡빡한 문제 → `StringTokenizer`  
> 그 외 일반적인 경우 → `split()`

### StringTokenizer 사용법
```java
import java.util.StringTokenizer;

StringTokenizer st = new StringTokenizer(br.readLine());

int a = Integer.parseInt(st.nextToken());
int b = Integer.parseInt(st.nextToken());
```

### split() 사용법
```java
// 기본
String[] tokens = br.readLine().split(" ");

// 정규식 활용
"1  2   3".split("\\s+");       // 공백 여러 개 처리 → ["1", "2", "3"]
"1,2 3:4".split("[,\\s:]");     // 여러 구분자 동시에 → ["1", "2", "3", "4"]
"1.2.3".split("\\.");           // 점(.)은 이스케이프 필수

// 정수 배열로 바로 변환 (실무 스타일)
int[] arr = Arrays.stream(br.readLine().split(" "))
                  .mapToInt(Integer::parseInt)
                  .toArray();
```

### split() 주의사항
```java
"1,,2".split(",");   // ["1", "", "2"]  빈 문자열 포함됨
"1,2,,".split(",");  // ["1", "2"]      뒤쪽 빈값은 자동 제거
"1.2.3".split(".");  // []              틀림! .은 정규식에서 '모든 문자'
```

---

## 토큰 역순 정렬

### 입력 순서 뒤집기
```java
List<String> list = new ArrayList<>(Arrays.asList(input.split(" ")));
Collections.reverse(list);
```

### 문자열 자체를 뒤집기
```java
String token = st.nextToken();
String reversed = new StringBuilder(token).reverse().toString();
```
