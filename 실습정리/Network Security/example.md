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
### 기타
* 무료 도메인 유지를 위한 crontab 설정
  
