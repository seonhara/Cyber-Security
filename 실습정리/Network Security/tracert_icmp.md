# Tracert(Windows) 명령
* 개념: 종단 구간 사이의 경로를 추적하기 위한 명령
* 목적: 종단 사이에 있는 라우터나 L3 장비 같은 중계 노드를 식별하고 각 구간에 대한 네트워크 상태를 점검하기 위한 명령으로 네트워크 라우팅 문제점을 찾아내는 목적으로 주로 사용한다.
* 유닉스/리눅스의 경우: tracerout 명령
* 두마디 정리 :
  
    `1) TTL 값을 1씩 증가 시키면서 ICMP Echo Request 패킷을 전송하여 다음 중계 구간에 대한 네트워크 상태를 점검한다.`
  
    `2) TTL 초과 시 ICMP Time Exceeded 메시지로 응답하며 목적지 호스트 도달 시 ICMP Echo Reply 메시지로 응답한다.`

* 동작 원리:
    1. 각 중계 노드 구간의 네트워크 상태를 점검하기 위해 IP 패킷의 TTL(Time To Live) 값을 1로 설정한 ICMP Echo Request 패킷을 보낸다.
    2. 라우터는 IP 패킷의 생존 기간을 계산하기 위해 패킷을 수신하면 TTL 값을 1 감소시킨 후 0 이 되면 TTL 초과로 판단하여 해당 패킷을 폐기한 후 ICMP Time Exceeded(Type 11) 오류 보고 메시지를 생성하여 출발지 호스트로 보낸다.
    3. 따라서 TTL 값을 1로 설정하면 첫번째 라우터에서 IP 패킷이 폐기되고 ICMP 응답이 오기 때문에 이를 이용하여 출발지 호스트와 첫번째 라우터 구간의 네트워크 상태를 점검할 수 있다.
    4. 목적지 호스트에 ICMP Echo Request 패킷이 도달하면 ICMP Echo Reply 패킷이 반환되며 출발지 호스트는 이 정보를 이용하여 목적지 호스트에 도달했음을 알 수 있게 된다.
       
* 보안:
  보안 상의 이유로 라우터에서 ICMP 응답을 보내지 않는 경우가 많다.
  명령 수행시 왕복 시간이 '*'로 표시되는 경우 응답이 없는 경우로 보안상 이유이거나 실제 해당 구간에 문젝 발생한 경우로 판단할 수 있다.

  <p align="center">
  <img src="https://github.com/seonhara/Cyber-Security/blob/main/images/tracert1.png" alt="Image 1" height="200" width ="250" />
    &nbsp;&nbsp;&nbsp;&nbsp; <!-- 사진 사이 여백 -->
  <img src="https://github.com/seonhara/Cyber-Security/blob/main/images/tracert2.png" alt="Image 2" height="200" width ="250" />
</p>

* AWS에서 화이트리스트 방식으로 네트워크 관리 : 기본적으로 ICMP 요청(ping) 차단
  인바운드 규칙에 ICMP-Echo Request 규칙 허용이 설정되어 있지 않음을 확인할 수 있음

--- 
🟡 **보안상 이유**

🔹 보안 강화 - ICMP 요청을 허용하면 **서버가 네트워크에서 탐색**될 수 있어 공격 대상이 될 가능성이 높아진다.

🔹 DDoS 공격 방지 – **ping 요청을 악용한 DDoS 공격(예: ICMP Flooding)을 방지**하기 위함이다.

🔹 네트워크 트래픽 관리 – **불필요한 ICMP 트래픽을 줄여 네트워크 성능을 최적화**하고, 중요한 서비스(웹 트래픽 등)에 우선순위를 부여한다.

