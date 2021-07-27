영상: [컴퓨터시스템구조 CSA-5 Part-5](https://youtu.be/4CKJs6s2OGI?list=PLc8fQ-m7b1hD4jqccMlfQpWgDVdalXFbH)

## [제 5장 Part-5,6](https://youtu.be/4CKJs6s2OGI?list=PLc8fQ-m7b1hD4jqccMlfQpWgDVdalXFbH)

### [입출력과 인터럽트 (Input-Output and Interrupt)](컴퓨터-구조/5장-기본-컴퓨터의-구조와-설계-Part2/입출력과-인터럽트.md)

- 입출력 구성

  - CPU와 IO 장치의 속도 차이 제어를 위하여 Flag 사용 : IO 장치가 CPU에 비해 현저히 느림
    - Buffer overrun
    - Buffer underrun
  - FGI
    - 1 : 입력 가능한 상태
    - 0 : 입력 블러킹
  - FGO
    - 1 : 출력 가능한 상태
    - 0 : 출력장치 사용중
  - 인터럽트
    - 인터럽트란 곧 입출력이다 -> 입출력 발생 시 인터럽트 유발
    - IEN flag (Interrupt Enable flag) : 입출력을 받을지 결정하는 장치, 1인 경우 입출력 가능 
    - IEN flag에 의하여 제어 
    - 입출력 전체를 제어

  ![image-20210727233335228](5장-기본-컴퓨터의-구조와-설계-Part2.assets/image-20210727233335228.png)

  - 어느 비트가 1인지에 따라 어떤 I/O인지 알 수 있음

![image-20210727234047480](5장-기본-컴퓨터의-구조와-설계-Part2.assets/image-20210727234047480.png)

## [제 5장 Part-7](https://youtu.be/693iK8vB7XU?list=PLc8fQ-m7b1hD4jqccMlfQpWgDVdalXFbH)

### 컴퓨터에 대한 완전한 기술 (Compute Computer Description)

- 

## [제 5장 Part-8](https://youtu.be/pUrzmOqsV58?list=PLc8fQ-m7b1hD4jqccMlfQpWgDVdalXFbH)

### 기본 컴퓨터의 설계 (Design of Basic Computer)

- 

### 누산기 논리의 설계 (Design of Accumulator Logic)

- 

### 수행 과제

-