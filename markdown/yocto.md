

# Yocto Project

### A Linux Foundation project that acts as an umbrella for various efforts to improve Embedded Linux.

 - Yocto Project는 자신만의 임베디드 리눅스를 만들기 위한 도구, 템플릿등을 제공하는 여러 작은 프로젝트를 가지고 있다.

 - Yocto Project가 제공하는 Tool을 사용하여 커널, 부트로더, 파일시스템 등과 같은 운영체제 구성요소를 쉽게 빌드하여 하나의 이미지로 묶어 운영체제를 만든다.

 - Yocto Project 아래 포키(pocky), 비트베이크(bitbake)와 같은 하위 프로젝트들이 있다.
 
 - Yocto Project의 근간이 되는 오픈임베디드(OpenEmbedded)를 사용하여 원하는 패키지를 이미지에 추가하고, 필요한 패키지를 OpenEmbedded 문법에 맞도록 구성할 수 있다. 
 
.

.
 
# OpenEmbedded

### The build system architecture promoted by the Yocto Project.

.

.
 
# 포키(pocky)

### A reference distribution used for test and release purposes by the Yocto Project.

 - Yocto Project 레퍼런스 시스템 (Bitbake + OpenEmbedded Core + Yocto Reference BSP 등)

 - Pocky는 비트베이크, 오픈임베디드코어, 메타데이터를 사용하여 크로스 컴파일을 수행한다.
 
 - Bitbake와 각종 OE component를 조합하여 POKY라 불리는 reference distribution을 만듦.
 
 - Pocky는 리눅스를 만들기 위해 수천 가지의 오픈 소스 프로젝트를 빌드하고, 조합하기 위한 메커니즘을 제공한다.
 
.

.

# 비트베이크(bitbake)

### A tool that reads metadata and runs tasks.

 - Bitbake는 파이썬과 쉘 스크립트가 함께 섞여 스크립트를 파싱하는 작업 스케줄러이다.
 
 - GNU Make와 비슷하다고 함.
 
### Bitbake가 Tasks를 수행하기 위해 Parsing하는 파일
 - recipes (.bb)
 - append (.bbappend) – 빌드 정보를 recipe 파일에 더하는 파일
 - class (.bbclass)
 - configuration (.conf)
 - include (.inc)
 - BitBake에 어떤 Task를 실행할 지와 Task간  종속성에 대한 정보를 제공
 
.

.
 
# 오픈 임베디드 코어(open embedded core)

### The common base set of metadata that BitBake uses. This metadata is shared between OpenEmbedded and the Yocto Project.

 - 기본적인 Recipe와 전체 OpenEmbedded 관련 기본 구조가 있음. Makefile과 비슷하다고 생각하면 됨.

 - Open embedded core는 포키 빌드 툴의 핵심이며 주요 기능을 제공한다.
 
 - ARM, x86, x86-64, MIPS, MIPS64 (다른 CPU?) 프로세스 아키텍처를 지원한다.
 
.

.
 
# 메타 데이터 (meta data)

 - Meta data는 파이썬과 쉘 스크립트의 혼합으로 만들어진 유연한 시스템이다.
 
 - Meta data는 오픈 임베디드 코어를 확장한다.
 
 - Meta data는 여러 종류로 나뉘어 지는데, 환경설정파일(*.conf), 클래스파일(*.bbclass), 레시피파일(*.bb, *.bbappend)로 구성된다. GNU Make의 makefile과 비슷한느낌이라고 한다.
 
### Recipe

 - Software/Image를 빌드하기 위한 Logical units
 
 - 소스코드가 어디에 있는지 어떻게 patch할지/compile할지 정의
 
### Meta Layer

 - Meta data를 구조화하여 관리할 목적으로 Layer Folder가 구성됨.
 
<http://layers.openembedded.org/layerindex/branch/master/layers/>



