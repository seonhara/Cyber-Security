# NetBIOS
Network Basic input output system : LAN 근거리 통신망 사이에 있는 호스트 간에 서로 통신할 수 있도록 해주는 IBM PC를 위한 네트워크 인터페이스 체계로 이름 해석, 세션, 데이터 그램의 세가지  서비스를 제공하고 있다.
윈도우 : TCP/IP 기반의 Net BIOS 를 기본 서비스로 제공한다.
사용 목적 : SMB 프로토콜을 이용하여 파일, 디렉토리, 프린터 등이 장치를 공유하는 목적으로 주로 사용된다.

**취약점 : NetBIOS TCP/IP 바인딩이 활성화 되어 있으면 인터넷을 통해 외부 공격자가 윈도우 시스템의 네트워크 공유 자원에 접근할 수 있는 취약점이 발생한다.**

**대처 방안 : NetBIOS와 TCP/IP간 바인딩을 제거하는 것이 필요하다.**

- 네트워크 제어판을 이용하여 Net BIOS TCP/IP 바인딩 제거
1. 실행(Windows +R) > ncapa.cpl 입력(네트워크 연결)
<p align="center">
<img src="https://github.com/seonhara/Cyber-Security/blob/main/images/net_bios1.png" alt="Image 1" height="200" />
</p>
   
2. 네트워크 인터페이스 속성 선택
<p align="center">
<img src="https://github.com/seonhara/Cyber-Security/blob/main/images/net_bios2.png" alt="Image 1" height="200" />
</p>

3. TCP/IPv4 속성 선택 
<p align="center">
<img src="https://github.com/seonhara/Cyber-Security/blob/main/images/net_bios3.png" alt="Image 1" height="200" />
</p>

4. 고급 선택 
<p align="center">
<img src="https://github.com/seonhara/Cyber-Security/blob/main/images/net_bios4.png" alt="Image 1" height="200" />
</p>

5. WINS 탭에서 ‘NetBIOS over TCP/IP 사용 안함’ 선택
<p align="center">
<img src="https://github.com/seonhara/Cyber-Security/blob/main/images/net_bios5.png" alt="Image 1" height="200" />
</p>
