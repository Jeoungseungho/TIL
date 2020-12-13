# Bitmask(2020.12.13)
> 집합의 요소들의 구성 여부를 표현할 때 유용한 테크닉

## 사용 이유
- DP나 순열 등, 배열 활용만으로 해결할 수 없는 문제


- 작은 메모리와 빠른 수행시간으로 해경이 가능 (But, 원소의 수가 많지 않아야 한다.)
- 집합을 배열의 인덱스로 표현할 수 있다.

- 코드가 간결해진다. 

## 비트(Bit)란?
- 컴퓨터에서 사용되는 데이터의 최소 단위(0과 1), 이진법을 생각하면 된다. 

## 비트마스킹 활용
> 0,1로, flag 활용 
[1, 2, 3, 4 ,5] 라는 집합이 있다고 가정해보자.

여기서 임의로 몇 개를 골라 뽑아서 확인을 해야하는 상황이 주어졌다. (즉, 부분집합을 의미)

	{1}, {2} , ... , {1,2} , ... , {1,2,5} , ... , {1,2,3,4,5}
	
물론, 간단히 for문 돌려가며 배열에 저장하며 경우의 수를 구할 순 있다.

하지만 비트마스킹을 하면, 각 요소를 인덱스처럼 표현하여 효율적인 접근이 가능하다.

	[1,2,3,4,5] → 11111
	[2,3,4,5]   → 11110
	[1,2,5]     → 10011
	[2]         → 00010
	
	
집합의 i번째 요소가 존재하면 1, 그렇지 않으면 0을 의미하는 것이다.

이러한 2진수는 다시 10진수로 변환도 가능하다.

11111은 10진수로 31이므로, 부분집합을 정수를 통해 나타내는 것이 가능하다는 것을 알 수 있다.

이로써, 해당 부분집합에 i를 추가하고 싶을때 i번째 비트를 1로만 바꿔주면 표현이 가능해졌다.

이런 행위는 비트 연산을 통해 제어가 가능하다.
	
## 비트 연산 
- AND(&) : 대응하는 두 비트가 모두 1일 때, 1 반환

- OR(|) : 대응하는 두 비트 중 모두 1이거나 하나라도 1일때, 1 반환

- XOR(^) : 대응하는 두 비트가 서로 다를 때, 1 반환

- NOT(~) : 비트 값 반전하여 반환
- SHIFT(>>, <<) : 왼쪽 혹은 오른쪽으로 비트 옮겨 반환
	- 왼쪽 시프트 : `A * 2^B`
	- 오른쪽 시프트 : ` A / 2^B`
		
				[왼  쪽] 0001 → 0010 → 0100 → 1000 : 1 → 2 → 4 → 8
		
				[오른쪽] 1000 → 0100 → 0010 → 0001 : 8 → 4 → 2 → 1 
				

### 1. 삽입 
현재 이진수로 `10101`로 표현되고 있을 때, i번째 비트의 값을 1로 변경하려고 한다. i = 3 일 때 변경 후에는 `11101`이 나와야 한다. 이때는 **OR 연산**을 이용한다.

	10101 | 1 << 3
	
`1 << 3`은 `1000`이므로 `10101 | 01000`이 되어 `11101`을 만들 수 있다. 

### 2. 삭제 
반대로 0으로 변경하려면, **AND 연산과 NOT 연산을** 활용한다. 
	
	11101 & ~1 << 3
`~1 << 3`은 `10111`이므로, `11101 & 10111`이 되어 `10101`을 만들 수 있다. 

### 3. 조회 
i번째 비트가 무슨 값인지 알려면, **AND 연산을 활용한다.**

	10101 & 1 << i

	3번째 비트 값 : 10101 & (1 << 3) = 10101 & 01000 → 0
	4번째 비트 값 : 10101 & (1 << 4) = 10101 & 10000 → 10000
	
이처럼 결과값이 0이 나왔을 때는 i번째 비트 값이 0인 것을 파악할 수 있다. (반대로 0이 아니면 무조건 1인 것)

이러한 방법을 활용하여 문제를 해결하는 것이 비트마스크다.
	
	