# 시스템 분석

## 1. rsyslog

### rsyslog 개요

`rsyslog`는 Linux 시스템에서 발생하는 로그 메시지를 수집하고 처리하는 로그 관리 시스템이다.

- 시스템 및 애플리케이션에서 발생하는 로그 수집
- 로그를 파일이나 원격 서버 등으로 전달
- 로그의 종류와 우선순위에 따라 저장 위치 및 처리 방법 지정
- 기존 syslog를 확장한 로그 관리 시스템

### 주요 파일

| 파일 | 설명 |
|---|---|
| `/etc/rsyslog.conf` | rsyslog의 주요 설정 파일 |
| `/etc/sysconfig/rsyslog` | rsyslog 데몬의 실행 환경 및 옵션 설정 |
| `/usr/sbin/rsyslogd` | rsyslog 데몬 실행 파일 |
| `/usr/lib/systemd/system/rsyslog.service` | systemd에서 rsyslog 서비스를 관리하기 위한 서비스 유닛 파일 |

### rsyslog 구성 요소

- `im` (Input Module) → 로그를 입력받는 모듈
- `om` (Output Module) → 로그를 출력하는 모듈

`im`은 시스템이나 외부에서 로그 메시지를 입력받고, `om`은 입력받은 로그를 파일이나 원격 호스트 등의 대상으로 출력한다.

---

## 2. `/etc/rsyslog.conf`

`/etc/rsyslog.conf`는 rsyslog의 주요 설정 파일이다.

### 기본 구성

`facility.priority action`

- `facility` → 로그의 종류
- `priority` → 로그의 우선순위
- `action` → 로그 처리 방법 또는 저장 위치

예:

`*.info /var/log/messages`

모든 facility의 `info` 이상 priority를 가진 로그를 `/var/log/messages`에 기록한다.

---

## 3. Facility

Facility는 로그 메시지가 발생한 시스템 또는 프로그램의 종류를 나타낸다.

| Facility | 설명 |
|---|---|
| `cron` | cron 및 at 관련 로그 |
| `auth` | 인증 관련 로그 |
| `security` | 보안 관련 로그 |
| `authpriv` | 인증 및 보안 관련 로그 |
| `daemon` | 시스템 데몬 관련 로그 |
| `kern` | 커널 관련 로그 |
| `lpr` | 프린터 관련 로그 |
| `mail` | 메일 시스템 관련 로그 |
| `mark` | 내부 타임스탬프 메시지 |
| `news` | USENET 뉴스 관련 로그 |
| `syslog` | syslog 관련 로그 |
| `user` | 사용자 프로세스 관련 로그 |
| `uucp` | UUCP 관련 로그 |
| `local0` ~ `local7` | 사용자 정의 로그 |
| `*` | 모든 facility |

`auth`와 `security`, `warning`과 `warn`, `error`와 `err`, `emerg`와 `panic`은 서로 대응되는 표현으로 사용된다.

---

## 4. Priority

Priority는 로그 메시지의 중요도 또는 심각도를 나타낸다.

| Priority | 의미 |
|---|---|
| `none` | 해당 facility의 로그를 제외 |
| `debug` | 디버깅 관련 메시지 |
| `info` | 일반적인 정보 |
| `notice` | 일반적인 중요 알림 |
| `warning` / `warn` | 경고 |
| `error` / `err` | 오류 |
| `crit` | 심각한 오류 |
| `alert` | 즉각적인 조치가 필요한 상황 |
| `emerg` / `panic` | 매우 심각한 상황 |
| `*` | 모든 priority |

일반적으로 특정 priority를 지정하면 해당 priority 이상으로 심각한 로그가 대상이 된다.

예:

`*.warning /var/log/messages`

모든 facility의 `warning` 이상 priority 로그를 `/var/log/messages`에 기록한다.

---

## 5. Action

Action은 조건에 일치하는 로그를 어디로 보내거나 어떻게 처리할 것인지 지정한다.

