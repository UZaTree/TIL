## tar

`tar`는 여러 파일과 디렉터리를 하나의 `tar 파일`로 묶거나, `tar 파일`을 해제하는 명령어이다.


### 기본 사용법

`tar [option] [파일명]`

### 주요 옵션

| 옵션 | 설명 |
|---|---|
| `-c` | 새로운 tar 파일 생성(Create) |
| `-x` | tar 파일 해제(Extract) |
| `-v` | 처리되는 파일의 목록을 자세히 출력(Verbose) |
| `-f 파일명` | 사용할 tar 파일 지정(File) |
| `-r` | 기존 tar 파일에 파일 추가(append) |
| `-t` | tar 파일 내부의 파일 목록 출력(list) |
| `-h` | 심볼릭 링크 대신 링크가 가리키는 실제 파일을 저장 |
| `-C 디렉터리` | 지정한 디렉터리로 이동한 후 작업 수행 |
| `-p` | 파일의 권한 정보를 그대로 유지 |
| `-Z` | `compress`를 이용한 압축/해제 |
| `-z` | `gzip`을 이용한 압축/해제 |
| `-j` | `bzip2`를 이용한 압축/해제 |
| `-J` | `xz`를 이용한 압축/해제 |
| `--delete` | tar 파일에서 지정한 파일 삭제 |

### 주요 사용 예시

`tar -cvf archive.tar files/`

→ `files/` 디렉터리를 `archive.tar`라는 tar 파일로 묶는다.

`tar -xvf archive.tar`

→ `archive.tar`라는 tar 파일을 해제한다.

`tar -tvf archive.tar`

→ `archive.tar`의 파일 목록을 확인한다.

`tar -rvf archive.tar file.txt`

→ 기존 `archive.tar`에 `file.txt`를 추가한다.

`tar -czvf archive.tar.gz files/`

→ `files/`를 tar 파일로 묶은 후 `gzip`으로 압축한다.

`tar -xzvf archive.tar.gz`

→ `gzip`으로 압축된 tar 파일을 해제한다.

`tar -cjvf archive.tar.bz2 files/`

→ `bzip2`로 압축한다.

`tar -xjvf archive.tar.bz2`

→ `bzip2`로 압축된 tar 파일을 해제한다.

`tar -cJvf archive.tar.xz files/`

→ `xz`로 압축한다.

`tar -xJvf archive.tar.xz`

→ `xz`로 압축된 tar 파일을 해제한다.

> **시험 포인트**
>
> - `-c` → Create, tar 파일 생성
> - `-x` → Extract, tar 파일 해제
> - `-t` → tar 파일 내부 목록 확인
> - `-r` → 기존 tar 파일에 파일 추가
> - `-f` → tar 파일 지정
> - `-z` → gzip
> - `-j` → bzip2
> - `-J` → xz
> - `-C` → 작업 디렉터리 지정
> - `-p` → 권한 유지
> - `--delete` → tar 파일에서 파일 삭제

## compress / uncompress

### compress

`compress`는 파일을 **LZW 방식으로 압축**하는 명령어이다.

기본적으로 압축된 파일에는 `.Z` 확장자가 붙는다.

### 주요 옵션

| 옵션 | 설명 |
|---|---|
| `-c` | 압축 결과를 표준 출력으로 출력 |
| `-v` | 압축 진행 및 결과 정보를 자세히 출력 |

예:

`compress file`

→ `file.Z` 생성

### uncompress

`uncompress`는 `compress`로 압축된 `.Z` 파일을 **압축 해제**하는 명령어이다.

예:

`uncompress file.Z`

→ `file.Z`의 압축을 해제하여 `file` 생성

### 핵심 정리

`compress` → 압축 → `.Z`

`uncompress` → `.Z` 압축 해제

> **시험 포인트**
>
> - `compress` → LZW 압축
> - `uncompress` → `compress`로 압축된 `.Z` 파일 해제
> - `-c` → 표준 출력
> - `-v` → 자세한 정보 출력

## gzip / gunzip

### gzip

`gzip`은 파일을 **GNU zip 방식으로 압축**하는 명령어이다.

기본적으로 압축된 파일에는 `.gz` 확장자가 붙는다.

### 주요 옵션

| 옵션 | 설명 |
|---|---|
| `-d` | 압축 해제(decompress). `gunzip`과 동일 |
| `-1` | 가장 빠르게 압축. 압축률은 낮음 |
| `-9` | 가장 높은 압축률로 압축. 압축 속도는 느림 |
| `-c` | 압축 결과를 표준 출력으로 출력 |
| `-l` | 압축 파일의 정보 출력 |
| `-r` | 디렉터리 내부의 파일을 재귀적으로 압축 |
| `-v` | 압축 과정과 결과를 자세히 출력 |

예:

`gzip file`

→ `file.gz` 생성

`gzip -9 file`

→ 높은 압축률로 `file.gz` 생성

`gzip -d file.gz`

→ `file.gz` 압축 해제

### gunzip

`gunzip`은 `gzip`으로 압축된 `.gz` 파일을 **압축 해제**하는 명령어이다.

`gunzip file.gz`

