# 로그 관련 파일

## 1. 주요 로그 파일

| 로그 파일 | 내용 |
|---|---|
| `/var/log/messages` | 시스템 전반의 일반적인 메시지 및 시스템 로그 |
| `/var/log/secure` | 사용자 인증 및 보안 관련 로그 |
| `/var/log/dmesg` | 커널 링 버퍼의 메시지 및 부팅 과정에서 발생한 커널 관련 로그 |
| `/var/log/maillog` | 메일 관련 로그 |
| `/var/log/xferlog` | FTP 파일 전송 관련 로그 |
| `/var/log/cron` | cron 및 at 작업 관련 로그 |
| `/var/log/boot.log` | 시스템 부팅 과정에서 발생하는 서비스 관련 로그 |
| `/var/log/lastlog` | 각 사용자의 최근 로그인 정보 |
| `/var/log/wtmp` | 시스템의 로그인 및 로그아웃 기록 |
| `/var/log/btmp` | 실패한 로그인 기록 |

> `maillog`의 정확한 파일명은 `/var/log/maillog`이다.

---

## 2. `/var/log/xferlog`

`xferlog`는 FTP를 이용한 파일 전송과 관련된 로그를 기록한다.

### 로그 포맷

다음과 같은 순서로 기록된다.

`current-time, transfer-time, remote-host, file-size, filename, transfer-type, special-action-flag, direction, access-mode, username, service-name, authentication-method, authentication-user-id, completion-status`

| 항목 | 설명 |
|---|---|
| `current-time` | 현재 시간 |
| `transfer-time` | 전송에 걸린 시간 |
| `remote-host` | 원격 호스트 |
| `file-size` | 전송된 파일의 크기 |
| `filename` | 파일 이름 |
| `transfer-type` | 전송 유형 |
| `special-action-flag` | 특수 동작 플래그 |
| `direction` | 전송 방향 |
| `access-mode` | 접근 모드 |
| `username` | 사용자 이름 |
| `service-name` | 서비스 이름 |
| `authentication-method` | 인증 방식 |
| `authentication-user-id` | 인증 사용자 ID |
| `completion-status` | 전송 완료 상태 |