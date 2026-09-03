## 소스 코드 컴파일 및 설치

Linux에서 소스 프로그램을 설치하는 일반적인 5단계는 다음과 같다.

`압축 풀기 → 디렉터리 이동 → configure → make → make install`

### configure

`configure`는 **설정(Configuration) 단계**이다.

현재 시스템의 환경과 필요한 라이브러리 등을 검사하고, 해당 시스템에 맞게 **컴파일에 필요한 설정을 생성**한다.

예:

    ./configure

설치 경로 등을 직접 지정할 수도 있다.

    ./configure --prefix=/usr/local

> **시험 포인트**
>
> `configure` → 시스템 환경을 검사하고 **컴파일에 필요한 설정을 생성**

### make

`make`는 `configure`에서 생성된 설정을 바탕으로 **소스 코드를 컴파일**한다.

예:

    make

소스 코드가 컴파일되어 실행 파일 등 설치에 필요한 결과물이 생성된다.

> **시험 포인트**
>
> `make` → 소스 코드 **컴파일**

### make install

`make install`은 `make`를 통해 생성된 결과물을 **지정된 설치 경로에 설치**한다.

예:

    make install

일반적으로 `configure`에서 지정한 `--prefix` 등의 설치 경로를 기준으로 파일이 설치된다.

> **시험 포인트**
>
> `make install` → 컴파일된 프로그램 **설치**

### 전체 과정

    소스 코드 압축 파일
          ↓
    압축 풀기
          ↓
    소스 코드 디렉터리 이동
          ↓
    ./configure
          ↓
    시스템 환경 검사 및 빌드 설정 생성
          ↓
    make
          ↓
    소스 코드 컴파일
          ↓
    make install
          ↓
    프로그램 설치

### 핵심 정리

| 단계 | 의미 |
|---|---|
| `configure` | **설정(Configuration)** |
| `make` | **컴파일** |
| `make install` | **설치** |

`configure → make → make install`

**설정 → 컴파일 → 설치**

## CMake

CMake는 소스 코드를 직접 컴파일하는 컴파일러가 아니라, **빌드 시스템을 생성하고 관리하는 도구**이다.

프로젝트의 소스 코드와 빌드 설정을 바탕으로 해당 운영체제와 컴파일러 환경에 맞는 빌드 파일을 생성한다.

### CMake 특징

- 여러 운영체제와 컴파일러를 지원하는 **플랫폼 독립적인 빌드 시스템**
- `CMakeLists.txt` 파일을 사용하여 프로젝트의 빌드 설정을 관리
- Makefile뿐만 아니라 다양한 빌드 시스템을 위한 빌드 파일을 생성할 수 있음
- 프로젝트의 라이브러리 및 의존성 설정을 관리할 수 있음
- 대규모 프로젝트의 빌드 과정을 관리하기에 적합
- C, C++, Fortran 등의 언어를 지원

### CMake 기본 동작 과정

일반적인 CMake 프로젝트는 다음과 같은 과정으로 빌드한다.

    소스 코드
        ↓
    CMakeLists.txt
        ↓
    cmake
        ↓
    빌드 시스템 생성
        ↓
    make 또는 다른 빌드 도구
        ↓
    실행 파일 생성

> **시험 포인트**
>
> `CMake` → 빌드 시스템을 생성하고 관리하는 도구
>
> `CMakeLists.txt` → CMake 프로젝트의 빌드 설정 파일
>
> CMake 자체가 컴파일러는 아니다.

### CMake를 채택한 주요 프로젝트

| 프로젝트 | 설명 |
|---|---|
| LLVM | 컴파일러 인프라 프로젝트 |
| Qt | 크로스 플랫폼 애플리케이션 개발 프레임워크 |
| OpenCV | 컴퓨터 비전 라이브러리 |
| KDE | Linux 및 Unix 계열 데스크톱 환경 |
| MySQL | 관계형 데이터베이스 관리 시스템 |
| VTK | 3D 그래픽 및 시각화 라이브러리 |

## tar

`tar`는 여러 파일과 디렉터리를 하나의 아카이브 파일로 묶거나, 아카이브 파일을 해제하는 명령어이다.

### 기본 사용법

`tar [option] [파일명]`

### tar의 특징

`tar`는 원본 파일이나 디렉터리를 삭제하거나 이동하는 것이 아니라 **복사하여 tar 파일로 묶기 때문에 원본이 그대로 보존된다.**

따라서 여러 파일과 디렉터리를 하나의 tar 파일로 묶어 **백업 용도**로 사용할 수 있다.

