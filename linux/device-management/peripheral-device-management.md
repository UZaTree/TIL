# 주변 장치 설정

## 1. 프린터

### 프린터 개요

Linux에서 사용하는 대표적인 프린터 관리 시스템으로 LPRng와 CUPS가 있다.

### LPRng

LPRng는 전통적인 BSD 계열의 프린팅 시스템이다.

- BSD 계열 프린팅 시스템
- `lpr`, `lpq`, `lprm`, `lpc` 등의 명령어 사용

### CUPS

CUPS(Common UNIX Printing System)는 Linux 및 Unix 계열에서 사용하는 프린팅 시스템이다.

- System V 계열 프린팅 시스템
- 네트워크 프린팅 지원
- 프린터 및 프린터 작업 관리
- 웹 기반 관리 기능 제공

### CUPS 관련 설정 파일

| 파일 | 경로 | 설명 |
|---|---|---|
| `cupsd.conf` | `/etc/cups/cupsd.conf` | CUPS 데몬 설정 파일 |
| `printers.conf` | `/etc/cups/printers.conf` | 프린터 설정 파일 |
| `classes.conf` | `/etc/cups/classes.conf` | 프린터 클래스 설정 파일 |

---

## 2. 사운드 카드

### ALSA

ALSA(Advanced Linux Sound Architecture)는 Linux에서 사운드 장치를 지원하기 위한 사운드 시스템이다.

- Linux의 대표적인 사운드 시스템
- 다양한 사운드 카드 지원
- 오디오 재생 및 녹음 지원
- 기존 OSS를 대체

### OSS

OSS(Open Sound System)는 Unix 계열 운영체제에서 사용되던 사운드 시스템이다.

- 전통적인 Unix/Linux 사운드 시스템
- 현재는 ALSA가 주로 사용됨

---

## 3. 스캐너

### SANE

SANE(Scanner Access Now Easy)은 Linux 및 Unix 계열에서 스캐너를 사용할 수 있도록 지원하는 표준 인터페이스 및 프레임워크이다.

- 다양한 스캐너 지원
- 스캐너 장치에 접근하기 위한 인터페이스 제공

### XSANE

XSANE은 SANE을 기반으로 동작하는 그래픽 스캐너 프로그램이다.

- GUI 환경에서 스캐너 사용
- SANE 백엔드를 이용하여 스캐너 제어

---

## 4. SSD

### SSD 개요

SSD(Solid State Drive)는 반도체 메모리를 이용하여 데이터를 저장하는 저장 장치이다.

- 플래시 메모리 사용
- 물리적인 회전 부품이 없음
- HDD보다 빠른 데이터 접근 속도
- 낮은 지연 시간

### 데이터 버스

SSD에서 사용하는 대표적인 데이터 버스로 SATA와 PCIe가 있다.

#### SATA

SATA(Serial ATA)는 저장 장치를 연결하기 위한 직렬 인터페이스이다.

- HDD 및 SATA SSD에서 사용
- 저장 장치 연결에 사용되는 인터페이스

#### PCIe

PCIe(Peripheral Component Interconnect Express)는 고속 직렬 데이터 버스이다.

- 높은 데이터 전송 속도
- NVMe SSD에서 주로 사용

### 통신 드라이버

#### AHCI

AHCI(Advanced Host Controller Interface)는 SATA 장치를 위한 호스트 컨트롤러 인터페이스이다.

- SATA 기반
- SATA SSD 및 HDD에서 사용

#### NVMe

NVMe(Non-Volatile Memory Express)는 PCIe 기반의 비휘발성 메모리 저장 장치를 위한 통신 프로토콜이다.

- PCIe 기반
- SSD에 최적화된 프로토콜
- AHCI보다 낮은 지연 시간
- 높은 병렬 처리 성능

### AHCI와 NVMe 비교

| 구분 | AHCI | NVMe |
|---|---|---|
| 기반 | SATA | PCIe |
| 주요 대상 | SATA SSD, HDD | NVMe SSD |
| 지연 시간 | 상대적으로 높음 | 상대적으로 낮음 |
| 성능 | 상대적으로 낮음 | 상대적으로 높음 |
| 특징 | SATA 장치용 | SSD에 최적화 |

