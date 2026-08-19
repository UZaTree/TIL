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