> **시험 포인트**
>
> `tar` → 원본 파일은 그대로 보존하면서 tar 파일 생성 → **백업 용도로 활용 가능**

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

### gunzip

`gunzip`은 `gzip`으로 압축된 `.gz` 파일을 **압축 해제**하는 명령어이다.

`gunzip file.gz`

→ `file.gz`를 압축 해제하여 `file` 생성

`gunzip`은 다음과 같이 `gzip -d`와 같은 역할을 한다.

`gzip -d file.gz`

`gunzip file.gz`

## bzip2 / bunzip2

### bzip2

`bzip2`는 파일을 **Burrows-Wheeler Block Sorting 방식과 Huffman Coding을 이용하여 압축**하는 명령어이다.

기본적으로 압축된 파일에는 `.bz2` 확장자가 붙는다.

### bunzip2

`bunzip2`는 `bzip2`로 압축된 `.bz2` 파일을 **압축 해제**하는 명령어이다.

`bunzip2 file.bz2`

→ `file.bz2`를 압축 해제하여 `file` 생성

`bunzip2`는 다음과 같이 `bzip2 -d`와 같은 역할을 한다.

`bzip2 -d file.bz2`

`bunzip2 file.bz2`

## xz / unxz

### xz

`xz`는 파일을 **LZMA 계열 알고리즘을 사용하여 압축**하는 명령어이다.

기본적으로 압축된 파일에는 `.xz` 확장자가 붙는다.

### unxz

`unxz`는 `xz`로 압축된 `.xz` 파일을 **압축 해제**하는 명령어이다.

`unxz file.xz`

→ `file.xz`를 압축 해제하여 `file` 생성

`unxz`는 다음과 같이 `xz -d`와 같은 역할을 한다.

`xz -d file.xz`

`unxz file.xz`

## zip / unzip

### zip

`zip`은 파일과 디렉터리를 **ZIP 형식으로 압축**하는 명령어이다.

기본적으로 압축 파일에는 `.zip` 확장자가 붙는다.

### unzip

`unzip`은 ZIP 형식으로 압축된 파일을 **압축 해제**하는 명령어이다.

## gcc

`gcc`는 C 언어 소스 코드를 컴파일하는 GNU C Compiler이다.

### 기본 사용법

`gcc [option] 소스파일`

## 컴파일과 링크

### 컴파일

컴파일은 **소스 코드를 컴퓨터가 이해할 수 있는 형태로 변환하는 과정**이다.

컴파일 자체가 프로그램을 실행하는 것은 아니다.

소스 코드 → 컴파일 → 목적 파일(Object File)

### 목적 파일

GCC에서 `-c` 옵션을 사용하면 소스 코드를 컴파일하여 **목적 파일(Object File)만 생성하고 링크는 수행하지 않는다.**

    gcc -c hello.c

결과:

    hello.c
      ↓
    컴파일
      ↓
    hello.o

`.o` 파일은 윈도우에서 C/C++ 프로그램을 빌드할 때 생성되는 `.obj` 파일과 비슷한 역할을 한다.

### 링크

링크(Link)는 여러 목적 파일과 필요한 라이브러리 등을 연결하여 **최종 실행 파일을 만드는 과정**이다.

    main.o
    필요한 라이브러리
          ↓
        링크
          ↓
      실행 파일

예:

    gcc hello.o -o hello

→ `hello.o`를 링크하여 `hello` 실행 파일을 생성한다.

### Windows와 비교

Windows에서 C/C++ 프로그램을 빌드하는 과정을 단순화하면 다음과 같이 이해할 수 있다.

    hello.c
      ↓
    컴파일
      ↓
    hello.obj
      ↓
    링크
      ↓
    hello.exe

Linux + GCC에서는:

    hello.c
      ↓
    gcc -c
      ↓
    hello.o
      ↓
    링크
      ↓
    hello

### gcc -c 핵심

    gcc -c hello.c

→ **컴파일만 수행하고 링크하지 않는다.**

따라서:

- `gcc hello.c` → 컴파일 + 링크 → 실행 파일 생성
- `gcc -c hello.c` → 컴파일만 수행 → `.o` 목적 파일 생성

### 핵심 구분

| 과정 | 의미 |
|---|---|
| 컴파일 | 소스 코드를 목적 파일로 변환 |
| 목적 파일 | 컴파일되었지만 링크가 완료되지 않은 파일 |
| 링크 | 목적 파일과 라이브러리 등을 연결하여 실행 파일 생성 |
| 실행 | 완성된 실행 파일을 실제로 실행 |

> **암기**
>
> 컴파일 = 부품을 만드는 과정
>
> 링크 = 부품을 조립하여 실행 파일을 만드는 과정
>
> 실행 = 완성된 프로그램을 실제로 실행하는 과정