---

## 5. LVM

### LVM 개요

LVM(Logical Volume Manager)은 물리적인 저장 공간을 논리적인 볼륨으로 구성하고 관리하는 방식이다.

LVM은 다음과 같은 계층 구조로 구성된다.

    물리 디스크
        ↓
        PV
        ↓
        VG
        ↓
        LV
        ↓
    파일 시스템

### PV

PV(Physical Volume)는 LVM에서 사용하는 물리적인 저장 공간이다.

물리 디스크 전체 또는 디스크의 파티션을 PV로 사용할 수 있다.

### PE

PE(Physical Extent)는 PV를 일정한 크기로 나눈 물리적인 저장 공간의 단위이다.

- PV는 여러 개의 PE로 구성됨
- PE는 LVM에서 공간을 할당하는 기본 단위
- PV가 VG에 추가되면 PV의 PE가 VG에 포함됨

    PV
    ├── PE
    ├── PE
    ├── PE
    ├── PE
    └── ...

### VG

VG(Volume Group)는 하나 이상의 PV를 하나로 묶은 논리적인 저장 공간이다.

    PV ─┐
        ├── VG
    PV ─┘

여러 PV의 저장 공간을 하나의 큰 저장 공간처럼 관리할 수 있다.

### LV

LV(Logical Volume)는 VG에서 필요한 크기만큼 공간을 할당하여 생성한 논리적인 볼륨이다.

    VG
    ├── LV
    ├── LV
    └── LV

LV에는 파일 시스템을 생성하여 일반적인 파티션처럼 사용할 수 있다.

### LVM 구성 관계

    PV → PE → VG → LV → 파일 시스템

---

## 6. LVM 확장

LVM의 저장 공간을 확장하는 일반적인 절차는 다음과 같다.

1. 새로운 디스크 또는 파티션을 준비한다.
2. 새로운 PV를 생성한다.
3. 새로운 PV를 기존 VG에 추가한다.
4. 기존 LV의 크기를 확장한다.
5. 파일 시스템의 크기를 확장한다.

    새 디스크
        ↓
    PV 생성
        ↓
    VG에 추가
        ↓
    LV 확장
        ↓
    파일 시스템 확장

---

## 7. RAID

RAID(Redundant Array of Independent Disks)는 여러 개의 디스크를 하나의 논리적인 저장 장치처럼 구성하는 기술이다.

RAID의 주요 목적은 다음과 같다.

- 저장 장치 성능 향상
- 데이터 안정성 향상
- 디스크 장애에 대한 대응

### RAID 0

데이터를 여러 디스크에 분산하여 저장한다.

- 스트라이핑(Striping)
- 읽기 및 쓰기 성능 향상
- 디스크 장애 발생 시 데이터 복구 불가능
- 최소 2개의 디스크 필요

### RAID 1

동일한 데이터를 여러 디스크에 복제하여 저장한다.

- 미러링(Mirroring)
- 데이터 안정성 향상
- 하나의 디스크가 고장 나도 데이터 유지 가능
- 저장 공간 효율이 낮음
- 최소 2개의 디스크 필요

### RAID 5

데이터와 패리티 정보를 여러 디스크에 분산하여 저장한다.

- 스트라이핑 + 분산 패리티
- 디스크 1개 장애 대응 가능
- 최소 3개의 디스크 필요
- 디스크 1개 분량의 용량을 패리티에 사용

### RAID 6

데이터와 이중 패리티를 여러 디스크에 분산하여 저장한다.

- 스트라이핑 + 이중 분산 패리티
- 디스크 2개 장애 대응 가능
- 최소 4개의 디스크 필요
- 디스크 2개 분량의 용량을 패리티에 사용

### RAID 10

RAID 1과 RAID 0을 결합한 방식이다.

- 미러링 + 스트라이핑
- 높은 성능과 안정성 제공
- 최소 4개의 디스크 필요
- 전체 디스크 용량의 약 절반을 사용 가능