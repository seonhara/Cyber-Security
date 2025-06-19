# 서비스 정보 노출이란?
💡 웹 애플리케이션 또는 웹 서버가 다음과 같은 정보를 의도치 않게 노출하는 것:
* 서버 종류 (Apache, Nginx, Express, etc.)
* 서버 버전 (e.g. Apache/2.4.29)
* X-Powered-By, Server 헤더
* 프레임워크/언어 정보 (PHP, ASP.NET, Node.js 등)
* 디렉토리 구조, 파일 경로, 에러 메시지
* 디버그 메시지, 스택 트레이스
* API endpoint 설명, Swagger 문서 노출

## 점검 방법

```
curl -I https://your-domain.com
```

# 웹 서비스 정보 노출 대응 방법
1. 서버 헤더 정보 제거
2. 에러 페이지 제공 
---
### 1. 서버 헤더 정보 제거
* 버전 제거
* Express 등 추가 헤더 제거
* 에러 페이지 하단의 서버정보 제거

**Nginx**

```
server_tokens off;
add_header X-Powered-By "";
```

**Apache**
```
ServerTokens Prod
ServerSignature Off
```

---
### 2. 에러페이지 제공
* 404 발생 시 커스텀 에러 페이지 제공
* 내부 경로나 코드 노출 없이 사용자 친화 메시지

**Nginx**
```
error_page 404 /custom_404.html;
location = /custom_404.html {
    root /usr/share/nginx/html;
}
```

**Apache**
```
ErrorDocument 404 /custom_404.html
```