## make 유틸리티

`make`는 소스 코드의 컴파일 및 빌드 과정을 자동화하는 유틸리티이다.

프로그램을 구성하는 여러 소스 파일의 변경 여부와 의존 관계를 확인하여 **변경된 부분만 다시 컴파일**할 수 있다.

### 기본 사용법

`make [option]`

### 주요 옵션

| 옵션 | 설명 |
|---|---|
| `-f 파일명` | 기본 `Makefile` 대신 지정한 파일을 사용 |

예:

`make -f MyMakefile`

→ `MyMakefile`을 사용하여 빌드한다.

---

## Makefile

`Makefile`은 `make`가 프로그램을 어떻게 빌드할지 정의해 놓은 파일이다.

일반적으로 `make`를 실행하면 현재 디렉터리에서 `Makefile` 또는 `makefile` 등의 파일을 찾아 빌드한다.

### 기본 구조

Makefile의 기본적인 구조는 다음과 같다.

    대상: 의존성
        명령어

- **대상(Target)** → 생성하려는 파일 또는 실행할 작업
- **의존성(Dependency)** → 대상을 만들기 위해 필요한 파일
- **명령어(Command)** → 대상을 생성하기 위해 실행할 명령

> **주의**
>
> Makefile의 명령어 앞에는 **탭(Tab)** 문자를 사용해야 한다.

### 생성 예

다음과 같은 C 소스 코드가 있다고 가정한다.

    main.c
    add.c
    add.h

Makefile:

    program: main.o add.o
    	gcc -o program main.o add.o

    main.o: main.c add.h
    	gcc -c main.c

    add.o: add.c add.h
    	gcc -c add.c

    clean:
    	rm -f *.o program

`make`를 실행하면 `program`을 생성하기 위해 필요한 `main.o`, `add.o`를 먼저 확인하고 필요한 경우 컴파일한 후 `program`을 생성한다.

### Makefile의 동작 과정

    make
      ↓
    최종 대상 확인
      ↓
    의존성 확인
      ↓
    변경된 파일이 있는지 확인
      ↓
    필요한 명령만 실행
      ↓
    실행 파일 생성

예를 들어 `main.c`만 수정했다면 `add.o`는 다시 만들지 않고 `main.o`만 다시 컴파일한 뒤 최종 실행 파일을 다시 생성할 수 있다.

---

## Makefile 응용 구조

여러 소스 파일과 공통 옵션을 사용하는 경우 변수와 패턴 규칙 등을 활용하여 Makefile을 구성할 수 있다.

예:

    CC = gcc
    CFLAGS = -Wall
    TARGET = program
    OBJS = main.o add.o

    $(TARGET): $(OBJS)
    	$(CC) $(CFLAGS) -o $(TARGET) $(OBJS)

    %.o: %.c
    	$(CC) $(CFLAGS) -c $< -o $@

    clean:
    	rm -f $(OBJS) $(TARGET)

### 주요 구성 요소

| 구성 요소 | 설명 |
|---|---|
| `CC` | 사용할 컴파일러 지정 |
| `CFLAGS` | 컴파일 옵션 지정 |
| `TARGET` | 최종 생성할 실행 파일 지정 |
| `OBJS` | 오브젝트 파일 목록 지정 |
| `$(변수명)` | Makefile에서 변수 값 참조 |
| `%.o: %.c` | `.c` 파일을 `.o` 파일로 만드는 패턴 규칙 |
| `$<` | 첫 번째 의존성 파일 |
| `$@` | 현재 대상(Target) |

### 핵심 정리

| 개념 | 의미 |
|---|---|
| `make` | 빌드 자동화 유틸리티 |
| `make -f 파일명` | 지정한 Makefile 사용 |
| `Makefile` | 빌드 규칙과 의존 관계를 정의한 파일 |
| Target | 생성하려는 대상 |
| Dependency | 대상 생성에 필요한 파일 |
| Command | 대상을 생성하기 위해 실행할 명령 |
| `CC` | 컴파일러 |
| `CFLAGS` | 컴파일 옵션 |
| `clean` | 생성된 오브젝트 파일 및 실행 파일 등을 삭제하는 규칙 |

> **시험 포인트**
>
> - `make -f 파일명` → 지정한 Makefile 사용
> - Makefile 기본 구조 → `대상: 의존성` + `명령어`
> - Makefile의 명령어 앞에는 **탭(Tab)** 사용
> - `make`는 파일의 **의존 관계와 변경 여부를 확인하여 필요한 부분만 다시 빌드**한다.