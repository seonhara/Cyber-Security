## 🔹배너 메시지 설정
### 주요 통신 기반 시설 가이드(3. 서비스 관리 > 3.3.2. 로그온 시 경고 메시지 제공)
1. telnet 배너 설정 파일(/etc/issue.net)에 적절한 로그인 배너 메시지를 설정한다.
   ![보안 개념 정리](https://github.com/seonhara/Cyber-Security/images/banner1.png)
2. 배너 활성화
   sudo nano /etc/ssh/sshd_config
   Banner /etc/issue.net
  ![보안 개념 정리](https://github.com/seonhara/Cyber-Security/images/banner2.png)
3. 변경사항 적용 시 SSH 서비스 재시작
   sudo systemctl restart ssh
   ![보안 개념 정리](https://github.com/seonhara/Cyber-Security/images/banner3.png)
4. 배너 확인
   /etc/ssh/sshd_config
   ![보안 개념 정리](https://github.com/seonhara/Cyber-Security/images/banner4.png)
