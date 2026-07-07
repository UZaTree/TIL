# 파일 시스템 관리

## 1. 디스크 장착 후 작업 순서

```
디스크 인식 여부 확인 (fdisk -l)
      ↓
파티션 작업 (fdisk)
      ↓
시스템 재부팅 (reboot / partprobe)
      ↓
파일 시스템 생성 (mkfs)
      ↓
디렉토리(마운트 포인트) 생성 (mkdir)
      ↓
마운트 작업 (mount)
      ↓
마운트 및 용량 확인 (mount, df -h)
      ↓
부팅 시 자동 마운트 되도록 /etc/fstab 에 등록
```

---

## 2. 주요 개념

### 마운트 (Mount)
디스크나 파티션을 리눅스 디렉토리에 연결하는 작업

- 리눅스는 모든 걸 디렉토리 구조로 관리
- 새 디스크를 꽂아도 디렉토리에 연결하지 않으면 사용 불가
- 마운트 포인트 = 디스크를 연결할 디렉토리
- 재부팅하면 마운트 초기화 → 영구적으로 쓰려면 fstab 등록 필요

```
새 디스크 /dev/sdb1  ──마운트──→  /data 디렉토리
```

### /etc/fstab (filesystem table)
부팅 시 자동으로 마운트할 목록을 저장하는 시스템 설정 파일

```
장치명        마운트포인트   파일시스템   옵션      덤프  검사순서
/dev/sdb1    /data         ext4        defaults   0     0
LABEL=backup /backup       xfs         defaults   0     0
```

> LABEL = 파티션에 붙이는 이름표. 장치명 대신 사용 가능

---

## 3. fdisk

디스크 파티션을 관리하는 명령어

```bash
fdisk -l            # 전체 디스크 파티션 목록
fdisk -l /dev/sdb   # /dev/sdb 파티션 목록
fdisk -s /dev/sdb1  # /dev/sdb1 파티션 크기
fdisk /dev/sdb      # /dev/sdb 파티션 작업 (대화형)
```

### 대화형 모드 주요 명령어

| 명령어 | 설명 |
|---|---|
| `p` | 현재 파티션 목록 출력 |
| `d` | 파티션 삭제 |
| `n` | 새 파티션 생성 |
| `t` | 파티션 타입 변경 |
| `w` | 변경사항 저장 후 종료 |
| `q` | 저장 없이 종료 |

### 파티션 타입 코드

| 코드 | 설명 |
|---|---|
| `82` | Linux swap |
| `83` | Linux (일반 리눅스 파티션) |
| `8e` | Linux LVM |
| `fd` | Linux raid auto |
| `l` | 사용 가능한 타입 코드 목록 출력 |

---

## 4. mkfs

파일 시스템을 생성하는 명령어 (포맷)

```bash
mkfs /dev/sdb1              # 기본값(ext2)으로 포맷
mkfs -t ext4 /dev/sdb1     # ext4로 포맷
mkfs -t xfs /dev/sdb1      # xfs로 포맷
mkfs.xfs /dev/sdb1         # mkfs -t xfs 와 동일
```

---

## 5. mke2fs

ext 계열 파일 시스템 전용 생성 명령어

| 옵션 | 설명 |
|---|---|
| `-j` | 저널링 추가하여 ext3 생성 |
| `-t fs_type` | 파일 시스템 종류 지정 |
| `-b block_size` | 블록 크기 지정 (국자 크기 느낌, 기본값 1024) |
| `-R raid_options` | RAID 환경에 맞게 최적화 |
| `-T usage_type` | 용도에 맞게 inode 수 조정 |

```bash
mke2fs /dev/sdb1              # ext2 생성
mke2fs -j /dev/sdb1           # ext3 생성
mke2fs -t ext4 /dev/sdb1      # ext4 생성
```

> `mkfs -t ext4` 와 `mke2fs -t ext4` 는 동일. mkfs가 내부적으로 mke2fs 호출

---

## 6. mkfs.xfs

XFS 파일 시스템 생성 명령어

| 옵션 | 설명 |
|---|---|
| `-b block_size` | 블록 크기 지정. 512~65536바이트, 기본값 4096바이트 |
| `-f` | 기존 파일 시스템 있어도 강제 덮어쓰기 |

---

## 7. 주요 파일 시스템 유형

| 유형 | 설명 |
|---|---|
| `ext2/3/4` | 리눅스 기본. ext3부터 저널링 추가. 데비안 계열 기본 |
| `xfs` | 대용량에 강함. 레드햇 계열 기본 |
| `msdos` | MS-DOS FAT16 |
| `vfat` | 윈도우 FAT32 |
| `ntfs` | 윈도우 NTFS |
| `iso9660` | CD/DVD |
| `smbfs` | 윈도우 네트워크 공유 (구버전) |
| `cifs` | 윈도우 네트워크 공유 (최신) |
| `nfs` | 리눅스/유닉스 네트워크 파일 시스템 |
| `udf` | DVD, Blu-ray |

---

## 8. 주요 디바이스 파일명

