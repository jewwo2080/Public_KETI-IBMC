# Public_KETI-IBMC 
<br/><br/>
<!--## 목차 
<br/><br/>
## 프로젝트 목적 및 용도 
- 이 프로젝트는 무엇을 위한 것인가
- 어떤 문제를 해결할 수 있는가
- 어떤 사람들이 이 프로젝트를 사용하면 좋은가
- 어떻게 작동하는가
<br/><br/>
## 프로젝트를 시작하는 방법 
프로젝트를 처음 사용하기 위해 필요한 내용
- 프로젝트를 설치, 사용하기 위해 필요한 전제조건이 있는가
- 어떻게 설치, 사용, 테스트 하는가
- 설치 가이드 문서는 어디에 있는가
  - 실행환경 ( OS, 컴파일러 혹은 하드웨어 관련 / CPU, RAM / Built with C++.. )
  - 코드 실행전 설치해야할 패키지 혹은 의존성이 걸리는 문제들<br/>
<br/><br/>
## 중요 코드파일 
해당 파일이 무슨 역할인지 설명
<br/><br/>
## 사용 방법 
프로그램을 어떻게 작동시키는가, usage example 을 함께 작성
<br/><br/>
## 버전 관리 (업데이트 내역)
<br/><br/>
## License 
<br/><br/>
## Contributing 
<br/><br/>
## Contact & Authors 
-->  

## Table of Contents

## Introduction of IBMC  
> **서버의 메인보드**에 내장된 컨트롤러로 **시스템 관리 SW와 HW간의 인터페이스**를 통해 **On Device AI**을 활용한 **지능형 소비전력 + 장애관리**를 가능하도록 하는 **펌웨어 SW 기술**  
<br/><br/>

+) 이미지
<br/><br/>

## Requirements  
IBMC를 사용하기 전 해야하는 것들  
### 1. 빌드루트 환경 구성
1. 파일 내려받기 ( 현재 위치 : /home/keti/Workspace )  
<https://buildroot.org/downloads/buildroot-2015.11.tar.gz>  

1. 내려받은 압축 파일 해제  
	```bash
	$ tar -xvzf buildroot-2015.11.tar.gz
	```
	
	1. 해당 디렉토리 진입  
	```bash
  $ cd buildroot-2015.11.tar.gz
  ```  
	
	1. KETI-IPMI.tar 압축을 풀어 ./source/ast_app 디렉토리에 복사  
  ```bash
  $ tar -xvzf KETI-IPMI.tar  
  $ cp -r KETI-IPMB ./source/ast_app  
  ```  
  
  1. prepare_buildTool.sh 를 실행
  ```bash
  $ ./prepare_buildTool.sh
  ```  
		
  
  
  buildroot 공식 홈페이지에서 권장하는 패키지와 옵션 패키지  
  - Mandatory : <https://buildroot.org/downloads/manual/manual.html#requirement-mandatory>
  - Optional : <https://buildroot.org/downloads/manual/manual.html#requirement-optional>  
  
  
  
### 2. Buildroot menuconfig  
 압축을 해제한 디렉토리에서 make menuconfig를 입력하면 Buildroot에 대한 전반적인 설정이 가능하다. 가장 먼저 아래와 같이 설정한다.
 
 1. Target Option 설정  
 > Target Architecture : ARM (little endian)  
 > Target binary Format : ELF  
 > Target Architecture Variant : arm1176jzf-s  
 > Target ABI : EABI  
 > Floating point strategy : Soft float  
 > ARM instruction set : ARM    
 
 2. Toolchain 설정  
 > Toolchain type : External toolchain  
 > Toolchain : External Toolchain -> Pre-installed toolchain  
 
 > Toolchain origin    
 	- downloaded and installed : Toolchain을 다운받을 주소 입력  
 	- Pre-installed toolchain : Toolchain이 설치된 절대경로 입력  
 
 > Toolchain path를 절대경로로 변경  
 	- Toolchain 경로 : /home/keti/Workspace/buildroot-2015.11/source/armv6-aspeed-linux-gnueabi  
 
 > Toolchain prefix 입력  
 	- ex) armv6-aspeed-linux-gnueabi  
 
 > External toolchain gcc version  
 	- External toolchain의 gcc 버전 확인 후 해당 버전으로 설정
```bash
$ ./armv6-aspeed-linux-gnueabi-gcc –v
```

  
> External toolchain C library를 glibc/eglibc로 변경
> 기타 Toolchain 설정  



### 3. KETI-IPMI 빌드

#### AST_2500
```bash
$ make toolchain
$ make
$ cd /home/keti/Workspace/buildroot-2015.11/source/ast_app
$ ./sk_make.sh
```

#### AST_2600
```bash
$ cd /home/keti/BMC_SDK
$ cmake CMakeLists.txt
$ make
   
 


## Files
- 중요한 코드파일 역할 설명

## How To Use IBMC

## Usage Example

## License










