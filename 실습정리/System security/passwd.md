# 패스워드 복잡성 설정
위치 :/etc/login.defs
1. 소문자 최소 1자 이상
2. 대문자 최소 1자 이상
3. 숫자 1자 이상
4. 특수문자 1자 이상
5. 최소 8자리 이상 설정
6. 기존 패스워드와 비교 기본 값 10 (50%)

```
lcredit = -1
ucredit = -1
dcredit = -1
ocredit = -1
minlen = 8
difok = N
```

# 계정 잠금 임계값 설정
위치 : /ect/pam.d/systm-auth

```
auth required /lib/security/pam_tally.so deny = 5
unlock_time = 120 no_magic_root
account required /lib/security/pam_tally.so
no_magic_root reset
```
