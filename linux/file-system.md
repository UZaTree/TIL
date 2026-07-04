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
