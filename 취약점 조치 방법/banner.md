## 🔹배너 메시지 설정
### 주요 통신 기반 시설 가이드(3. 서비스 관리 > 3.3.2. 로그온 시 경고 메시지 제공)
1. telnet 배너 설정 파일(/etc/issue.net)에 적절한 로그인 배너 메시지를 설정한다.
<p align="center">
  <img src="https://github.com/seonhara/Cyber-Security/blob/main/images/banner1.png" alt="Image 1" height="200" />
</p>
2. 배너 활성화

   ```
   sudo nano /etc/ssh/sshd_config
   Banner /etc/issue.net
   ```
   
   * 적용 예시
   <p align="center">
     <img src="https://github.com/seonhara/Cyber-Security/blob/main/images/banner2.png"alt="Image 1" height="200" />
      &nbsp;&nbsp;&nbsp;&nbsp; <!-- 사진 사이 여백 -->
      <img src="https://github.com/seonhara/Cyber-Security/blob/main/images/banner3.png"alt="Image 1" height="200" />
  </p>
  
3. 변경사항 적용 시 SSH 서비스 재시작

   ```
   sudo systemctl restart ssh
   ```
   
5. 배너 확인

   ```
   /etc/ssh/sshd_config
   ```
   <p align="center">
   <img src= "https://github.com/seonhara/Cyber-Security/blob/main/images/banner4.png" alt="Image 1" height="200" />
   </p>
