## RPM 패키지 파일명

RPM 패키지 파일은 일반적으로 다음과 같은 형식으로 구성된다.

`패키지이름-버전-릴리즈.리눅스버전.아키텍처.rpm`

예:

`httpd-2.4.57-8.el9.x86_64.rpm`

| 구성 요소 | 설명 | 예시 |
|---|---|---|
| 패키지이름 | 설치할 패키지의 이름 | `httpd` |
| 버전(Version) | 패키지 자체의 버전 | `2.4.57` |
| 릴리즈(Release) | 동일 버전에서 패키지가 몇 번째로 배포되었는지 나타냄 | `8` |
| 리눅스 버전 | 해당 패키지가 만들어진 배포판 또는 배포판 계열을 나타냄 | `fc38`, `el8`, `el9`, `centos` |
| 아키텍처(Architecture) | 패키지가 실행될 CPU 아키텍처를 나타냄 | `x86_64` |
| `.rpm` | RPM 패키지 파일임을 나타내는 확장자 | `.rpm` |

### 리눅스 버전 표기 예시

| 표기 | 의미 |
|---|---|
| `fc38` | Fedora 38 |
| `el8` | Enterprise Linux 8 계열 |
| `el9` | Enterprise Linux 9 계열 |
| `centos` | CentOS 계열 |

### 아키텍처 표기 예시

| 표기 | 설명 |
|---|---|
| `i386` | Intel 80386 계열 32비트 |
| `i486` | Intel 80486 계열 32비트 |
| `i586` | Intel Pentium 계열 32비트 |
| `i686` | Intel Pentium Pro 이상 계열 32비트 |
| `ia64` | Intel Itanium 64비트 |
| `x86_64` | x86 기반 64비트 |
| `alpha` | DEC Alpha 계열 |
| `ppc` | PowerPC 계열 |
| `ppc64` | PowerPC 64비트 |
| `sparc` | SPARC 계열 |
| `s390` | IBM System/390 계열 |
| `aarch64` | ARM 64비트 |

> **시험 포인트**
>
> - `i386`, `i486`, `i586`, `i686` → x86 **32비트 계열**
> - `x86_64` → x86 **64비트**
> - `ia64` → **Itanium** 계열
> - `alpha` → **Alpha** 계열
> - `ppc` → **PowerPC** 계열