# Public_KETI-IBMC 
<br/>


## Table of Contents
1. [Introduction of IBMC](#introduction-of-ibmc)
2. [Requirements](#requirements)  
	2.1. [Buildroot 환경 구성](#1-buildroot-환경-구성)  
	2.2. [Buildroot menuconfig](#2-buildroot-menuconfig)  
	2.3. [KETI-IPMI 빌드](#3-keti-ipmi-빌드)  
	2.4. [이미지 빌드](#4-이미지-빌드)  
	2.5. [BMC에 이미지 쓰기](#5-bmc에-이미지-쓰기)  
3. [Usage](#usage)  
	3.1. [KETI-IPMI 실행](#1-keti-ipmi-실행)  
	3.2. [IPMItool](#2-ipmitool)
	3.3. [KETI-REST 실행](#3-keti-rest-실행)  
	



## Introduction of IBMC

<br/><br/>

![no image](https://lh3.googleusercontent.com/fife/AAbDypCtK6BI63Yy9-Xu94yEFQKfSzcNHH43DU-EPHJSTTorhtJB_9J7Ut_HWCH-LnnfglWS5kZSpDrgyQ9F3ptpsF747MxiuJCcs_tY4m-Qhwlv7_Qa6k6FSSv8kgAIuvUTaHDPqy3XlyrvuVsFHA2O9QMQqR8kAy_i800Pm4JmWmVF6LBp1vG751Ek_hoEcTQZJRtgSqcW03AHVf8fpcSz9eYVbPrvMaP2l1zM3Rb6qN0vY-qCZkgVQ04W8loI5pWx8AlwuQKBa6OwTSo6fWBnuGgyDDsVOstmer17P-qmRwEa1LqmX0JyowPcf1-l9aD0sx64STwABXDsJFLRXmHNGnw-nqhAyNfztobJbrI9lbC9KhIlsXr2Om-CDDobYm0X2tI3ZcVREvVAtVU-exo7USpLBJPZVWzEtu5fNVrnefcLXAiRLebS2kMbbvZdTKFzG-O13lwqTzk58ykXC1yl_2di808JYdG5A9ARHm9MTrH1FKYqQ_G5RMiopVfvzZpOvQExprQIyR2i3v7ZwmZCLUlEL4NJh59dqlMJ4NzDf99Lq7579AmnwAVNp5A98tuAQW9egIOp4bahv0YhylBvqG5Z_43o-0c8ok71lWKzbm1lvU9Ps975op3j-VW0vRApj49RVIo0GFCJtXoRpKrPi6x73ETmB7hQsIV-8jL1Tf1hVm82yinJ5xe-87iVJopw9FUBy5pf5zzIhX905HyCCAY6oS1T6Nb1vcFUMNUQSMw77QDHqjifXk6Z8M44XgAi-EEkbS2dqQonUxOXJHPUWtXPSGt_8kvl4gYsCboq-SBaZyib4OOIYSYkM0DUIysEFIdVfiz9uq0pXUoFiFNQSyOPsbHoL0E-y4W0NcXfHOhmTQ6HeQsDsmirES61r5m5oVzOqTZE4UCtWMxwF5jgeeO7hwJfTfwkhpRXdkraz6ZkdgpFeI5QFm4qzfqopqFSDgcQ2LI6qIHso9tgaec-bQbGIDBruRdKbSQffwqt9y1SSNG1waBaw4GQW5-DkrP71OJVNQGz2QQiwyEQuTCzprp9t3TxBwmFe1EgkQNSGrM4Bv5OFvWj3KdOAZhaqJdnPU7CXXKL74PVS48GZo3DytRuAE-HntTj8eyrHQbuaibVi2CeAL1lo2tYOM_FANOKENfoos2AqKglSxsOt43VcytGfH4Eow2H5IXW15_aPvNn4J7oiveS9e7bs_7gdXw7Ztze1qHFlv9Xc0R7imlYkfoxqKRsElJcS5yzCqr1oiFqRAenAKz1R_andpj4vNVnp1kRZ4CK7kJrl84j9bK0I-x8HGaSaHFpOYw6q7nd4F5Op9eCI94ybOtChKwzT4Ous06X8PTaVTtdrcGMK0WcQMKJ_1m7itLdTBYfgIKWkfCuWpJdy-nECOYGM6CPx0iPFfUMfkb3ZqNjWV9m-oMG1DIQVIYSRp0xwJ8inLwLjDrtkMcyqUav6lizgXrPpv-fFmfkQC2DnsjcjHUJed0=w1278-h1307)  

<br/><br/>
>**서버의 메인보드에 내장된 컨트롤러로 시스템 관리 S/W와 H/W간의 인터페이스를 통해 On Device AI을 활용한 지능형 소비전력 + 장애 관리 펌웨어 SW 기술**   

<br/><br/>

## Requirements  

### 1. Buildroot 환경 구성
1. 파일 내려받기 ( 현재 위치 : /home/keti/Workspace )  
<https://buildroot.org/downloads/buildroot-2015.11.tar.gz>  

1. 내려받은 압축 파일 해제  
```bash
$ tar -xvzf buildroot-2015.11.tar.gz
```
	
3. 해당 디렉토리 진입  
```bash
$ cd buildroot-2015.11.tar.gz
```  
	
4. KETI-IPMI.tar 압축을 풀어 ./source/ast_app 디렉토리에 복사  
```bash
$ tar -xvzf KETI-IPMI.tar  
$ cp -r KETI-IPMB ./source/ast_app  
```  
  
5. prepare_buildTool.sh 를 실행
```bash
$ ./prepare_buildTool.sh
```  
		
- Buildroot 공식 홈페이지에서 권장하는 패키지와 옵션 패키지  
	- Mandatory : <https://buildroot.org/downloads/manual/manual.html#requirement-mandatory>
	- Optional : <https://buildroot.org/downloads/manual/manual.html#requirement-optional>  
<br/><br/>
  
  
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
```bash
External toolchain의 gcc 버전 확인    
$ ./armv6-aspeed-linux-gnueabi-gcc –v  

확인 후 해당 버전으로 설정
```

  
> External toolchain C library를 glibc/eglibc로 변경
> 기타 Toolchain 설정  

<br/><br/>


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
```

### 4. 이미지 빌드
<br/>

```
Buildroot로 이미지 빌드
$ ./build_option.sh
빌드한 이미지는 ./output/images/all.bin 파일로 생성됨
```

### 5. BMC에 이미지 쓰기
#### AST2500(2600)-EVB
1. 빌드한 이미지 파일을 FTP로 다운받아 Windows 10 디렉토리로 옮김
2. AST2500 Evaluation Board의 좌측에 점퍼 케이블 중 오른쪽 핀을 빼서 GND에 연결하여 BMC Booting을 Disable 
3. 좌측 상단에 GND 핀에 점퍼 케이블을 연결
4. SF100-ISP Programmmer를 BMC ROM에 연결
5. AST2500 Evaluation Board 전원 켜기
6. Dediprog Engineering 소프트웨어를 실행시킨 뒤 Memory Type을 설정
7. Load file 버튼을 클릭하여 다운받은 all.bin 파일을 불러옴
8. Erase 버튼을 클릭하여 롬을 초기화한 뒤 Prog 버튼을 클릭하여 새 이미지를 기록
9. BMC Booting 점퍼 와이어를 다시 연결하고 SF100-ISP Programmer를 제거
10. 전원 인가

#### 32MB/64MB ROM
1. 펌웨어를 기록할 ROM을 칩 좌측 상단의 점(1번 핀)을 기준으로 장착
2. SF100 ISP Programmer에 롬을 장착한 뒤 PC에 연결
3. Dediprog Engineering을 실행한 뒤 장착한 ROM의 모델명을 선택
4. 좌측 상단의 File 버튼을 클릭하여 기록할 펌웨어 이미지 파일을 선택
5. Batch 버튼을 클릭하여 이미지를 기록
6. 기록이 완료되면 서버보드의 BMC ROM 장착 위치에 방향이 맞게 장착



## Usage

### 1. KETI-IPMI 실행
```bash
$ KETI-IPMI
```

### 2. IPMItool  
- 사용할 Host Server에 IPMItool 설치  
```bash
$ apt-get install -y ipmitool
```
- BMC의 Administrator 계정은 ID : admin, Password : admin으로 설정되어있음  
```bash
IPMItool 기본 사용법
$ ipmitool –I <lan/lanplus> -H <BMC IP Address> -U <User ID> -P <User Password> <command>
```
> IPMItool 명령어 <https://docs.oracle.com/cd/E40704_01/html/E40350/z400000c1016683.html>  

<br/>  

### 2. KETI-REST 실행
```bash
# 8000번 포트 사용
$ restful_server
```  

### 3. KETI-REST 지원 API 리스트 및 URL
- System Information  

|   ID   |    URL   |   Method   |                   상세기능                 |
| ------ | -------- | ---------- | ------------------------------------------ |
|  ST01  | /sysinfo |    GET     |        IPMI 및 BMC 정보 제공                |


<br/>

- FRU Information  

|   ID   |    URL   |   Method   |               상세기능        |     
| ------ | -------- | -----------|------------------------------- |
|  FU01  |   /fru   |     GET    |    BMC FRU 정보 제공            |
|  FU02  |   /fru   |     PUT    |    BMC FRU 정보 수정             |

<br/>

- Server Health  

|   ID   |    URL   |   Method   |                       상세기능                       |     
| ------ | -------- | -----------   |---------------------------------------------------- |
|  SH01  |   /sensor   |     GET    |    센서 상태 정보 제공                            |
|  SH02  |   /sensor   |     PUT    |    센서 Threshold 값 수정                         |
|  SH03  |   /event    |     GET    |    BIOS, Sensor, System Event Log 정보 제공       |

- Configuration

|   ID      |   URL    |   Method    |                   상세기능                        |
|---------- |----------|-------------|---------------------------------------------------|
|  CF01      |   /ddns    |     GET    |         Dynamic DNS 설정 정보 제공                      |  
|  CF02      |   /ddns     |    POST     |        Dynamic DNS 설정 정보 수정                       |  
|  CF03      |    /network    |    GET     |        BMC 네트워크 정보 제공                       |  
|  CF04      |    /network    |    POST     |       BMC 네트워크 정보 수정                        |  
|  CF05      |   /ntp     |   GET      |            NTP(Network Time Protocol) 정보 제공                   |  
|  CF06      |   /ntp     |   POST      |           NTP 설정 정보 수정 (자동 / 수동)                    |  
|  CF07      |   /smtp     |   GET      |           SMTP(Simple Message Transfer Protocol) 정보 제공                    |  
|  CF08      |   /smtp     |   POST      |          SMTP 설정 정보 수정                     |  
|  CF09      |   /ssl     |   POST      |          SSL 인증서 생성                     |  
|  CF10      |   /ssl     |   GET      |          SSL 인증서 정보 제공                    |  
|  CF11      |   /activedir     |   GET      |          Active Directory 그룹 정보 제공                 |  
|  CF12      |   /activedir     |   POST      |          Active Directory 그룹 추가                 |  



## Files
- 중요한 코드파일 역할 설명


## Usage Example

## License










