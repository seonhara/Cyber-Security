## 📦 예: AWS에 TLS 적용
AWS EC2에 Vite 앱을 올렸다면, Nginx + Certbot 사용해 TLS 적용 가능
적용 후 "http://" 접속 시 "https://"로 리디렉션하면 안전한 웹 완성
* 사전 조건
  * 도메인 없이 TLS를 발급받을 수 없음
  * 이유:
    * 무료 TLS 발급 서비스의 도메인 소유권 검증 필요
    * 브라우저가 도메인 이름을 기준으로 인증서 유효성 검증
    * IP 주소 기반 인증서는 매우 드물고 유료이며 제한적

### TLS 적용 전후 비교
<p align="center">
  <img src="https://github.com/seonhara/Cyber-Security/blob/main/images/tls_before.png" alt="Image 1" height="200" width ="250" />
    &nbsp;&nbsp;&nbsp;&nbsp; <!-- 사진 사이 여백 -->
  <img src="https://github.com/seonhara/Cyber-Security/blob/main/images/tls_complete.png" alt="Image 2" height="200" width ="250" />
</p>

---

### Certbot 설치 및 인증서 발급
```
sudo apt install certbot python3-certbot-nginx -y
sudo certbot --nginx -d yourname.duckdns.org
```
<p align="center">
<img src="https://github.com/seonhara/Cyber-Security/blob/main/images/tls_certbot.png" alt="Image 1" height="200" />
</p>

---
### 인증서 자동 갱신 테스트
```
sudo certbot renew --dry-run
```
<p align="center">
<img src="https://github.com/seonhara/Cyber-Security/blob/main/images/tls_renew_check.png" alt="Image 1" height="200" />
</p>

---
### Nginx 80 포트용 리다이렉트 설정
Nginx 설정 파일(예: /etc/nginx/sites-available/default 또는 별도 설정 파일)에 80 포트 리다이렉트용 server 블록을 추가
```
server {
    listen 80;
    server_name foodie-guide.duckdns.org;

    return 301 https://$host$request_uri;
}
```
* 의미
return 301 → 영구 리다이렉트
$host → 클라이언트가 요청한 도메인 그대로 유지
$request_uri → 경로/쿼리 파라미터도 그대로 유지

---
### HTTPS 리디렉션이 방어에 효과적인 주요 사이버 공격

| 공격 유형                                | 설명                                        | HTTPS 리디렉션 방어 효과                                                         |
| ------------------------------------ | ----------------------------------------- | ------------------------------------------------------------------------ |
| **세션 하이재킹 (Session Hijacking)**      | 공격자가 쿠키나 세션 토큰을 탈취해 사용자의 인증된 세션을 가로채는 공격  | HTTPS로 세션 쿠키를 암호화 전송하고, `Secure` 플래그로 HTTPS에서만 쿠키 전송되도록 제한해 **쿠키 탈취 방지** |
| **중간자 공격 (MITM: Man-in-the-Middle)** | 클라이언트와 서버 사이에 공격자가 개입해 데이터를 도청하거나 변조하는 공격 | HTTPS는 전송 중 데이터가 암호화되어 있어 **패킷 도청 및 조작 불가**                              |
| **DNS 스푸핑**                          | 가짜 DNS 응답을 보내 사용자 트래픽을 공격자 서버로 유도         | HTTPS는 도메인 인증서를 검사하므로 **잘못된 서버로의 연결 차단**                                 |
| **피싱 공격 유도**                         | 사용자를 **`http://IP`나 유사한 도메인으로 유도 후 악성 행위**    | 사용자가 항상 `https://도메인`으로 접속되게 하면 **피싱 유도 방지**                             |
| **쿠키 탈취 (Session Cookie Theft)**     | 비암호화된 HTTP로 전송되는 쿠키를 스니핑해서 탈취             | HTTPS + `Secure` 속성으로 쿠키를 암호화된 채널에서만 전송하게 하여 **쿠키 탈취 불가**                |
| **사이트 변조 (Content Injection)**       | 공공 와이파이 등에서 HTML에 악성 스크립트를 삽입하는 공격        | HTTPS는 콘텐츠 무결성을 보장하여 **스크립트 삽입 불가**                                      |


---
## 정리
🔐 요약: HTTPS 리디렉션의 보안 효과
* 데이터 전송 암호화 → MITM, 세션 하이재킹 방지
* 세션 쿠키 보호 → 세션 탈취 방지
* 브라우저 인증서 검사 → DNS 스푸핑 방지
* 피싱 및 콘텐츠 변조 방지 → 사용자 신뢰 확보
---
### 기타
* 무료 도메인 유지를 위한 crontab 설정
  