| 장치 | 파일명 |
|---|---|
| FDD | `/dev/fd0`, `/dev/fd1` |
| CD-ROM / DVD | `/dev/cdrom`, `/dev/dvd`, `/dev/sr0` |
| IDE HDD | `/dev/hda1`, `/dev/hdb1` |
| USB / SCSI / S-ATA | `/dev/sda`, `/dev/sdb1` |

> `sd` 뒤 알파벳 = 디스크 구분 (sda, sdb ...), 숫자 = 파티션 번호

---

## 9. mount

파티션을 디렉토리에 연결하는 명령어

```bash
mount                              # 현재 마운트 목록 출력
mount -t xfs /dev/sdb1 /backup    # xfs로 /backup에 마운트
mount -a                           # fstab에 등록된 전체 마운트
mount -o ro /dev/sdb1 /backup     # 읽기 전용으로 마운트
```

### 옵션

| 옵션 | 설명 |
|---|---|
| `-a` | `/etc/fstab` 에 등록된 모든 파일 시스템 마운트 |
| `-t fs_type` | 파일 시스템 종류 지정 |
| `-o` | 마운트 옵션 지정 |

### -o 세부 옵션

| 옵션 | 설명 |
|---|---|
| `ro` | 읽기 전용 (read only) |
| `rw` | 읽기/쓰기 (read write, 기본값) |
| `remount` | 이미 마운트된 것을 재설정 (옵션 변경 시 사용) |
| `loop` | 이미지 파일(ISO 등) 마운트 시 사용 |
| `noatime` | 파일 접근 시 접근 시간 업데이트 안 함 (성능 향상) |
| `username=사용자명` | 네트워크 파일 시스템 접속 시 사용자명 지정 |
| `password=암호` | 네트워크 파일 시스템 접속 시 암호 지정 |
| `acl` | ACL 활성화 |
| `uquota` | 사용자별 디스크 사용량 제한 활성화 |
| `gquota` | 그룹별 디스크 사용량 제한 활성화 |

---

## 10. umount

마운트된 파일 시스템을 해제하는 명령어

```bash
umount /dev/sdb1       # 디바이스명으로 언마운트
umount /backup         # 마운트 포인트로 언마운트
umount -a              # fstab 등록된 전체 언마운트 (/ 제외)
umount -t xfs          # xfs 파일 시스템만 언마운트
```

| 옵션 | 설명 |
|---|---|
| `-a` | 전체 언마운트 (루트 제외) |
| `-t fs_type` | 특정 파일 시스템 유형만 언마운트 |

> 해당 디렉토리 안에 있을 때 언마운트하면 오류 발생

---

## 11. eject

물리적 장치를 꺼내는 명령어

```bash
eject /dev/cdrom
```

> `umount` = 안전하게 제거 버튼 (소프트웨어적 해제)
> `eject` = 실제로 장치 꺼냄 (내부적으로 umount 먼저 수행)

---

## 12. parted

fdisk보다 더 많은 기능을 제공하는 파티션 관리 명령어

| 옵션 | 설명 |
|---|---|
| `-h`, `--help` | 도움말 출력 |
| `-l`, `--list` | 모든 디스크의 파티션 목록 출력 |

### 실행 후 주요 명령어

| 명령어 | 설명 |
|---|---|
| `help` | 도움말 출력 |
| `print` | 현재 파티션 정보 출력 (파티션 번호 확인) |
| `mklabel` | 디스크 레이블 생성 (msdos / gpt) |
| `mkpart` | 파티션 생성 |
| `rm` | 파티션 삭제 |
| `resizepart` | 파티션 크기 변경 |
| `quit` | 종료 |

### mklabel 타입

| 타입 | 설명 |
|---|---|
| `msdos` | 2TB 이하, 최대 4개 주 파티션 |
| `gpt` | 2TB 이상, 파티션 수 제한 없음 |

### mkpart 사용법

```bash
mkpart PART-TYPE [FS-TYPE] START END
```

| 항목 | 설명 |
|---|---|
| `PART-TYPE` | primary, extended, logical |
| `FS-TYPE` | ext4, xfs 등 (생략 가능) |
| `START` | 파티션 시작 위치 (물리적 위치) |
| `END` | 파티션 끝 위치 (포함 안 됨) |

### 파티션 종류

| 종류 | 설명 |
|---|---|
| primary | 직접 사용 가능. 최대 4개 |
| extended | primary 4개 제한 극복용. 데이터 저장 불가. 1개만 가능 |
| logical | extended 안에 생성. 개수 제한 없음 |

> 일반적으로 primary 3개 + extended 1개 조합 사용

### resizepart 사용법

```bash
resizepart Number END
# Number = 파티션 번호 (print로 확인)
# END = 새로운 끝 지점
```

### fdisk vs parted

| | fdisk | parted |
|---|---|---|
| 2TB 이상 | 불가 | 가능 |
| 실시간 반영 | 재부팅 필요 | 즉시 반영 |

---

## 13. /etc/fstab 상세

### 필드 구성

