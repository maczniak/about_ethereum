
BFT-SMaRt를 조사하고 있습니다. "total order multicast (tom)"와 "reliable
 authenticated link" 같은 개념을 알기위해 "Introduction to Reliable and Secure
 Distributed Programming (2nd)" (2011, Springer)을 함께 읽고 있습니다.

BFT-SMaRt는 DepSpace coordination service에서 시작하여 독립된 BFT 복제
 라이브러리를 거쳐 5년 이상 개발했고, 현재 Symbiont과 R3 Corda 등
 [다양하게](https://github.com/bft-smart/library/wiki/Used-in-and-by...)
 사용하고 있습니다.

BFT SMR(state machine replication) 계열에 속하며 버그도 많고 현재 관리되지 않는
 PBFT와 UpRight 그리고 (CFT only) JPaxos와 비교하여 안정성, 모듈화, 멀티코어
 활용, 재설정(reconfiguration, 동적인 노드 추가 제거) 지원, 유연한 API를
 장점으로 주장합니다. 기본적으로는 다른 BFT 복제처럼 악의적이지 않은 BF를
 방어하지만, CFT만 방지하거나 악의적인 공격도 방어하도록 변경할 수 있습니다.

네트워크 노드는 replica와 client로 구분합니다. 소수의 replica는 동의 과정에 직접
 참여하고, 다수의 client는 replica를 통해 요청을 합니다. (그러나 replica와
 client를 동일한 클래스로 구현했다고 합니다.)<br>
과정은 다른 BFT와 유사합니다. 리더가 PROPOSE하면, 다른 replica들은 검증 후
 약하게 인정하고(weaky accept) WRITE 메시지를 방송합니다(broadcast). replica가
 WRITE 메시지를 (n+f)/2개 이상 수신하면 강하게 인정하고(strongly accept) ACCEPT
 메시지를 방송합니다. replica가 ACCEPT 메시지를 (n+f)/2개 이상 수신하면 합의를
 결정하고 로그에 기록합니다.<br>
프로세스가 복구하거나 노드를 추가할 때 STATE_REQUEST와 STATE_REPLY 메시지를
 사용하여 state transfer를 진행합니다.<br>
노드를 추가하거나 제거할 때, 즉 재설정시, View Manager를 통합니다. View
 Manager가 변경이 있는 replica 정보를 방송하면, replica들은 cv(current view)를
 갱신하고 응답합니다. 응답을 받은 View Manager는 새로운 노드에서 동작을 시작해도
 된다고 알립니다. 동일한 과정으로 f 값 변경을 알리기도 합니다. client도 자체
 cv를 유지하고 모든 요청에 cv 정보를 포함합니다. 만약 replica가 이전 cv를 가진
 client 요청을 받으면, replica는 자신의 cv를 클라이언트에게 알려주어 갱신하게
 합니다.

자바 [소스코드](https://github.com/bft-smart/library)는 오픈소스로 공개되었고,
 [시각화 도구](https://github.com/varijkapil13/BFT-SMaRt-Visualization-/tree/visualization)도
 발견했습니다.<br>
실제 BFT-SMaRt를 사용한다면, 클래스들을 상속하여 현재 적용하려는 용도의 고유
 기능을 추가 구현해야 합니다 (예, 링크드 리스트를 저장하는 인메모리 표를 구현한
 `BFTMapList` 서비스).<br>
그동안 구현에 참여한 개발자들이 크기에 비해 가장 복잡한 소스코드라고 평가했다고
 합니다. 처음 보기에 불필요해 보이는 부분이 많지만, BFT-SMaRt를 실제 다양한
 프로젝트에 적용하면서 발견한 버그 때문에 추가된 부분입니다. 프로토콜 명세와
 실제 효율적이고 안정적인 구현 사이에 간격이 넓습니다.

앞으로 동작을 이해하기위해 코드를 살펴보려고 합니다.

