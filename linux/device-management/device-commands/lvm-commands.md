# LVM 관리 명령어

## 1. PV 관련 명령어

### pvscan

시스템의 PV(Physical Volume)를 검색하고 정보를 표시한다.

#### 주요 옵션

- `-u` → UUID 표시
- `-p` → PV 관련 정보 표시

---

### pvs

PV의 정보를 요약하여 표시한다.

#### 주요 속성

- `PV` → 물리 볼륨 이름
- `VG` → 소속 볼륨 그룹
- `Fmt` → LVM 형식
- `Attr` → PV 속성
- `PSize` → PV 전체 크기
- `PFree` → 사용 가능한 공간

#### 주요 옵션

- `-a` → 모든 PV 표시

---

### pvdisplay

PV의 상세 정보를 표시한다.

---

### pvcreate

물리 볼륨을 생성한다.

#### 주요 옵션

- `-f` → 기존 데이터를 확인하지 않고 강제로 생성

---

## 2. VG 관련 명령어

### vgscan

시스템의 VG(Volume Group)를 검색한다.

---

### vgcreate

새로운 VG를 생성한다.

#### 주요 옵션

- `-s` → PE(Physical Extent)의 크기 지정

---

### vgdisplay

VG의 상세 정보를 표시한다.

---

### vgextend

기존 VG에 PV를 추가하여 크기를 확장한다.

---

### vgreduce

VG에서 PV를 제거한다.

#### 주요 옵션

- `-a` → 사용 가능한 모든 PV를 대상으로 작업

---

### vgchange

VG의 속성을 변경한다.

#### 주요 옵션

- `-a y` → VG 활성화
- `-a n` → VG 비활성화
- `-l` → 논리 볼륨 관련 설정

---

### vgremove

VG를 삭제한다.

---

## 3. LV 관련 명령어

### lvcreate

새로운 LV(Logical Volume)를 생성한다.

#### 주요 옵션

- `-L` → LV 크기 지정
- `-l` → PE 단위로 크기 지정
- `-n` → LV 이름 지정
- `-i` → 스트라이프 개수 지정
- `-l` → 스트라이프 크기 지정
- `-s` → 스냅샷 생성

---

### lvscan

시스템의 LV를 검색한다.

#### 주요 옵션

- `-v` → 상세 정보 출력

---

### lvdisplay

LV의 상세 정보를 표시한다.

---

### lvextend

LV의 크기를 확장한다.

#### 주요 옵션

- `-L` → LV 크기를 지정하여 확장
- `+` → 기존 크기에 지정한 크기를 추가
- `-l` → PE 단위로 크기 지정
- `+` → 기존 크기에 지정한 PE를 추가

---

### lvreduce

LV의 크기를 축소한다.

#### 주요 옵션

- `-L` → LV 크기를 지정하여 축소
- `-l` → PE 단위로 크기를 지정하여 축소

---

### lvrename

LV의 이름을 변경한다.

---

### lvremove

LV를 삭제한다.

---

## 4. 기타 LVM 명령어

### pvmove

PV에 있는 데이터를 다른 PV로 이동한다.

#### 주요 옵션

- `-v` → 상세 정보 출력

---

### fsadm

파일 시스템의 크기를 조정한다.

#### 주요 옵션

- `-v` → 상세 정보 출력
- `-f` → 강제로 실행
- `-y` → 모든 질문에 yes로 응답

---

## LVM 명령어 흐름

```text
PV
├── pvcreate
├── pvscan
├── pvs
└── pvdisplay

VG
├── vgcreate
├── vgscan
├── vgdisplay
├── vgextend
├── vgreduce
├── vgchange
└── vgremove

LV
├── lvcreate
├── lvscan
├── lvdisplay
├── lvextend
├── lvreduce
├── lvrename
└── lvremove