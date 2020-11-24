# Mutex VS Semaphore(2020.11.15)
## Mutex
- 공유된 자원의 데이터를 여러 스레드가 접근하는 것을 막는 것
- 상호배재라고도 하며, Critical Section을 가진 스레드의 Running time이 서로 겹치지 않도록 각각 단독으로 실행하게 하는 기술이다. 
- 다중 프로세스들의 공유 리소스에 대한 접근을 조율하기 위해 synchrinized 또는 lock을 사용한다. 즉, 뮤택스 객체를 두 스레드가 동시에 사용할 수 없다.

## Semaphore
- 공유된 자원의 데이터를 여러 스레드가 접근하는 것을 막는 것
- 리소스 상태를 나타내는 간단한 카운터로 생각할 수 있다.
	- 운영채제 또는 커널의 한 지정된 저장장치 내의 값이다.
	- 일반적으로 비교적 긴 시간을 확보하는 리소스에 대해 이용한다.
	- 유닉스 시스템 프로그레밍에서 세마포어는 운영체제의 리소스를 경쟁적으로 사용하는 다중 프로세스에서 행동을 조정하거나 또는 동기화 시키는 기술이다. 
- 공유 리소스에 접근할 수 있는 프로세스의 최대 허용치만큼 동시에 사용자가 접근하여 사용할 수 있다. 
- 각 프로세스는 세마포어 값을 확인하고 변경할 수 있다. 
	- a. 사용 중이지 않는 자원의 경우 그 프로세스가 즉시 자원을 사용할 수 있다.
	- b. 이미 다른 프로세스에 의해 사용 중이라는 사실을 알게 되면 재시도하기 전에  일정 시간을 기다려야 한다. 
	- 세마포어를 사용하는 프로세스는 그 값을 확인하고, 자원을 사용하는 동안에는 그 값을 변경함으로써 다른 세마포어 사용자들이 사용하도록 기다려야 한다. 
- 세마포어는 이진수(0 또는 1)를 사용하거나, 또는 추가적인 값을 가질 수도 있다. 

## 차이점
- 가장 큰 차이점은 관리하는 **동기화 대상의 개수**
	- Mutex는 동기화 대상이 오직 하나뿐일 때, Semaphore는 동기화 대상이 하나 이상일 때 사용한다. 
- Semaphore는 Mutex가 될 수 있지만 Mutex는 Semaphore가 될 수 없다. 
	- Mutex는 상태가 0,1 두 개 뿐인 binary Semaphore
- Semaphore는 소유할 수 없는 반면, Mutex는 소유가 가능하며 소유주가 이에 대한 책임을 가진다. 
	- Mutex의 경우 상태가 두개 뿐인 lock이므로 lock을 가질 수 있다. 
- Mutex의 경우 Mutex를 소유하고 있는 스레드가 이 Mutex를 해제할 수 있다. 하지만 Semaphore의 경우 이러한 Semaphore를 소유하지 않는 스레드가 Semaphore를 해제할 수 있다. 
- Semaphore는 시스템 범위에 걸쳐있고 파일 시스템 상의 파일 형태로 존재하는 반면 Mutex는 프로세스 범위를 가지며 프로세스가 종료될 때 자동으로 Clean Up 된다.         