```
장치           마운트포인트   파일시스템   옵션      덤프  검사순서
/dev/sdb1     /data         ext4        defaults   0     0
LABEL=backup  /backup       xfs         defaults   0     0
UUID=xxxx...  /home         ext4        defaults   0     0
```

> 최근 배포판은 장치명 대신 LABEL이나 UUID 사용 권장 (장치명은 상황에 따라 바뀔 수 있음)

### 덤프 필드

| 값 | 설명 |
|---|---|
| 0 | 덤프 사용 안 함 |
| 1 | 매일 수행 |
| 2 | 이틀에 한 번 수행 |

### 검사순서 필드

| 값 | 설명 |
|---|---|
| 0 | 검사 안 함 |
| 1 | 루트 파일 시스템 |
| 2 | 나머지 파일 시스템 |

### 4번째 필드 주요 옵션

| 옵션 | 설명 |
|---|---|
| `defaults` | rw, suid, dev, exec, auto, nouser, async 적용 |
| `auto` | 부팅 시 자동 마운트. `-a` 옵션으로도 마운트 가능 |
| `noauto` | 부팅 시 자동 마운트 안 함. 명시적으로만 가능 |
| `user` | 일반 사용자도 마운트 가능 |
| `owner` | 장치 소유자만 마운트 가능 |
| `nofail` | 장치 없어도 오류 출력 안 함 |
| `uquota, usrquota, quota` | 사용자별 용량 제한 |
| `gquota, grpquota` | 그룹별 용량 제한 |
| `noquota` | quota 사용 안 함 |
| `nosuid` | SUID, SGID 사용 불허 |
| `nodev` | 특별한 장치 허용 안 함 |
| `noexec` | 실행 파일 실행 불허 |
| `suid` | SUID, SGID 허용 |
| `ro` | 읽기 전용 |
| `rw` | 읽기/쓰기 |
| `async` | 파일 비동기적으로 관리 |
| `acl` | Access Control Lists 사용 |

> fstab 변경 후 `systemctl daemon-reload` 실행 필요

### /etc/mtab
현재 마운트된 파일 시스템 현황 파일 (시스템이 자동 관리, 직접 편집 안 함)

> fstab = 마운트할 목록 (설정), mtab = 현재 마운트된 목록 (현황)

---

## 14. 파티션/파일시스템 관련 유틸리티

### udevadm settle
커널이 새 파티션을 인식할 때까지 대기

```bash
udevadm settle
```

### cat /proc/partitions
커널이 현재 인식하고 있는 모든 파티션 목록 출력

```bash
cat /proc/partitions
```

> `/proc` = 커널이 실시간으로 만들어주는 가상 파일 디렉토리

### blkid
블록 장치의 UUID, 라벨 등 정보 출력

```bash
blkid                    # 전체 블록 장치 정보
blkid -L backup          # backup 라벨을 가진 장치명 출력
blkid -U xxxx-xxxx       # 해당 UUID를 가진 장치명 출력
```

### lsblk
블록 장치 목록을 트리 형태로 출력

```bash
lsblk        # 트리 출력
lsblk -f     # 파일시스템 정보 포함 (UUID, 라벨)
lsblk -m     # 소유자, 권한 정보 포함
lsblk -o NAME,SIZE,FSTYPE  # 원하는 컬럼만 출력
```

### findfs
라벨이나 UUID로 장치를 찾는 명령어

```bash
findfs LABEL=backup
findfs UUID=xxxx-xxxx
```

### findmnt
마운트된 파일 시스템을 찾아서 출력

```bash
findmnt              # 트리 형태 출력
findmnt -D           # 디스크 사용량 포함 출력
findmnt -s           # fstab 기준으로 출력
findmnt -t xfs       # xfs만 출력
findmnt -l           # 목록 형태로 출력
```

---

## 15. fsck / e2fsck

### fsck
파일 시스템 검사 및 복구 명령어

| 옵션 | 설명 |
|---|---|
| `-r` | 명령 수행 확인 질문 (병렬 모드 시 유용) |
| `-A` | fstab 등록된 전체 검사 (루트 먼저, 나머지 병렬) |
| `-P` | `-A` 사용 시 루트도 병렬로 검사 |
| `-R` | `-A` 사용 시 루트 검사 건너뜀 |
| `-N` | 실제 실행 않고 작업 내용만 출력 (dry-run) |
| `-T` | 시작 시 타이틀 출력 안 함 |
| `-s` | 순차적으로 검사 (병렬 비활성화) |
| `-V` | 상세 정보 출력 |
| `-t fs_type` | 특정 파일 시스템만 검사 |

> 마운트된 상태에서 실행 위험. 언마운트 후 실행
> XFS는 fsck 사용 불가 → xfs_repair 사용

### e2fsck
ext2/3/4 전용 검사 및 복구 명령어

| 옵션 | 설명 |
|---|---|
| `-n` | 모든 질문에 자동으로 no (읽기 전용 검사) |
| `-y` | 모든 질문에 자동으로 yes |
| `-c` | 배드블록 검사 후 목록 업데이트 |
| `-f` | 정상이어도 강제 검사 |
