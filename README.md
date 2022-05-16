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
