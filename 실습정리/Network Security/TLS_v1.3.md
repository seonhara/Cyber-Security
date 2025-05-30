# TLS(Transport Layer Security) v1.3

## TLS의 보안성
### TLS v1.3사용 여부 확인

```
openssl s_client -connect <도메인>:443 -tls1_3
```
s_client : SSL/TLS 서버와의 연결을 시도해서 인증서, 프로토콜 버전, 암호화 알고리즘 등을 직접 확인함

<p align="center">
<img src="https://github.com/seonhara/Cyber-Security/blob/main/images/tls1.3.png" alt="Image 1" height="200" />
</p>

### ✅ **TLS 1.3이 TLS 버전 중 가장 안전한 이유**

**1. ❌ 낡고 취약한 암호 알고리즘 제거**

RC4, MD5, SHA-1, EXPORT cipher, CBC 모드 등 과거 공격 사례가 있었던 알고리즘들을 완전히 제거

▶︎ 공격자가 과거 알고리즘의 취약점을 이용해 암호 해독을 시도하는 걸 원천 차단

**2. ✅ Forward Secrecy (전방향 기밀성) 강제 적용**

세션 키를 Ephemeral Diffie-Hellman (DHE, ECDHE) 방식으로 매번 새롭게 생성

▶︎ 서버 Private Key가 노출되더라도 과거 세션은 복호화할 수 없음

**3. ⏩ 핸드셰이크 과정 간소화 (1-RTT)**

핸드셰이크를 한 번만 왕복(1-RTT)하면 완료

▶︎ 초기 통신 속도 향상 + 중간자 공격(MITM)에 노출될 기회를 줄임

**4. 🔒 암호화 적용 범위 확장**

핸드셰이크의 대부분 메시지를 암호화

▶︎ 인증서 정보 외에도 협상 정보까지 암호화되어 패킷 분석/추적 방지

**5. 🧼 클리어 텍스트 제거 (예: Client Finished Message)**

평문 교환 최소화 → 정보 노출 가능성 대폭 축소

**6. ✅ Zero Round Trip Resumption (0-RTT) 도입 (옵션)**

이전 세션 정보를 이용해 빠르게 재연결 가능 (단, 재전송 공격 주의 필요)

▶︎ 사용자 경험 개선 + 성능 향상, 단 선택적으로 사용해야 함


