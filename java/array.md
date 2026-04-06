# 배열 제어

> 관련 주제: Swap, Reverse, 인덱스 매핑, 중복 체크

---

## Swap (값 교환)

### 핵심
데이터를 덮어쓰기 전에 임시로 저장할 `temp` 변수가 반드시 필요합니다.

```java
int temp = arr[i];
arr[i] = arr[j];
arr[j] = temp;
```

---

## Reverse (구간 역순 뒤집기)

### 핵심
구간 `[i, j]`를 뒤집을 때는 **절반까지만** 반복하며 양 끝 값을 서로 바꿉니다.

```java
// P10811 - 바구니 뒤집기
for (int k = 0; k <= (j - i) / 2; k++) {
    int tmp = arr[i + k];
    arr[i + k] = arr[j - k];
    arr[j - k] = tmp;
}
```

---

## 인덱스 매핑 전략

### 문제 (P10810)
바구니 번호는 1~N인데 배열 인덱스는 0~N-1이라 매번 `-1` 변환이 필요합니다.

### 해결
배열 크기를 `N + 1`로 선언하여 인덱스 1번부터 사용합니다.  
문제의 번호를 그대로 인덱스로 쓸 수 있어 코드가 직관적입니다.

```java
int[] arr = new int[N + 1]; // 0번 인덱스는 버림
arr[1] ~ arr[N] 사용
```

---

## 중복 체크 (서로 다른 값의 개수)

### 기초 방법 (P3052)
이중 `for`문으로 현재 값이 이전에 나타난 적 있는지 전수 조사합니다.

```java
int count = 0;
for (int i = 0; i < n; i++) {
    boolean isDuplicate = false;
    for (int j = 0; j < i; j++) {
        if (arr[i] == arr[j]) {
            isDuplicate = true;
            break;
        }
    }
    if (!isDuplicate) count++;
}
```

### 심화 방법 (추후 학습)
- `boolean` 배열을 인덱스로 활용
- `HashSet` 사용 → 더 빠르고 간결
