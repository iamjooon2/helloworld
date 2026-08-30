
## SNS
- Pub/Sub 기반의 메시징 서비스
	- 하나의 토픽을 여러 주체가 구독
	- 토픽에 전달된 내용을 구독한 모든 주체가 전달받아서 처리한다
- 하나의 메시지를  여러 서비스에서 처리
	- email, http(s), SQS, SMS, Lambda 등등
- Fan Out Architecture 시 주로 사용

## SQS
- Simple Queue Service
- *MSA, Distributed System, Serverless application을 쉽게 분리하고 확장할 수 있도록 지원하는 완전관리형 메시지 대기열 서비스* 
- 말 그대로 Queue - FIFO
	- 다른 서비스에서 사용할 수 있도록 메시지를 잠시 저장하는 용도
	- 26년 8월 현재 기준 최대 14일까지 저장 가능
- 대개 AWS 서비스들의 느슨한 연결을 수립하려 할 때 사용
- 하나의 메시지를 한번만 처리한다
- AWS 내 가장 오래된 서비스라고 😮
- 서비스간의 디커풀링을 위해 주로 사용한다


대개 국룰 패턴은
- 람다, SNS 등에서 SQS에 메시지를 넣고
- 그 다음에 서비스(대개 컨슈머)에서 Queue의 메시지를 Poll 해서 쓰는 패턴이 주요하다
	- Poll : `ReceiveMessage()`
		- 이때 조회만 하지 않고, 큐 안에서 다른 **컨슈머들에게 보이지 않는 상태로 만든다** - 멱등성을 위해
	- Remove :  `DeleteMessage()`
		- 완전 삭제
- 우리 팀도 SNS, SQS 아니면 카프카 - 이런식으로 많이 쓴다



