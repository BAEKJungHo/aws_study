# AWS

# IAM

IAM(Identity and Access Management)은 유저를 관리하고 접근 레벨 및 권한에 대한 관리할 수 있는 웹 서비스.

> AWS 리소스에 대한 액세스를 안전하게 제어할 수 있는 웹 서비스입니다.

## Root User

- AWS 계정을 처음 생성할 때는 해당 계정의 모든 AWS 서비스 및 리소스에 대한 완전한 액세스 권한을 지닌 통합 인증(SSO) 자격 증명으로 시작할 수 있다. 
- 이 자격 증명은 AWS 계정 루트 사용자라고 한다.
- 계정을 생성할 때 사용한 이메일 주소와 암호로 로그인하여 액세스한다. 
- 일상적인 작업, 심지어 관리 작업의 경우에도 루트 사용자를 사용하지 않는 것을 강력히 권장한다. 

## 특징

- 접근키(Access Key), 비밀키(Secret Access Key)
- 매우 세밀한 접근 권한 부여 기능 (Granular Permission)
- 비밀번호를 수시로 변경 가능케 해줌
- Multi-Factor Authentication(다중 인증) 기능

```
- 그룹 (Group)
- 유저 (User)
- 역할 (Role)
- 정책 (Policy) 

- (`*`) 정책은 그룹, 역할에 추가시킬 수 있다.
- (`*`) 하나의 그룹 안에 다수의 유저가 존재 가능하다.
```

## References

- Inflearn. AWS 입문자를 위한 강의
- https://docs.aws.amazon.com/ko_kr/IAM/latest/UserGuide/introduction.html