→ `file.gz`를 압축 해제하여 `file` 생성

`gunzip`은 다음과 같이 `gzip -d`와 같은 역할을 한다.

`gzip -d file.gz`

`gunzip file.gz`

### 핵심 정리

`gzip` → `.gz`로 압축

`gunzip` → `.gz` 압축 해제

`gzip -d` → `.gz` 압축 해제

> **시험 포인트**
>
> - `-d` → 압축 해제(decompress)
> - `-1` → 가장 빠른 압축, 낮은 압축률
> - `-9` → 가장 높은 압축률, 느린 압축
> - `-c` → 표준 출력
> - `-l` → 압축 파일 정보 출력
> - `-r` → 디렉터리 내부를 재귀적으로 처리
> - `-v` → 자세한 정보 출력
> - `gzip -d` = `gunzip`

## bzip2 / bunzip2

### bzip2

`bzip2`는 파일을 **Burrows-Wheeler Block Sorting 방식과 Huffman Coding을 이용하여 압축**하는 명령어이다.

기본적으로 압축된 파일에는 `.bz2` 확장자가 붙는다.

### 주요 옵션

| 옵션 | 설명 |
|---|---|
| `-d` | 압축 해제(decompress). `bunzip2`와 동일 |
| `-1` | 가장 빠른 압축. 압축률은 낮음 |
| `-9` | 가장 높은 압축률로 압축. 압축 속도는 느림 |
| `-c` | 압축 결과를 표준 출력으로 출력 |
| `-f` | 기존 파일이 있더라도 강제로 덮어씀 |

예:

`bzip2 file`

→ `file.bz2` 생성

`bzip2 -9 file`

→ 높은 압축률로 `file.bz2` 생성

`bzip2 -d file.bz2`

→ `file.bz2` 압축 해제

### bunzip2

`bunzip2`는 `bzip2`로 압축된 `.bz2` 파일을 **압축 해제**하는 명령어이다.

`bunzip2 file.bz2`

→ `file.bz2`를 압축 해제하여 `file` 생성

`bunzip2`는 다음과 같이 `bzip2 -d`와 같은 역할을 한다.

`bzip2 -d file.bz2`

`bunzip2 file.bz2`

### 핵심 정리

`bzip2` → `.bz2`로 압축

`bunzip2` → `.bz2` 압축 해제

`bzip2 -d` → `.bz2` 압축 해제

> **시험 포인트**
>
> - `-d` → 압축 해제(decompress)
> - `-1` → 가장 빠른 압축, 낮은 압축률
> - `-9` → 가장 높은 압축률, 느린 압축
> - `-c` → 표준 출력
> - `-f` → 강제 덮어쓰기
> - `bzip2 -d` = `bunzip2`

## xz / unxz

### xz

`xz`는 파일을 **LZMA 계열 알고리즘을 사용하여 압축**하는 명령어이다.

기본적으로 압축된 파일에는 `.xz` 확장자가 붙는다.

### 주요 옵션

| 옵션 | 설명 |
|---|---|
| `-z` | 파일을 압축(compress) |
| `-d` | 압축 해제(decompress). `unxz`와 동일 |

예:

`xz file`

→ `file.xz` 생성

`xz -z file`

→ `file.xz`로 압축

`xz -d file.xz`

→ `file.xz` 압축 해제

### unxz

`unxz`는 `xz`로 압축된 `.xz` 파일을 **압축 해제**하는 명령어이다.

`unxz file.xz`

→ `file.xz`를 압축 해제하여 `file` 생성

`unxz`는 다음과 같이 `xz -d`와 같은 역할을 한다.

`xz -d file.xz`

`unxz file.xz`

### 핵심 정리

`xz` → `.xz`로 압축

`unxz` → `.xz` 압축 해제

`xz -d` → `.xz` 압축 해제

> **시험 포인트**
>
> - `-z` → 압축
> - `-d` → 압축 해제
> - `xz -d` = `unxz`

## gcc

`gcc`는 C 언어 소스 코드를 컴파일하는 GNU C Compiler이다.

### 기본 사용법

`gcc [option] 소스파일`

### 주요 옵션

| 옵션 | 설명 |
|---|---|
| `-o 파일명` | 생성되는 실행 파일의 이름을 지정 |
| `-c` | 소스 코드를 컴파일하여 오브젝트 파일(`.o`)까지만 생성하고 링크하지 않음 |

### 사용 예시

`gcc hello.c`

→ `hello.c`를 컴파일하여 기본 실행 파일 `a.out` 생성

`gcc -o hello hello.c`

→ `hello.c`를 컴파일하여 `hello`라는 실행 파일 생성

`gcc -c hello.c`

→ `hello.c`를 컴파일하여 `hello.o` 오브젝트 파일 생성

### 핵심 정리

`-o` → **출력 파일 이름 지정**

`-c` → **컴파일만 수행하고 링크하지 않음**

> **시험 포인트**
>
> - `gcc -o hello hello.c` → `hello` 실행 파일 생성
> - `gcc -c hello.c` → `hello.o` 오브젝트 파일 생성
> - `-c` 사용 시 링크 과정은 수행하지 않는다.

