# 프로세스 관리

## /proc 파일 시스템

- `/proc`은 실제 디스크에 존재하는 파일이 아니라 커널이 실시간으로 생성하는 가상 파일 시스템(procfs)이다.
- 시스템 및 프로세스 정보를 파일 형태로 제공한다.

## /proc/PID의 구조

프로세스 하나당 `/proc/PID` 디렉터리가 생성되며, 해당 프로세스의 정보가 파일 형태로 저장된다.

| 파일 | 설명 |
|------|------|
| cmdline | 프로세스 실행 시 사용한 명령어 |
| cwd | 현재 작업 디렉터리 |
| environ | 환경 변수 |
| exe | 실행 파일의 심볼릭 링크 |
| fd | 열린 파일 디스크립터 목록 |
| maps | 메모리 맵 정보 |
| mounts | 마운트 정보 |
| root | 프로세스의 루트 디렉터리 |
| stat | 프로세스 상태 정보(숫자 형태) |
| statm | 메모리 사용량 |
| status | 프로세스 상태 정보(읽기 쉬운 형태) |

## /proc 디렉터리의 주요 정보 파일 및 디렉터리

| 파일/디렉터리 | 설명 |
|--------------|------|
| acpi | ACPI 전원 관리 정보 |
| bus | 시스템 버스 정보 |
| cmdline | 부팅 시 커널 옵션 |
| cpuinfo | CPU 정보 |
| devices | 등록된 장치 정보 |
| dma | DMA 채널 정보 |
| filesystems | 지원하는 파일 시스템 |
| interrupts | 인터럽트 사용 현황 |
| iomem | 메모리 입출력 정보 |
| ioports | I/O 포트 정보 |
| kallsyms | 커널 심볼 정보 |
| kcore | 커널 메모리 이미지 |
| kmsg | 커널 로그 메시지 |
| loadavg | 시스템 평균 부하 |
| locks | 파일 잠금 정보 |
| mdstat | RAID 상태 정보 |
| meminfo | 메모리 사용 정보 |
| misc | 기타 장치 정보 |
| mounts | 현재 마운트 정보 |
| net | 네트워크 정보 |
| partitions | 디스크 파티션 정보 |
| scsi | SCSI 장치 정보 |
| self | 현재 프로세스(`/proc/self`) |
| stat | 시스템 상태 정보 |
| swaps | 스왑 영역 정보 |
| sys | 커널 시스템 정보 |
| sysvipc | System V IPC 정보 |
| uptime | 시스템 가동 시간 |
| version | 커널 버전 정보 |

