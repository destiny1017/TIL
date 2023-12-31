## 가상 메모리와 페이지 교체 알고리즘
- - -
### 가상메모리(Virtual Memory)

![img.png](../assets/virtual_memory.png)

가상메모리란 메인 메모리(RAM)의 한정된 공간의 문제를 해결하기 위한 메모리로, 
프로세스에 이용되는 메모리를 추상화하여 효율적으로 메모리를 사용하게하는 기술이다.
가령 30Mb의 메모리를 사용하는 프로세스를 구동시킨다면, 모든 순간에 항상 30bM의 데이터가 필요하지는 않을 것이므로
가장 중요하고 빈번하게 사용되는 10M의 데이터만을 메인 메모리에 로드 시킨뒤, 나머지 20M의 데이터는
추상화하여 가상메모리에 물리 주소만을 남겨두는 방식으로 동작한다.

- #### 요구페이징(Demand Paging)
  
  ![img_1.png](../assets/demand_paging.png)
  
  위 설명에서 말했듯 프로그램 실행에 모든 메모리가 필요한 것은 아니기에, 프로그램 실행에 필요한 부분과 필요하지 않은 부분을 
  페이지로 나누어 필요한 페이지만 메모리에 적재하는 기술이 요구 페이징이다. 당장 필요 없는 페이지들은 Backing Store에 저장해뒀다가
  해당 페이지가 필요해지면 메모리에 올리게 된다.
  
  프로그램 실행시 필요할 것 같은 페이지를 미리 메모리에 올려놓는 방식을 pre-paging이라고 하고, 필요해지기 전까지는
  어떠한 페이지도 메모리에 올리지 않고 실행하는 것을 Pure demand paging이라 한다.

- #### Valid-Invalid Bit
  ![img_2.png](../assets/demand_paging2.png)  
  요구 페이징 기법을 사용하면, 페이지 테이블의 데이터는 메모리 또는 Backing Store에 존재하게 된다.
  Backing Store에 존재한다면 물리 메모리에 적재하는 과정을 거쳐야하므로, 현재 페이지가 어떤 상태인지 판단할 flag값이 필요한데,
  이를 valid-invalid bit라고 하며, 페이지 테이블에는 기본적으로 페이지와 이 v/i bit가 존재하게 된다.
  valid(1) invalid(0) 상태로 구분하며, 페이지 테이블 접근시 만일 invalid 상태라면 페이지 부재(Page Fault)가 발생하게 된다.   


- #### Page Fault
  ![img_3.png](../assets/page_fault.png)
  1. MMU(Memory Management Unit)가 Page Fault를 발생시키면, OS는 backing store에서 해당 페이지를 찾는다
  2. 만일 이 과정에서 페이지가 존재하지 않는다면 부적절한 참조(Invalid Reference)로 판단하고 프로세스를 중지한다.
  3. backing store에 존재한다면 물리 메모리의 프레임(frame)에 페이지를 읽어오는데, 
     만일 빈 프레임이 없다면 페이지교체 알고리즘에 따라 기존 페이지를 교체한다
  4. 위 작업이 끝나면 페이지 테이블을 리셋하여 valid-invalid 상태를 업데이트 한다
  5. 프로세스를 다시 실행한다.


### 페이지 교체 알고리즘

페이지 교체 알고리즘이란 요구페이징 도중 Page Fault가 발생했을 때, 메인 메모리에 빈 프레임이 없을 경우
점유중인 프레임중 교체되기에 가장 적합한 프레임을 찾는 알고리즘이다. 여러 방식의 알고리즘이 있지만
모두 궁극적으로는 Page Fault 발생을 줄이는 데에 목적을 두고 있다.

- #### 1. FIFO(First In First Out) 알고리즘
  ![img.png](../assets/fifo_algo.png)
  - FIFO 알고리즘은 말그대로 먼저 들어온 페이지를 먼저 교체하는 방식이다.
  - 구현이 간단하지만 성능은 떨어지는 편이다.
  - **Belady's Anomaly*** 현상이 발생할 수 있다.
    * Belady's Anomaly : 메인 메모리에 적재된 프레임의 개수가 많아져도 오히려 Page Fault가 늘어나는 현상

- #### 2. LRU(Least Reacently Used) 알고리즘
  ![img_1.png](../assets/LRU_algo.png)
  - LRU 알고리즘은 가장 오랫동안 참조되지 않은 프레임을 교체하는 알고리즘이다.
  - 최적 알고리즘과 비슷한 효과를 낼 수 있다.
  - 성능이 좋아 많은 운영체제에서 채택중인 알고리즘이다.

