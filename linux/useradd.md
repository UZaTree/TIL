# useradd 명령어

## 1. 기본 구조

```bash
useradd [option] 사용자명
```

---

## 2. 옵션 정리

| 옵션 | 약어 | 설명 |
|---|---|---|
| `-p` | `--password` | 암호화된 값으로 비밀번호 지정 |
| `-d` | `--home-dir` | 홈 디렉토리 경로 직접 지정 (기본값: /home/사용자명) |
| `-g` | `--gid` | 기본 그룹 지정 (그룹명 또는 GID) |
| `-b` | `--base-dir` | 홈 디렉토리의 기준 디렉토리 지정 |
| `-G` | `--groups` | 보조 그룹 지정 (여러 개면 쉼표로 구분) |
| `-c` | `--comment` | 사용자 설명(코멘트) 지정. `/etc/passwd`의 GECOS 필드에 저장됨 |
| `-s` | `--shell` | 로그인 셸 지정 (기본값: /bin/bash) |
| `-D` | `--defaults` | useradd 기본값 확인 또는 변경 |
| `-m` | `--create-home` | 홈 디렉토리가 없으면 자동 생성 |
| `-k` | `--skel` | 홈 디렉토리 생성 시 복사할 스켈레톤 디렉토리 지정 (`-m`과 함께 사용) |
| `-f` | `--inactive` | 암호 만료 후 계정 비활성화까지의 유예기간(일) 지정. -1이면 비활성화 안 함 |
| `-e` | `--expiredate` | 계정 만료일 지정 (YYYY-MM-DD 형식) |
| `-u` | `--uid` | UID 직접 지정 |
| `-h` | `--help` | 도움말 출력 |

> `-g` (기본 그룹, 소문자) vs `-G` (보조 그룹, 대문자) 혼동 주의

---

## 3. 주요 개념

### 로그인 셸
사용자가 로그인했을 때 실행되는 셸 환경

| 셸 | 경로 | 특징 |
|---|---|---|
| bash | `/bin/bash` | 가장 많이 쓰는 기본 셸 |
| sh | `/bin/sh` | 가장 오래된 기본 셸 |
| zsh | `/bin/zsh` | macOS 기본 셸 |
| nologin | `/sbin/nologin` | 로그인 자체를 막음 (시스템 계정에 사용) |

### 스켈레톤 디렉토리
새 사용자의 홈 디렉토리를 만들 때 복사해주는 기본 템플릿 (`/etc/skel`)

```
/etc/skel/
  ├ .bashrc
  ├ .bash_profile
  └ .bash_logout
```

`-m` 옵션으로 홈 디렉토리 생성 시 위 파일들이 자동으로 복사됨

---

## 4. useradd 실행 시 영향받는 파일

```
useradd -m jiwon 실행
      │
      ├→ /etc/passwd  : 사용자 기본 정보 추가
      ├→ /etc/shadow  : 암호화된 비밀번호 정보 추가
      ├→ /etc/group   : 기본 그룹 정보 추가
      └→ /home/jiwon/ : 홈 디렉토리 생성 + /etc/skel 내용 복사
```

### `/etc/passwd` 구조

```
jiwon:x:1000:1000:코멘트:/home/jiwon:/bin/bash
  │   │   │    │     │        │          └ 로그인 셸
  │   │   │    │     │        └ 홈 디렉토리
  │   │   │    │     └ 코멘트 (-c 옵션)
  │   │   │    └ GID
  │   │   └ UID
  │   └ 암호 (x = /etc/shadow에 저장됨)
  └ 사용자명
```

### `/etc/shadow`
암호화된 비밀번호 + 비밀번호 정책 저장. root만 읽기 가능

---

## 5. 사용 예시

```bash
useradd -m -d /home/jiwon -s /bin/bash -G dev,security jiwon
# 홈 디렉토리 생성 + 경로 지정 + 셸 지정 + 보조 그룹 지정
```