### 파일

로그를 지정한 파일에 기록한다.

`*.info /var/log/messages`

### 원격 호스트

`@host`를 사용하면 UDP를 통해 원격 호스트로 로그를 전달한다.

`@@host`를 사용하면 TCP를 통해 원격 호스트로 로그를 전달한다.

| 형식 | 방식 |
|---|---|
| `@host` | UDP |
| `@@host` | TCP |

### 특정 사용자

특정 사용자의 터미널로 로그를 전달할 수 있다.

### 모든 사용자

`*`을 사용하면 로그인한 모든 사용자의 터미널로 로그를 전달할 수 있다.

### 콘솔 또는 터미널

콘솔이나 특정 터미널 장치를 대상으로 로그를 출력할 수 있다.

---

## 6. logrotate

### logrotate 개요

`logrotate`는 시스템에서 생성되는 로그 파일을 효율적으로 관리하기 위한 프로그램이다.

로그 파일은 계속 기록되기 때문에 시간이 지나면 크기가 지나치게 커질 수 있다.

`logrotate`는 로그 파일을 일정한 주기마다 교체하고 오래된 로그를 삭제하거나 압축하여 로그 파일의 크기를 관리한다.

주요 기능:

- 로그 파일 교체(Rotation)
- 오래된 로그 보관
- 로그 파일 압축
- 로그 파일 생성
- 로그 파일 관리 주기 설정

### 관련 파일

| 파일 | 설명 |
|---|---|
| `/etc/logrotate.conf` | logrotate의 기본 설정 파일 |
| `/etc/logrotate.d/` | 개별 서비스의 logrotate 설정 파일이 저장되는 디렉터리 |
| `/var/lib/logrotate.status` | logrotate가 각 로그 파일을 마지막으로 처리한 시점을 기록하는 상태 파일 |

---

## 7. `/etc/logrotate.conf`

`/etc/logrotate.conf`는 logrotate의 기본 설정을 지정한다.

### 주요 설정

#### 기간 관련 옵션

- `daily` → 매일
- `weekly` → 매주
- `monthly` → 매월
- `yearly` → 매년

#### rotate 4

로그 파일을 4개까지 보관한다.

`rotate 4`

#### create

로그를 교체한 후 새로운 로그 파일을 생성한다.

`create`

#### dateext

교체된 로그 파일의 이름에 날짜를 추가한다.

`dateext`

#### compress

오래된 로그 파일을 압축한다.

`compress`

#### include /etc/logrotate.d

`/etc/logrotate.d` 디렉터리에 있는 개별 서비스의 설정 파일을 포함한다.

`include /etc/logrotate.d`

#### missingok

로그 파일이 존재하지 않아도 오류를 발생시키지 않고 다음 로그 파일로 진행한다.

`missingok`

#### nomissingok

로그 파일이 존재하지 않을 경우 오류를 발생시키도록 한다.

`nomissingok`

---

## 8. logrotate 설정 예시

### 예시 1

`/var/log/messages {
    weekly
    rotate 4
    compress
    missingok
    create
}`

설명:

- `/var/log/messages`를 대상으로 한다.
- 매주 로그를 교체한다.
- 최근 로그 4개를 보관한다.
- 오래된 로그를 압축한다.
- 로그 파일이 없어도 오류를 발생시키지 않는다.
- 로그 교체 후 새로운 로그 파일을 생성한다.

### 예시 2

`/var/log/httpd/*.log {
    daily
    rotate 7
    dateext
    compress
    missingok
    create
}`

설명:

- `/var/log/httpd/` 아래의 `.log` 파일을 대상으로 한다.
- 매일 로그를 교체한다.
- 최근 로그 7개를 보관한다.
- 교체된 로그 파일에 날짜를 붙인다.
- 오래된 로그를 압축한다.
- 로그 파일이 없어도 오류를 발생시키지 않는다.
- 새로운 로그 파일을 생성한다.