- #### 3. LFU(Least Frequently Used) 알고리즘
  ![img_2.png](../assets/LFU_algo.png)
  - LFU 알고리즘은 가장 참조횟수가 적은 프레임을 교체하는 알고리즘이다.
  - 최소 참조횟수가 동일한 프레임이 여러개라면 가장 오래된 프레임을 교체한다.
  - LRU가 최근의 시점만을 기준으로 판단하는 반면 LFU는 오랜 기간의 참조기록을 반영할 수 있다.
  
- #### 4. NUR(Not Used Recently) 알고리즘
  ![img_3.png](../assets/NUR_algo.png)
  - LRU 알고리즘을 변형한 알고리즘으로, 오랫동안 참조되지 않은 페이지를 교체하지만 가장 오래된 페이지를 교체한다는 보장은 없다.
  - 페이지마다 변형비트와 참조비트가 존재하여 해당 비트들의 조합으로 교체 대상을 선정한다.
  - 참조되지도, 수정되지도 않은 페이지가 최우선 교체대상이다.


### 스레싱(Thrashing)

스레싱이란 멀티프로그래밍 환경에서 CPU의 이용률이 낮아지면 이용률을 높이기 위해 프로세스를 추가 할당하는 과정에서 발생하는 문제점이다.
CPU이용률이 낮다는 것은, 현재 스케줄링 중인 프로세스들이 I/O작업 비중이 높아 모두 중지 상태로 빠지고 대기큐에 프로세스가 하나도 남지 않는 상황이 발생한다는 뜻이다.
그러므로 운영체제는 프로세스를 더 할당해서 이 준비큐를 채워 CPU 이용률을 높이려 하는데, 문제는 I/O작업이 프로세스의 작업 처리중에 발생한 I/O외에도 페이지 교체중 Page Fault발생 시 디스크 스왑으로 인한 작업도 I/O라는 데에 있다.
즉 Page Fault가 높아지면 스왑으로 인한 I/O작업이 빈번해져 운영체제가 프로세스를 더 채워넣게 되는데, 프로세스가 늘어날 수록 디스크에 내려놓아야하는 페이지도 더 많아지므로 Page Falut비율은 더 상승하게 된다.\
그럼 더 상승한 Page Fault비율로 인해 운영체제는 프로세스를 또 추가 할당하고, page falut는 더 높아지고하는 악순환이 발생하게 되는데, 이것을 스레싱이라고 하는 것이다.
  
***프로세스 증가에 따른 CPU 이용률 저하 그래프**  
![img.png](../assets/Thrashing.png)  
  
그리고 이런 스레싱을 해결하기 위한 기법으로는 **워킹셋 알고리즘**과 **페이지 부재 빈도 알고리즘**이 있다.  

#### 워킹셋(Working set) 알고리즘
워킹셋이란 프로그램의 수행중에 자주 참조되는 메모리는 특정 구간 내로 정해져있다는 개념을 기반으로, 이렇게 같은 작업 수행중에 동시에 참조되는 데이터들을 묶은 것을 워킹셋이라고 한다.
워킹셋 알고리즘을 사용하면 참조 확률이 높은 데이터가 같이 메모리에 올라가있기 때문에 페이지 부재율이 줄어들며, 만일 하나의 워킹셋이 올라갈 공간이 없는 경우에는 워킹셋 전체를 올리지 않기 때문에 더욱 효과적으로 참조하게 된다.
이러한 동시 참조 영역을 주로 지역성이라고 하며, 워킹셋은 이러한 지역성을 기반으로 구성된다.
  
#### 페이지 부재 빈도 알고리즘(PFF, Page Fault Frequently)
![img_1.png](../assets/PFF.png)
페이지 부재 빈도 알고리즘이란 프로세스별 페이지 부재율을 주기적으로 조사하여, 특정 값을 기준으로 프로세스별 페이지 프레임 할당량을 조절하는 알고리즘이다.
프로세스의 페이지 부재율이 정해진 상한값을 넘어가면 이는 해당 프로세스에 할당된 페이지 프레임이 적어서 그렇다고 판단하고 추가적으로 페이지 프레임을 할당하며,
부재율이 정해진 하한값 이하로 내려가면 해당 프로세스에 할당된 페이지 프레임이 너무 많다고 판단하고 페이지를 줄이는 식으로 동작한다.
이런식으로 프레임을 조절하면 페이지 부재율이 특정구간 내에서 일정하게 유지되므로 스레싱이 예방된다.

