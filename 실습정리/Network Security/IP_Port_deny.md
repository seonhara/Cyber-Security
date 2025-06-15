# IP 접속 차단 및 도메인을 통해서 사이트 제공
### 💡 보안상 장점

✅ 서버 노출 최소화

✅ IP 스캐닝 공격 방지

✅ 도메인 기반 정책(HSTS, CSP) 유지

✅ SSL 인증서 관련 경고/오류 노출 방지

/etc/nginx/sites-available/default 예시

```
# IP 접속 및 잘못된 Host 헤더 접근 차단 (80 포트)
server {
    listen 80 default_server;
    listen [::]:80 default_server;
    server_name _;

    return 444;  # 응답 없이 연결 끊기
}
```

| <p align="center"><img src="https://github.com/seonhara/Cyber-Security/blob/main/images/ip_deny1.png" height="200"></p> | <p align="center"><img src="https://github.com/seonhara/Cyber-Security/blob/main/images/ip_deny2.png" height="200"></p> |
|:--:|:--:|
| http://IP주소 접속 차단 화면 | https://IP주소 접속 차단 화면 |
---

### 🚀 IP redirect 접속 vs  IP 접속 차단 비교 요약
* 서비스 측면

| 항목        | 차단          | 리다이렉션                 |
| --------- | ----------- | --------------------- |
| 서버 존재     | 숨김 (노출 안 됨) | 노출됨 (IP에 서비스가 있음을 알림) |
| 응답        | 없음 (연결 끊김)  | 301/302 응답 + Location |
| 보안        | 강력          | 상대적으로 노출됨             |
| 사용자 경험    | "접속 불가" 느낌  | 자동 도메인 이동             |
| SEO       | 무관          | 도메인 이동 유도             |
| SSL 경고 위험 | 없음          | IP→HTTPS 리디렉션 시 경고 가능 |

* 보안 측면
  
| 위협           | IP 접속 허용 시            | IP 접속 차단 + 도메인 제공 시 |
| ------------ | --------------------- | ------------------- |
| 서비스 정보 노출    | IP 스캔, 배너 노출          | 존재 자체 숨김            |
| SSL mismatch | 인증서 경고, 정보 노출         | SSL mismatch 시도 불가  |
| 세션 하이재킹      | SameSite, HSTS 미적용 위험 | 도메인 정책 강제 적용        |
| DNS 보안 무효화   | DNS 보안 우회 가능          | DNS 보안 정책 적용        |
| DoS 대응       | IP 트래픽 공격에 취약         | Nginx 레벨 차단         |

---

