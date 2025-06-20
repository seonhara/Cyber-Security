# 1️⃣ 쿠키에 Secure 플래그 설정
"Set-Cookie 응답헤더"에 설정하는 속성으로 클라이언트에서 **https통신일 경우에만 해당 쿠키를 전송하고 http 통신일 경우에는 전송하지 않는 속성**이다.

💡 목적: 중간자공격 방지 = 쿠키의 기밀성 보장

전송 중에 평문 쿠키가 노출되는 것을 방지(네트워크 스니핑 공격 대응)하기 위한 목적이다.
```
Set-Cookie: sessionId=abc123; Secure
```

# 2️⃣ 쿠키에 HttpOnly 플래그 설정
"Set-Cookie 응답헤더"에 설정하는 속성으로 클라이언트에서 스크립트(자바스크립트 등)를 통해 해당 쿠키에 접근하는 것을 차단해주는 속성이다.

💡 목적: 클라이언트에서 스크립트(JavaScript)를 통한 쿠키에 접근하지 못하게 하여 악의적인 쿠키 정보 탈취 방지, XSS로부터 세션 탈취 방어
```
Set-Cookie: sessionId=abc123; HttpOnly
```

# 3️⃣ 쿠키에 SameSite 플래그 설정
💡 목적:
다른 사이트에서 오는 요청에 쿠키가 전송되지 않도록 해 CSRF 방어

💡 SameSite 값

Strict: 다른 사이트 요청에는 쿠키 절대 전송 안 함 (보안 최고)

Lax: 링크 클릭은 허용, POST/Form 등에는 전송 안 함

None; Secure: 교차 사이트 전송 허용하되 Secure 필요

```
Set-Cookie: sessionId=abc123; SameSite=Strict
```
# 4️⃣ 쿠키에 Expires 플래그 설정
💡 목적:
쿠키의 유효기간을 설정하는 옵션으로 유효기간을 최소한으로 설정하여 쿠키 정보가 클라이언트의 하드디스크 등에 지속해서 남아 공격자에게 노출되는 위험을 방지할 수 있다.

---
🚀 요약
| 설정       | 방어 효과                    |
| -------- | ------------------------ |
| Secure   | HTTPS에서만 쿠키 전송 (MITM 방어) |
| HttpOnly | JS 접근 차단 (XSS 방어)        |
| SameSite | CSRF 방어                  |
| Expires  | 쿠키 노출 방어                  |

