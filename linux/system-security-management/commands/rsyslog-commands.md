# rsyslog 및 logrotate 명령어

## 1. systemctl

`systemctl`은 systemd 기반 시스템에서 서비스를 관리하는 명령어이다.

### 주요 명령

| 명령 | 설명 |
|---|---|
| `start` | 서비스 시작 |
| `stop` | 서비스 중지 |
| `restart` | 서비스 재시작 |
| `status` | 서비스 상태 확인 |
| `enable` | 부팅 시 서비스 자동 시작 |
| `disable` | 부팅 시 서비스 자동 시작 해제 |

### 주요 옵션

| 옵션 | 설명 |
|---|---|
| `-l` | 출력 내용을 생략하지 않고 전체 표시 |

---

## 2. rsyslog 데몬 관리

### rsyslog 데몬 동작 확인

`systemctl status rsyslog`

현재 rsyslog 데몬의 동작 상태를 확인한다.

### rsyslog 데몬 재시작

`systemctl restart rsyslog`

rsyslog 데몬을 재시작한다.

### 부팅 시 rsyslog 데몬 활성화

`systemctl enable rsyslog`

시스템 부팅 시 rsyslog 데몬이 자동으로 시작되도록 설정한다.

### rsyslog 데몬 시작

`systemctl start rsyslog`

현재 중지되어 있는 rsyslog 데몬을 시작한다.

### rsyslog 데몬 중지

`systemctl stop rsyslog`

현재 실행 중인 rsyslog 데몬을 중지한다.

### 서비스 상태 전체 확인

`systemctl status -l rsyslog`

rsyslog 서비스의 상태를 확인하면서 출력 내용을 생략하지 않고 전체 표시한다.

---

## 3. logrotate

### logrotate

`logrotate`는 로그 파일을 일정한 주기로 교체하고 관리하는 명령어이다.

### -f

`-f` 옵션은 로그 교체 조건이 충족되지 않았더라도 강제로 로그를 교체하도록 한다.

예:

`logrotate -f /etc/logrotate.conf`

`/etc/logrotate.conf`의 설정을 기준으로 로그 로테이션을 강제로 실행한다.