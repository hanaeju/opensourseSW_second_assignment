## opensourseSW_assignment2

### top
* 시스템의 상태를 가장 빠르게 파악 가능하다(CPU, Memory, Process)
* 옵션 없이 입력하면 interval 간격(기본 3초)으로 화면을 갱신하며 정보를 보여준다.
* top 실행 전 옵션
  + 순간의 정보를 확인하려면 ```-b``` 옵션 추가(batch mode)
  + ```-n``` : top 실행 주기 설정(반복 횟수)
  
* 실행 후 명령어
  + shift + p : CPU 사용률 내림차순
  + shift + m : Memory 사용률 내림차순
  + shift + t : Process가 돌아가고 있는 시간순
  + k : kill.k 입력후 PID 번호 작성, signal은 9
  + f : sort field 선택 화면 -> q 누르면 RES순으로 정렬
  + a : Memory 사용량에 따라 정렬
  + b : Batch mode로 작동
  + 1 : CPU Core별로 사용량 보여줌
 
* ps와 top의 차이점
  + ps는 ps한 시점에 process에서 검색한 CPU 사용량
  +  top은 process에서 일정 주기로 합산해 CPU 사용률 출력

* ```top -b -n 1```

![top -b -n 1](https://user-images.githubusercontent.com/98371516/168509598-a8527ca7-6750-4c7c-8031-b68191ced0f1.PNG)

* 1:41은 1시간 41분 전에 서버가 구동되었음을 의미한다.
* load average : 현재 시스템이 얼마나 일을 하는 지를 나타냄. 3개의 숫자는 1분,5분, 15분간의 평균 실행/대기 중인 프로세스의 수. CPU Core 수 보다 적으면 문제 없음
* Tasks : Process의 개수
* KiB Mem, Swap : 각 Memory의 사용량
* PR : 실행 우선 순위
* VIRT, RES, SHR : Memory 사용량 => 누수 check 가능
* S : Process Status(작업중, I/O 대기, 유휴 상태 등)

### VIRT, RES, SHR
* 현재 Process가 사용하고 있는 Memory
* VIRT
  + Process가 사용하고 있는 virtual memory의 전체 용량
  + Process에 할당된 virtual memory 전체
  + SWAP + RES

* RES
  + 현재 Process가 사용하고 있는 물리 메모리의 양
  + 실제로 memory에 올려서 사용하고 있는 물리적 memory
  + 실제로 memory를 쓰고있는 RES가 핵심이다.

* SHR
  + 다른 Process와 공유하고 있는 shared memory의 양
  + 예시로 라이브러리를 들 수 있음. 대부분의 linux process는 glibc라는 라이브러리를 참고하기에 이런 라이브러리를 shared memory에 올려서 사용
 
 ### Memory Commit
 * Process가 커널에게 필요한 메모리를 request하면 커널은 프로세스에 메모리 영역을 주고 실제로 할당은 하지 않으나 해당 영역을 process에게 주었다는 것을 save해두는 과정
 * 왜 커널은 process의 memory request에 따라 즉시 할당하지 않고 Memory Commit과 같은 기술을 사용하여 request를 delay 시키는가?
   + fork()와 같은 새로운 process를 만들기 위한 call을 처리해야 하기 때문
   + fork() 시스템 call을 사용하면 커널은 실행중인 process와 동일한 process를 하나 더 만들고, exec() system call을 통해 다른 프로세스로 변함. 이때 확보한 memory가 쓸모 없어질 수 있다.
   + COW(Copy-On-Write) 기법을 통해 copy된 memory 영역에 실제 write 작업이 발생한 후 실질적인 memory 할당을 진행

### Process Status
* SHR 옆에 있는 S 항목으로 볼 수 있음
  + D : Uninterruptiable sleep. disk or network I/O를 대기
  + R : 실행 중(CPU 자원을 소모)
  + S : Sleeping, request한 resource를 즉시 사용 가능
  + T : Traced or Stopped. 보통의 system에서 자주 볼 수 없는 상태
  + Z : Zombie. 부모 process가 죽은 자식 프로세스
 
 ---
 
 ### 아래의 문서를 참고하여 작성하였습니다.
 [top] https://zzsza.github.io/development/2018/07/18/linux-top/
 
 
