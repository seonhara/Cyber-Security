# 웹서비스 정보 노출 취약점 점검
### Foodie-Guide web service 예시
**취약점 패치 전**
| <p align="center"><img src="https://github.com/seonhara/Cyber-Security/blob/main/images/info_dis1.png" width="500" height="200"></p> | <p align="center"><img src="https://github.com/seonhara/Cyber-Security/blob/main/images/info_dis2.png" width="500" height="200"></p> |
|:--:|:--:|
| 웹서버 버전 노출 확인 | 브라우저 에러 페이지 부재 확인 |

---
## 1️⃣ Nginx에서 server_tokens 제거 (버전 숨기기)

`/etc/nginx/nginx.conf` 의 http 블록 안에 추가합니다.
```
http {
    server_tokens off;

    # 기존 설정들...
}
```

## 2️⃣ Nginx 커스텀 404 에러 페이지 설정
1. 404 에러 페이지 파일 만들기
Nginx의 기본 HTML 폴더(`/usr/share/nginx/html`) 또는 프로젝트 폴더에 파일 생성
```
sudo nano /usr/share/nginx/html/custom_404.html
```

2. Nginx 설정에 커스텀 404 페이지 지정
* 404 에러 발생 시 /usr/share/nginx/html/custom_404.html 제공
* internal → 직접 URL로 접근 불가 (보안)
 `/etc/nginx/sites-available/ooo` 또는 Nginx 설정 파일에서 server 블록에 추가:
```
server {
    listen 443 ssl;
    server_name foodie-guide.duckdns.org;

    # SSL 설정 ...
    # proxy_pass ...

    error_page 404 /custom_404.html;
    location = /custom_404.html {
        root /usr/share/nginx/html;
        internal;
    }
}
```
---
결과
**취약점 패치 후**
| <p align="center"><img src="https://github.com/seonhara/Cyber-Security/blob/main/images/info_dis1_after1.png" width="500" height="200"></p> | <p align="center"><img src="https://github.com/seonhara/Cyber-Security/blob/main/images/info_dis1_after2.png" width="500" height="200"></p> |
|:--:|:--:|
| 웹서버 버전 제거 확인 | 브라우저 에러 페이지 확인 |
